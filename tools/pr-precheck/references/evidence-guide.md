# Evidence guide: where evidence lives in a PR package

## Plan fidelity

Practice package: the plan section of the bundle (scope, changes, test plan, any Deviations), the diff section, and the PR description's Summary and Changes bullets.
Own PR: plan.md including ## Deviations, the output of git diff main...HEAD, and the Summary and Changes sections of pr_draft.md.
Good looks like: every changed file and hunk maps to a plan item or a recorded deviation. Every plan item has a hunk or a disclosed omission. Every description claim has a matching hunk. Silent extras or silent gaps are drift.

## Test evidence

Practice package: the test evidence block (command output, before and after repro) and the ticked boxes in the description's Testing section.
Own PR: test_evidence.md (make test-unit, make test-integration, make lint, make typecheck, repro before on main and after on the branch) and the Testing section of pr_draft.md.
Good looks like: real pasted output for all four checks and for the plan's repro, before and after, with output that differs the way the fix claims. A failing check reported with its reason counts. "no tests ran" for integration is expected. Every ticked box has output behind it. The CI box stays unticked.

## Diff quality

Practice package: the diff section of the bundle, added lines and file list.
Own PR: git diff main...HEAD and git diff main...HEAD --stat.
Good looks like: only files and hunks that serve the issue's fix or its tests. No debug prints, commented-out code, leftover TODOs, stray files, or reformatting of unrelated code. Seeded xfail markers for the issue are removed.

## Standards and comms

Practice package: the repo-facts block (PR template, CONTRIBUTING rules, AI policy) read against the title and description.
Own PR: .github/PULL_REQUEST_TEMPLATE.md and docs/CONTRIBUTING.md read against pr_draft.md, plus the branch name.
Good looks like: every template section filled with real content, the issue named after Closes #, the title and branch name following the repo format (type prefix, issue number, short description), and Notes for Reviewers stating specifically how AI was used and any departures from the plan or things left out.
