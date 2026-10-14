# Procedure: how this tool grades a PR package

## Read order

1. Live mode only: read scope.md, then voice-guide.md. Eval mode skips both.
2. Read the issue and the repo facts first (live: the issue thread, .github/PULL_REQUEST_TEMPLATE.md, docs/CONTRIBUTING.md; eval: the bundle's issue and repo-facts blocks). Note the template sections and every stated ask (title format, branch naming, disclosure, test commands, xfail markers).
3. Read the plan next (live: plan.md; eval: the bundle's plan). List the files and changes it names, its test plan, and everything under ## Deviations. The plan comes before the diff so the diff can be judged against it.
4. Read the diff (live: git diff main...HEAD; eval: the bundle's diff). List every changed file and summarize each hunk in one line.
5. Read the test evidence (live: test_evidence.md; eval: the bundle's evidence). Note each command run and its output.
6. Read the PR title and description last (live: pr_draft.md; eval: the bundle's description). Note each claim, each Changes bullet, each ticked Testing box, and the Notes for Reviewers text.

## Evidence gathering

- Diff matches plan: pair each changed file and hunk with a plan item or a deviation. Record unpaired hunks, and plan items with no hunk.
- Description matches diff: pair each Summary claim and Changes bullet with a hunk. Record claims with no hunk, and meaningful hunks with no mention.
- Repro before and after: find the plan's repro steps in the test evidence. Record whether a before run and an after run both exist, and whether their outputs differ the way the fix claims.
- Repo checks run: for make test-unit, make test-integration, make lint, make typecheck, record whether pasted output exists and its result. Compare any claimed result against the output.
- Testing claims honest: for each ticked box, record the evidence line that backs it, or none.
- No debris: scan the diff's added lines for debug prints, commented-out code, leftover TODOs, and stray files.
- No unrelated changes: for each hunk, record whether it serves the issue's fix or its tests.
- Template filled: compare the description's sections to the template's. Record empty or placeholder sections and whether the issue number follows Closes #.
- AI disclosure: quote what Notes for Reviewers says about AI use and about departures from the plan.
- Repo asks followed: list each ask from the repo facts and record whether the title, branch name, and diff meet it.
- Description clarity: record whether the Summary states what changed and why.

## Check execution

1. Run the checks in the rubric's table order, one at a time, using only the evidence gathered above.
2. Grade each check against its pass condition only. Do not grade on length or polish.
3. Name the deciding fact or quote for every grade, including passes.
4. If the evidence for a check is absent from the package, grade it unclear. Do not look outside the package in eval mode.
5. A disclosed shortfall counts as a pass where the check's pass condition allows disclosure.
6. A check may be graded without re-reading the whole package once its evidence is gathered.
7. Note any step this procedure does not cover in the summary as a procedure gap.

## Verdict assembly

1. Apply the rubric's verdict rule: accept if every required check passes, reject if any required check fails or is unclear.
2. Preferred checks never change the verdict. List them in the summary only.
3. Quote the first failing required check in rubric order as the deciding check. If an unclear check comes before any fail, quote that one.
4. Live mode: add voice-guide notes to the summary, never to the verdict.
5. Print the per-check summary, then end with the JSON block: one entry per check in rubric order, then the verdict, with nothing after it.
