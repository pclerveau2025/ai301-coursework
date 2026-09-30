# Unit 2 — Claim and Reproduce

## Your identity upstream

### GitHub username

pclerveau2025

## Posted upstream

### Claim comment

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5902145888

Hi, I'm a new contributor working through a course, and I'd like to take this one.

As I read it: the README's Quick Start says to add OPENROUTER_API_KEY to .env and then copy .env.example, but .env.example has no OPENROUTER_API_KEY line, and its LLM_PROVIDER comment lists only mock and openai. core/config.py declares both openai_api_key and openrouter_api_key.

My next step is to clone my fork on macOS, follow the Quick Start's copy step exactly, and record what the resulting .env contains and what the app's Settings object resolves for each key. I'll post a repro report here with my environment, commit, steps, and output, whether or not it reproduces. I'm not promising a fix or a date.

Disclosure: Claude to help draft this comment a little bit

### Reproduction comment

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-5902300812

Result: reproduced on macOS at f89c06f. After the README's cp step, my .env had zero OPENROUTER_API_KEY lines, and loading core/config.py's Settings gave openrouter_api_key -> ''.

Environment

OS: macOS 26.5.1 (build 25F80), arm64
Python 3.12.7, git 2.50.1 (Apple Git-155)
Fresh clone of my fork pclerveau2025/pathreview-ai301-fa26-s1 at https://github.com/codepath/pathreview-ai301-fa26-s1/commit/f89c06fc3ff292df2a04a39ac51319d32a76b779 (2026-09-16), main, clean working tree
For the Settings check only: a throwaway venv with pydantic 2.13.5 and pydantic-settings 2.15.0. I skipped docker compose and make setup; this issue is about which variables the docs and template name, and the Settings check only needs core/config.py and its two dependencies.
Steps (from the repo root)

git clone https://github.com/pclerveau2025/pathreview-ai301-fa26-s1.git
cd pathreview-ai301-fa26-s1
git checkout f89c06fc3ff292df2a04a39ac51319d32a76b779

# What the setup docs ask for
grep -n "OPENROUTER_API_KEY" README.md docs/SETUP.md

# The Quick Start copy step, verbatim
cp .env.example .env
grep -c "OPENROUTER_API_KEY" .env
grep -n -A3 "# LLM provider" .env
grep -n "api_key\|llm_provider" core/config.py

# What the app resolves
python3 -m venv /tmp/prvenv
/tmp/prvenv/bin/pip install "pydantic[email]>=2.5.0" "pydantic-settings>=2.1.0"
/tmp/prvenv/bin/python -c "
from core.config import Settings
s = Settings()
for k in ('llm_provider', 'openai_api_key', 'openrouter_api_key'):
    print(k, '->', repr(getattr(s, k)))
"
Expected

The README says to add OPENROUTER_API_KEY to .env and to create .env by copying .env.example. After both steps, the .env should have an OPENROUTER_API_KEY line to fill in.

Actual

README.md:24:# Configure environment (add your OPENROUTER_API_KEY to .env)
docs/SETUP.md:47:# Edit .env and set your OPENROUTER_API_KEY (required for AI features)

$ grep -c "OPENROUTER_API_KEY" .env
0

16:# LLM provider
17-# Options: "mock" (default, no API key needed), "openai"
18-LLM_PROVIDER=mock
19-OPENAI_API_KEY=sk-your-key-here

core/config.py:
18:    llm_provider: str = Field(default="mock")
19:    openai_api_key: str = Field(default="")
20:    openrouter_api_key: str = Field(default="")

Settings output (run from my clone):
llm_provider -> 'mock'
openai_api_key -> 'sk-your-key-here'
openrouter_api_key -> ''
README.md names OPENROUTER_API_KEY, and so does docs/SETUP.md:47 (@morishbhayani spotted that one first; I confirmed it on my clone). The template they tell you to copy has zero occurrences of it and lists only mock and openai as providers. core/config.py does declare openrouter_api_key, and it resolves empty after the documented setup.

Limits of this check

This covers the setup path only: what the docs say, what the copied .env contains, and what Settings loads. I never started the app or called a provider, so I can't say whether the empty key causes a failure at runtime. Which file should change to match the other is for a maintainer to decide.

Disclosure: I used Claude to help draft this report. I ran the commands and checked the output myself.


## Eval iterations

### Run history

1. Full run: 14/20 scored items (below the bar). Categories: clear-accept 2/8, disclosure 1/1, no-evidence 4/4, unfollowable-comms 3/3, wrong-target 4/4.
2. Partial run with `--only pkg-01,pkg-03,pkg-05,pkg-07,pkg-11,pkg-12,pkg-20`: 7/7 (the six misses plus pkg-20 as the disclosure canary).
3. Confirming full run with `--save-run eval-run.txt`: 20/20 scored items (bar: 18/20: PASS). This matches the agreement line in the committed eval-run.txt.

### Package analysis

pkg-07 (processing/p5.js#7168). Gold label: accept. My rubric's first run: reject, with the note "failed: claim-promise, conventions-disclosure, voice". Final run: accept, matching gold.

Why it read it that way the first time: my original claim-promise check said the claim must have "no fix, PR, date, or assertion that it already reproduced". pkg-07's claim is written after reproducing, so it states the repro, and my check failed it even though the attached report backs that statement up. The conventions-disclosure check originally pointed at "Repo policy (scope.md, CONTRIBUTING)", which let the grader mix in the wrong repo's policy instead of reading p5.js's own repo-facts block. The gold note says the package "discloses AI assistance as p5.js's stated policy requires, which is what the conditional-policy pass looks like". After I made claim-promise allow a backed repro statement and tied conventions-disclosure to "The package's own repo-facts block", the rubric accepted pkg-07.

### Check rationale

Quoted from tools/repro-check/rubric.md as it reads now:

"| claim-promise | Claim comment vs repro report | States a concrete next step in the investigation; never promises a fix, PR, or date. Saying it already reproduced is fine when the package's repro report shows it; fails only if the claim asserts a repro that no report backs | required |"

Why it reads that way: the first version banned any "assertion that it already reproduced". That failed all six clear-accept misses in run 1 (pkg-01, 03, 05, 07, 11, 12), because eval claims are written after the repro, like pkg-01's "I can reproduce the missing Content-Type: application/json on 3.2.4". The real problem the check guards against is over-promising (pkg-19's "guaranteed 2-day fix") or claiming a repro with nothing behind it, so I kept the ban on fix/PR/date and made the repro statement conditional on the report backing it.

### Trade-offs

Loosening claim-promise means the check no longer catches a claim that states a repro on its own; it now relies on the repro checks (repro-evidence, repro-target, honest-outcome) to catch a claim whose report is weak. Because the change loosened a check, I re-ran pkg-20 (the single disclosure package) as a canary with `--only`, and it stayed reject. The confirming full run then showed the loosening flipped nothing that agreed before: every no-evidence, wrong-target, and unfollowable-comms package still rejected, including pkg-19, which still fails on its over-promising claim.
