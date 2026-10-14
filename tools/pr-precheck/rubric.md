# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Diff matches plan | The diff's changed files and hunks, read against the plan's scope and its ## Deviations section | Every changed file and hunk is covered by the plan or a recorded deviation. Anything the plan promised that the diff lacks is disclosed in the description or deviations. Fails if the diff silently does more or less than the plan. | required |
| Description matches diff | The description's Summary and Changes bullets, read against the diff | Every claim and Changes bullet is visible in the diff, and no meaningful diff change is missing from the description. Fails if the description claims something the diff contradicts or omits. | required |
| Repro before and after | The before and after behavior of the plan's repro, from the plan's repro evidence, the description, and the test evidence together | Both the before behavior and the after behavior appear with observable output (a quoted error, exit code, or result), and they differ as the fix claims. The before may come from the plan's repro evidence or the description. Fails if either side is missing, invented, or proves nothing. | required |
| Repo checks run | Test results anywhere in the test evidence or description, read against the plan's test plan and any checks the repo facts name | Every check the plan or repo facts name has a result: pasted output or an explicit statement such as 'go test ./... passes'. A failure reported honestly with its reason passes. If nothing is named, any shown test or repro result passes. Fails if a named check has no result at all, if a claimed pass is contradicted by shown output, or if a shown failure is not disclosed. | required |
| Testing claims honest | The ticked boxes in the description's Testing section, read against the test evidence | Every ticked box is backed by evidence in the package. The CI box unticked is fine. Fails if a box is ticked without evidence. | required |
| No debris | The diff's added lines | No debug prints, commented-out code, leftover TODOs, or stray files among the added lines. | required |
| No unrelated changes | The diff's hunks, read against the issue and the plan | Every hunk serves the issue's fix or its tests. Fails on cleanups, reformatting, or edits to unrelated files. | required |
| Template filled | The repo facts' PR template, if the package states one, read against the description | If a template is stated, every section is present with real content and the issue is named. If no template is stated, passes when the description names the issue and says what changed and why. Placeholder text in a stated section fails. | required |
| AI disclosure | The repo facts' AI policy or template ask, if stated, read against the description | If the repo facts require AI disclosure, the description states specifically how AI was used. Fails if required and missing or generic. If no disclosure is required, passes. | required |
| Repo asks followed | The repo facts and docs/CONTRIBUTING.md, read against the title, branch name, and diff | Every stated ask is met (title format, branch prefix with issue number, removing the seeded xfail marker, and so on). Fails if the package ignores a stated ask. | required |
| Description clarity | The description's Summary | A reviewer can tell what changed and why in a few sentences without opening the diff. | preferred |

## Verdict rule

Accept if every required check passes. Reject if any required check fails or is unclear. Preferred checks never change the verdict; report them in the summary only. A shortfall that the description or plan.md honestly discloses does not fail a check whose pass condition allows disclosure. A shortfall that only shows up in the diff does.
