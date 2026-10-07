# Unit 3 — Plan and Build

## Posted upstream

### GitHub username

pclerveau2025

### Plan comment

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73#issuecomment-6029902230

Plan for #73, built on my reproduction above at f89c06f.

**Diagnosis.** In my repro, `README.md:24` and `docs/SETUP.md:47` both say to set `OPENROUTER_API_KEY`, and `core/config.py:20` declares `openrouter_api_key`. But after the Quick Start `cp .env.example .env`, `grep -c "OPENROUTER_API_KEY" .env` printed `0`, and `Settings()` resolved `openrouter_api_key -> ''`. Two docs and the config agree; `.env.example` is the file that's missing the key.

**Change.** `.env.example` only. Under the existing `OPENAI_API_KEY` line, add a one-line comment and `OPENROUTER_API_KEY=sk-or-your-key-here`, matching the existing placeholder style.

**Not in scope.** `README.md`, `docs/SETUP.md`, `core/config.py`, the `# Options:` line, the `LLM_PROVIDER=mock` default, and `OPENROUTER_BASE_URL` / `OPENROUTER_MODEL` (config.py already has defaults for those).

**Test.** Re-run my repro steps unchanged on the branch. I expect `grep -c "OPENROUTER_API_KEY" .env` to go from `0` to `1`, and `Settings()` to give `openrouter_api_key -> 'sk-or-your-key-here'` instead of `''`, with `llm_provider -> 'mock'` and `openai_api_key` unchanged.

**Unknowns.** I haven't confirmed which `LLM_PROVIDER` value, if any, selects OpenRouter at runtime, so I'm leaving the `# Options:` line alone. If a maintainer confirms a value, I can add it.

**Relation to PR #77.** #77 also targets this issue and documents `LLM_PROVIDER=openrouter`. My change is narrower because I can't show that value does anything yet. If maintainers prefer #77's direction, I'll drop mine.

Branch: `fix/73-env-example-openrouter-key` on my fork.

Disclosure: I used Claude to help draft this plan. I ran the repro commands and checked the output myself.

## Your branch

### Branch

fix/73-env-example-openrouter-key

## Evidence

Run from the root of my fork's clone, after `cp .env.example .env`, using the same commands as my Unit 2 repro.

Before (main, f89c06f):

    $ grep -c "OPENROUTER_API_KEY" .env
    0
    $ grep -n -A5 "# LLM provider" .env
    16:# LLM provider
    17-# Options: "mock" (default, no API key needed), "openai"
    18-LLM_PROVIDER=mock
    19-OPENAI_API_KEY=sk-your-key-here
    20-
    21-# App settings
    $ Settings check
    llm_provider -> 'mock'
    openai_api_key -> 'sk-your-key-here'
    openrouter_api_key -> ''

After (fix/73-env-example-openrouter-key, commit 4826698):

    $ grep -c "OPENROUTER_API_KEY" .env
    1
    $ grep -n -A5 "# LLM provider" .env
    16:# LLM provider
    17-# Options: "mock" (default, no API key needed), "openai"
    18-LLM_PROVIDER=mock
    19-OPENAI_API_KEY=sk-your-key-here
    20-# OpenRouter key named in README Quick Start and docs/SETUP.md
    21-OPENROUTER_API_KEY=sk-or-your-key-here
    $ Settings check
    llm_provider -> 'mock'
    openai_api_key -> 'sk-your-key-here'
    openrouter_api_key -> 'sk-or-your-key-here'

## Eval iterations

### Run history

Run 1 (full run, saved as eval-run.txt): agreement 19/20 scored items (bar: 18/20: PASS). Categories: clear-accept 6/7, scope-creep 4/4, thread-convention 2/2, unbuildable 3/3, wrong-cause 4/4.

### Package analysis

pkg-14 (zellij-org/zellij#5174, category clear-accept). My rubric decided reject; the gold label is accept. It failed my `executable` check (and the preferred `honest-unknowns` check, which does not affect the verdict). The plan's Files section says "exact functions to be pinned in the PR after tracing the query issuance with debug logs". My `executable` check fails a plan whose first step is to investigate before the change is decided, so the grader read "to be pinned later" as an undecided code location. The gold label accepts it because the plan does name the area (the reattach path in `zellij-server`'s client connection handling), commits to one approach (drain OSC responses before pane input is wired), and has a decisive test (5 SSH reattach cycles with no rgb strings). My check is stricter than gold here: it treats "I know the area and the approach but not the function name yet" the same as "I don't know which layer".

### Check rationale

| bounded-scope | Every change listed in the candidate plan (change/approach section, files, "while I'm here" items), read against the behavior the issue and repro evidence describe | Pass if every planned change is needed to fix the reproduced behavior. Fail if the plan also commits to any work the issue did not ask for: a refactor, rewrite, migration, dependency upgrade, new option/setting/UI, new framework, CI or test-harness change, or "unify across other constructs", even when the core fix inside it is correct. Work the plan explicitly defers or marks out of scope does not count against it; an honest scope-down is a pass. | required |

It reads this way because the scope-creep packages are dangerous precisely when the core fix is right. pkg-15 has the correct one-constant fix but bundles a migration, a settings panel and a retry framework, so the condition says "even when the core fix inside it is correct". I rejected a looser condition that only asked whether the plan contains a correct bounded fix, because that would pass pkg-15. The last sentence ("Work the plan explicitly defers or marks out of scope does not count against it; an honest scope-down is a pass") is there so plans like pkg-09 and pkg-14 that defer work with reasons are not read as scope problems. The list of creep types (refactor, migration, dependency upgrade, new option, CI or test-harness change) comes from the patterns in pkg-06, pkg-12, pkg-15 and pkg-19.

### Trade-offs

My `executable` check gives up pkg-14: requiring a concrete code location plus one approach rejects a sound plan that names the area and approach but defers the exact function to tracing. I accepted that miss rather than loosening the check, because loosening it to "names an area" risks passing pkg-17 and pkg-18, which also gesture at an area ("the input stack", "somewhere") without deciding anything. Separately, my live run on my own plan flagged a procedure gap: the procedure does not say whether a non-maintainer PR like #77 counts as maintainer direction for `thread-direction`. It graded #77 as not direction; I left the files unchanged so they match the fingerprints in eval-run.txt.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in `tools/plan-check/`.
