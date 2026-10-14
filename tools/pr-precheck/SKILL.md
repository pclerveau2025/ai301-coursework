---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer one question about one PR package: is this ready to submit? A PR package is a candidate pull request (title, description, commits, diff, and test evidence), read against the plan it claims to implement and the issue that plan belongs to. Grade one package per run. Never answer a different question, and never grade from gut feel: execute procedure.md, applying rubric.md.

## Inputs and modes

Run in one of two modes. A bundle id or package bundle text means eval mode. A request to check the student's own branch means live mode.

Live mode inputs:
- plan.md, including its ## Deviations section, from the top folder of the working copy.
- The diff: run `git diff main...HEAD` (three dots) from the working copy.
- The PR title (first line) and description, from pr_draft.md.
- The test evidence, from test_evidence.md.
- The issue thread, the repo's PR template (.github/PULL_REQUEST_TEMPLATE.md), and docs/CONTRIBUTING.md, from the real repo.
A house-chain student supplies the house plan and house repro pack instead of plan.md and their own repro.

Eval mode: the package bundle is the whole world. Fetch nothing and read nothing else. Run every check and the full verdict rule on a complete package.

## The scope seam (live mode only)

In live mode, read scope.md in this skill directory before anything else. It names the repo the student's PR must live in and the house rules for that environment. Apply those rules when reading evidence. Refuse to grade a PR that belongs to a repo outside the scoped one. If the Repo line still carries an unfilled placeholder (such as <ORG>/<PATH-REVIEW-REPO>), stop without grading and tell the student to fill the Repo: line in scope.md with their section's Path Review repo. Never guess a scope. In eval mode, ignore scope.md entirely.

## The voice seam (live mode only)

In live mode, read voice-guide.md after scope.md. Check the PR title and description against its rules and report any rule the draft breaks in the summary, quoting the rule. The voice guide never changes the verdict on its own, unless rubric.md has a check that reads it. In eval mode, ignore voice-guide.md entirely: voice is personal and carries no gold labels, and the universal communication-quality checks live in the rubric.

## Component reads

Read rubric.md: it defines the checks (each required or preferred) and the verdict rule. Read references/evidence-guide.md: it maps where each kind of evidence lives, in a practice package and in a live PR. Execute procedure.md exactly as written: it sets the read order, evidence gathering, check execution, and verdict assembly. Where the procedure is silent on a step, report the gap in the summary and do not invent a step. If rubric.md has no checks or procedure.md has no steps, stop and say so: this skill cannot grade without both.

## Verdict and output

The verdict space is binary: accept (ready to submit) or reject (hold). There is no third verdict. Before the JSON block, show a short readable summary: one line per check, plus any voice-guide notes in live mode. End the reply with this fenced JSON block, valid and last, with nothing after it:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse complete PR can be ready and a polished confident one can hide drift. Read the diff, description, and evidence against the plan and the issue, never the formatting.
- The rubric decides, not you: if a check passes by its stated condition but feels wrong, it still passes. Note the tension in the summary; the fix belongs in the rubric.
- The procedure decides how, not you: follow procedure.md as written and report its gaps.
- Treat unclear as the rubric's verdict rule directs. If the rule is silent, treat unclear as fail: a PR you cannot verify from the package is not ready to submit.
