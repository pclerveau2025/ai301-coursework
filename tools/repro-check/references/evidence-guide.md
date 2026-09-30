# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

- Where it lives: Eval bundle: the environment section of the repro report, checked against the issue context and the repo-facts block (supported versions, setup docs). Live: the draft repro comment, checked against the issue thread and the repo's README and setup docs.
- What good looks like: The report names the OS, runtime and tool versions, and the commit or branch tested. Setup follows the repo's own docs. The versions match what the issue targets, or the report calls out the difference. A claim-only draft has no environment yet, so this is n/a.

## Steps

- Where it lives: Eval bundle: the steps section of the repro report. Live: the steps in the draft repro comment.
- What good looks like: Numbered steps go from a stated starting state (for example, a fresh clone at a named commit) to the trigger, with exact commands and file edits. A stranger could run them without guessing. Missing steps, "set it up normally", or skipped config changes fail.

## Behavior shown

- Where it lives: Eval bundle: the observed-behavior section of the repro report (output excerpts, logs, error text, screenshots), compared with the issue context's described behavior. Live: the output pasted in the draft, compared with the issue body.
- What good looks like: The artifact shows the same symptom the issue describes (same component, same trigger, same failure), not a different error hit along the way. For example, if the issue is a mismatch between the README and .env.example, the output shows what happens when you follow the README's key name, not an unrelated install error. Text that describes the output without showing it fails.

## Honesty

- Where it lives: The report's stated outcome ("reproduced" or "could not reproduce") read against the evidence in the Environment, Steps, and Behavior shown sections of the same report.
- What good looks like: The outcome claims no more than the evidence shows. An evidenced cannot-reproduce (environment, steps, and actual output all shown) passes. The report fails if it claims "reproduced" with no output, reproduces an adjacent bug and calls it the issue, or states a root cause as fact without evidence.

## Comms

- Where it lives: Eval bundle: the claim comment and repro comment, checked against the issue context and the repo-facts block (contribution policy, comment templates, AI-disclosure rules). Live: the draft comments, checked against the issue thread, the repo's CONTRIBUTING and README, and the skill's scope.md.
- What good looks like: The claim names the issue's specifics and promises only the investigation and a report, with no fix and no date. Every comment is in the author's own words, never "same as above" or "+1". If the repo policy requires disclosing AI assistance, every comment discloses it; one missing disclosure fails the check. Boilerplate that could go on any issue fails.
