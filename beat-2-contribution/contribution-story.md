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
**Pull Request:** pending

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

I wrote upstream rules for claims, questions, and pings into my voice guide and installed a hook that checks every comment I post through Claude Code. The first settings write failed silently, so the hook check said "not found"; I rewrote it with a short Python command and the wiring test then blocked the body-less command as it should. My first claim draft included a promise I never asked for, and I decided to keep it only because I will really test my own work, so I now read drafts for added promises before posting.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

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

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

macOS 26.5.1 on a MacBook Pro. This is a docs-only issue, so no language runtime or install is needed: I cloned codepath/pathreview-ai301-fa26-s1 and read docs/API.md at commit f89c06f (main). No challenges came up.

**Steps to Reproduce**

1. 1. git clone https://github.com/codepath/pathreview-ai301-fa26-s1.git, then cd into it and git pull.
2. 2. Run grep -c curl docs/API.md and wc -l docs/API.md.
3. Observed: grep prints 0 and the file is 32 lines. The doc lists endpoints under Profiles and Reviews with one-line descriptions and has no curl examples anywhere.

**Reproduction Evidence**

- **Commit showing reproduction:** none
- **Screenshots/logs:** grep -c curl docs/API.md printed 0; wc -l printed 32 docs/API.md
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
