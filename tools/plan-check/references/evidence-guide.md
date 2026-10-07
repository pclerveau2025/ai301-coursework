# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

- Where it lives: the cause line at the top of `## Candidate plan` (often "Cause:"), read against the numbered steps, control runs, and debug/timing output in `## Repro evidence`. Maintainer confirmations in `## Thread highlights` count as supporting evidence. Live: plan.md's diagnosis vs. the student's posted repro comment on the issue.
- What good looks like: the stated cause explains every repro step, and no control run shows the bug with that component removed or shows that component working in the same build. In calib-01, "commits view model not refreshed after push" matches step 4 (re-entering fixes the color). A cause the control rules out is wrong, however confident it sounds.

## Scope

- Where it lives: the change/approach section of `## Candidate plan`, including "In:" / "Out:" lines and any "also" or follow-up items. Live: plan.md's scope section and files-to-touch list.
- What good looks like: one bounded change aimed at the reproduced behavior, plus an explicit out-of-scope line (calib-01: "Out: any change to how push status is computed"). Fails when the fix is wrapped in refactors, migrations, upgrades, new options, or rewrites the issue never asked for. Deferring work with a reason is good scoping, not a gap.

## Executability

- Where it lives: file paths, functions, and callbacks named in `## Candidate plan` (calib-01: the push completion callback in `pkg/gui/controllers/sync_controller.go`). Live: plan.md's files and approach sections.
- What good looks like: a stranger could open the named file and make the change without asking the author which layer or which option. Fails on "somewhere", "X or Y, whichever is easier", or "investigate first" with no decision.

## Test plan

- Where it lives: the "Test:" part of `## Candidate plan`, mapped onto the repro evidence step that showed the bug. Live: plan.md's test plan vs. the unit 2 repro steps.
- What good looks like: the repro re-run with the exact post-fix observable (calib-01: "at step 3 the color must flip without leaving the view"), or a specific output, value, or exit code. Fails on "run the test suite", "should feel fast", or "nothing breaks" with no observable for the fix itself.

## Honesty

- Where it lives: risks/unknowns lines and deferral notes in `## Candidate plan`; live, also plan.md's `## Deviations` section after the build.
- What good looks like: unknowns are named as unknowns, assumptions say whether they were checked, and deferrals give a reason. A mid-build change is recorded under Deviations, not left only in the diff.

## Comms

- Where it lives: `## Candidate plan comment`, read against `## Thread highlights` (maintainer/owner comments, linked PRs, patched builds, test requests) and the contribution-policy line in `## Repo facts`. Live: the draft comment.md vs. the issue thread and the repo's README/CONTRIBUTING.
- What good looks like: if a maintainer gave direction, the comment acknowledges it and the plan follows it or explains why not. If the stated policy requires AI-use disclosure, the comment discloses it (every package is AI-assisted). calib-01's comment references the CONTRIBUTING review-bandwidth note; that repo has no disclosure requirement, so none is needed.
