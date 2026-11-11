# Contribution: Add example curl commands to the API docs

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** 1
**Student:** Patrice
**GitHub Username:** pclerveau2025
**Issue:** https://github.com/codepath/pathreview-ai301-fa26-s1/issues/47
**Pull Request:** https://github.com/codepath/pathreview-ai301-fa26-s1/pull/253

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Built an issue scout that searches Path Review and grades candidates**

I built a scout that searches Path Review for open "good first issue" + "tier-1" issues, drops assigned or stale ones, ranks by fewest comments, and grades the top five. My first scan rejected four of five issues because the "Not already claimed" check counted classmates' open PRs, which the Path Review house rule says shouldn't block an issue. I edited that row in rubric.md so classmates' open PRs don't count in Path Review, while merged PRs and closed issues still fail. When I graded my two picks, #12 and #37, both were accepted, and #37 only passed because of the fix.

**Unit 6: Installed a voice guard and wrote my upstream rules**

I wrote upstream rules for claims, questions, and pings into my voice guide and installed a hook that checks every comment I post through Claude Code. The first settings write failed silently, so the hook check said "not found"; I rewrote it with a short Python command and the wiring test then blocked the body-less command as it should. My first claim draft included a promise I never asked for, that I would run every command myself, and I posted it unchanged. I did not run the curl commands before opening my PR, so I broke that promise at first and only kept it afterward, when I ran all four against a local server. I now read drafts for added promises before posting.

**Unit 7: Installed the ship-gate and wrote my manifest**

I installed the ship-gate and wrote a manifest with two checks from CONTRIBUTING.md, make check and make test-unit. Its hook test stopped gh pr create with no PR text, as expected, and on my branch it ended with ship-gate: PASS. My local clone was still on an old branch with leftover files from a different issue, so I switched to main and moved those files out before the gate ran. Its notes also flagged that my claim promised to run every command myself while my PR said I had not, so I ran them against a local server afterward.

**Unit 8: Installed the PR monitor and wrote my playbook**

I installed the PR monitor and wrote a playbook from CONTRIBUTING.md, which asks me to answer reviewers within 48 hours but states no maintainer wait time. No PRs have merged in this repo, so I could not measure a real wait and set a 7-day nudge threshold as a guess. On my PR, which was under a day old with 5 passing checks and no comments, it drafted a wait note, so I posted nothing. I would revise the threshold once any PR in this repo merges.

---

## Why I Chose This Issue

I searched the Path Review repo with my scout for open "good first issue" + "tier-1" issues, dropped assigned or stale ones, and ranked by fewest comments. The first scan rejected four of five issues because classmates had open PRs on them. I fixed that check and graded my two picks, #12 and #37. Both were accepted, but #12 already had a classmate asking to work on it and #37 already had a classmate's open PR, so I treated both as taken. A second scan showed #11 and #47 had no claims and no PRs, but my 60-day filter had kept them out of grading. I graded #47 directly and it was accepted: one task in one file, adding example curl commands to docs/API.md. It fits my Python and web background and has a clear description, and I want to practice reading an unfamiliar codebase by documenting how its endpoints really behave.

My scout mostly held up, but it fell short twice. Its claim check treated classmates' open PRs as blocking, and my 60-day filter hid the one issue nobody had touched. I fixed the first in the rubric. I would remove or reverse the 60-day filter in my search strategy, because in this repo an old untouched issue is a good sign.

Claim comment: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/47#issuecomment-6779859177

**Toolkit**

- Tool: issue-scout (my search strategy and rubric), run as a scan and as grading on specific issues
- What it produced: a scan of five graded issues, re-grades of #12 and #37 after the scope patch, and an accept verdict on #47 with no claims and no PRs
- Difficulties: the claim check rejected issues over classmates' open PRs, and the 60-day filter hid #47 from the scan
- What changed: edited the claim check in rubric.md, patched the scope check, and I would remove the 60-day filter from search-strategy.md

---

## Understanding the Issue

**Problem Description**

docs/API.md lists the API endpoints with one-line descriptions but has no curl examples, so a new developer cannot see how to get a token or send a request to POST /profiles or POST /reviews.

**Expected Behavior**

The doc should show a working curl example for getting a token, for POST /profiles (multipart form, Bearer header) and for POST /reviews (JSON with profile_id).

**Current Behavior**

grep -c curl docs/API.md prints 0 on main at f89c06f. The doc has 32 lines and no examples anywhere.

**Affected Components**

docs/API.md is the file I change. I read api/routes/auth.py, api/routes/profiles.py, api/routes/reviews.py and api/schemas/user.py to get the fields right. No code changes.

**Toolkit**

- Tool: Claude Code, asked to read the route files and list request fields and auth
- What it produced: A table of the POST /profiles and POST /reviews fields, which are required, and the Bearer header, plus a note that PDF uploads look broken
- Difficulties: Its first answer cut off the profiles part, so I asked again for only that part
- What changed: I used a Markdown resume in the examples and noted the PDF issue instead of documenting it

---

## Reproduction Process

**Environment Setup**

macOS 26.5.1 on a MacBook Pro. This is a docs-only issue, so no language runtime or install is needed: I cloned codepath/pathreview-ai301-fa26-s1 and read docs/API.md at commit f89c06f (main). No challenges came up.

**Steps to Reproduce**

1. git clone https://github.com/codepath/pathreview-ai301-fa26-s1.git, then cd into it and git pull.
2. Run grep -c curl docs/API.md and wc -l docs/API.md.
**Observed result:** grep prints 0 and the file is 32 lines. The doc lists endpoints under Profiles and Reviews with one-line descriptions and has no curl examples anywhere.

**Reproduction Evidence**

- **Commit showing reproduction:** none
- **Screenshots/logs:** grep -c curl docs/API.md printed 0; wc -l printed 32 docs/API.md
- **My findings:** The issue is real today: docs/API.md has zero curl examples, as the issue says. I confirmed it on main at f89c06f.

**Toolkit**

- Tool: repro-check, run on my claim draft and then on my claim and repro report together
- What it produced: an accept on the claim, then a reject on the repro report because the environment check failed, then an accept after my fix
- Difficulties: my local clone was still on an old branch from issue #73, so I recorded commit 4826698, which isn't on upstream main, and I left out the macOS version
- What changed: I switched to main, re-ran the check at f89c06f, added macOS 26.5.1 to the report, and now check which branch I'm on before recording a commit

---

## Solution Approach

**Analysis**

docs/API.md lists the endpoints with one-line descriptions only and has zero curl examples (grep -c curl docs/API.md prints 0 on main at f89c06f). The request details live in api/routes/profiles.py (POST /profiles, multipart form data with optional github_username, portfolio_url, resume_file) and api/routes/reviews.py (POST /reviews, JSON body with required profile_id). Both need an Authorization: Bearer token from POST /auth/login or /auth/register.

**Proposed Solution**

Add curl examples for register, login, POST /profiles and POST /reviews to docs/API.md. Use a Markdown resume in the profile example, because PDF uploads look broken at profiles.py line 63. I am not changing any code, and I am not documenting other endpoints or fixing the PDF issue here.

**Implementation Plan**

1. Edit docs/API.md only.
2. Add curl examples for register, login, POST /profiles and POST /reviews.
3. No tests to change (docs only); run make check and make test-unit.

Deviation: the plan listed only a login example, but I also added a register example, because register returns a token in one call and a new user has to register first.

**Toolkit**

- Tool: plan-check, which I did not run on my plan; I wrote plan.md by hand from the route code
- What it produced: plan.md with Analysis, Proposed Solution and Implementation Plan
- Difficulties: I skipped the plan-check step, so the plan was never graded
- What changed: I added a deviation for the register example and would run plan-check next time

---

## Testing Strategy

Before the fix, on main at f89c06f, grep -c curl docs/API.md printed 0. After the fix, on branch docs/47-curl-examples at commit 2b21bc0, it prints 4, and git diff --stat shows only docs/API.md changed, with 34 lines added. The repo checks from my manifest also pass: make check is clean (ruff, black, mypy) and make test-unit shows 375 passed, 53 xfailed, the same as main. I also ran all four curl commands against a local server (Docker Postgres and Redis, uvicorn on port 8000): register and login each returned a token, POST /profiles returned a profile with an id, and POST /reviews returned a review with status pending.

**Toolkit**

- Tool: make check and make test-unit from my ship manifest
- What it produced: make check clean; make test-unit 375 passed, 53 xfailed, the same as main
- Difficulties: make check and make test-unit cannot prove the curl examples work, so I ran them by hand after opening the PR
- What changed: all four commands worked against a live local server; I will tell the maintainers on the PR

---

## Implementation Notes

Dated log of what I did.

**2026-11-10**

Created branch docs/47-curl-examples from main at f89c06f. Read the route files and schemas, wrote plan.md, and added curl examples for register, login, POST /profiles and POST /reviews to docs/API.md. Committed as 2b21bc0.

**2026-11-10**

Ran make check and make test-unit (375 passed, 53 xfailed), wrote test_evidence.md and pr_draft.md, passed the ship-gate, and opened PR 253 on the original repo. After opening the PR I ran all four curl commands against a local server and each returned what the docs say.

**Toolkit**

- Tool: Claude Code, to read the code and draft the docs edit
- What it produced: A docs/API.md edit of 34 added lines in one commit, 2b21bc0
- Difficulties: Claude added a register example my plan did not list, and my claim comment promised I would run every command myself
- What changed: I recorded the deviation in Solution Approach, and after opening the PR I ran the curl commands against a local server and they worked

---

## Pull Request

**PR Link:** https://github.com/codepath/pathreview-ai301-fa26-s1/pull/253

**PR Description:** Adds curl examples to docs/API.md for register, login, POST /profiles and POST /reviews. Fixes #47. Docs only, 34 lines added. make check clean, make test-unit 375 passed, 53 xfailed. The curl commands were written from the route code; I ran them against a local server after opening this PR and they worked.

**Maintainer Feedback:**

- 2026-11-10: none yet

**Status:** Awaiting review

**Toolkit**

- Tool: ship-gate, run by hand on my branch before opening the PR
- What it produced: ship-gate: PASS, then PR 253 opened on the original repo
- Difficulties: Its notes pointed out that my claim promised to run every command while my PR said I had not; I ran them afterward and they worked
- What changed: I kept the PR honest about it; I would run the commands before opening next time

---

## Learnings and Reflections

**Technical Skills Gained**

I learned to read FastAPI route files and Pydantic schemas to find the exact request fields and auth for an endpoint, how multipart form data differs from JSON in curl, and how to run a repo's make targets before opening a PR.

**Challenges Overcome**

My first two issue picks were already taken by classmates, so I re-ran my scout and found an untouched one that my own 60-day filter had hidden. My local clone also sat on an old branch, which made repro-check reject my commit hash until I switched to main.

**What I'd Do Differently Next Time**

I would run the curl commands against a live server before opening the PR, because my claim promised I would. I would also run plan-check, which I skipped, and fix my scout's 60-day filter.

---

## Resources Used

docs/CONTRIBUTING.md for the checks and the 48-hour reply rule, and api/routes and api/schemas in the Path Review repo for the real request fields.

- docs/CONTRIBUTING.md in the Path Review repo (checks and the 48-hour reply rule)
- Issue 47 thread in codepath/pathreview-ai301-fa26-s1
