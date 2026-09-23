# Unit 1 — Issue Selection

## Selected issue

### Issue link
https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73

### Verdict output

```
[
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/53",
    "checks": [
      {"name": "Maintainer is alive", "grade": "pass", "evidence": "Aburke225 (COLLABORATOR) commented on #52 and #43 on 2026-09-16, 6 days ago"},
      {"name": "Repo is in use", "grade": "pass", "evidence": "Latest main commit 2026-09-16 by Aburke225; repo not archived"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Single regex bug in pii_scrubber.py with repro and four named failing tests; labeled good first issue"},
      {"name": "Not already claimed", "grade": "pass", "evidence": "No assignees, no comments, no linked PR; only a commit reference from a student fork (Evin009/ai301-coursework)"},
      {"name": "Issue is open and unresolved", "grade": "pass", "evidence": "state: open; no merged PR references it"},
      {"name": "Maintainer engagement on issue", "grade": "pass", "evidence": "Opened by Aburke225 (COLLABORATOR)"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/60",
    "checks": [
      {"name": "Maintainer is alive", "grade": "pass", "evidence": "Aburke225 (COLLABORATOR) commented on #52 and #43 on 2026-09-16, 6 days ago"},
      {"name": "Repo is in use", "grade": "pass", "evidence": "Latest main commit 2026-09-16 by Aburke225; repo not archived"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "One-line None-handling bug in faithfulness_checker.py with repro and a named failing test"},
      {"name": "Not already claimed", "grade": "pass", "evidence": "No assignees; open PR #74 by classmate nianiiier (NONE) closes #60, but the Path Review house rule says classmates' claims do not block"},
      {"name": "Issue is open and unresolved", "grade": "pass", "evidence": "state: open; PR #74 is open and unmerged"},
      {"name": "Maintainer engagement on issue", "grade": "pass", "evidence": "Opened by Aburke225 (COLLABORATOR)"}
    ],
    "verdict": "accept"
  },
  {
    "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/73",
    "checks": [
      {"name": "Maintainer is alive", "grade": "pass", "evidence": "Aburke225 (COLLABORATOR) commented on #52 and #43 on 2026-09-16, 6 days ago"},
      {"name": "Repo is in use", "grade": "pass", "evidence": "Latest main commit 2026-09-16 by Aburke225; repo not archived"},
      {"name": "Scope fits a newcomer", "grade": "pass", "evidence": "Make README.md and .env.example agree; two named files; 'Estimated effort: 1–2 hours'"},
      {"name": "Not already claimed", "grade": "pass", "evidence": "No assignees, no comments, no linked or cross-referenced PRs"},
      {"name": "Issue is open and unresolved", "grade": "pass", "evidence": "state: open; no PR references it"},
      {"name": "Maintainer engagement on issue", "grade": "pass", "evidence": "Opened by Aburke225 (COLLABORATOR)"}
    ],
    "verdict": "accept"
  }
]
```

## Eval iterations

### Run history
1. `--limit 3` (first attempt): 0/0 — all 3 items errored ("claude exited 1") because Claude Code was not logged in.
2. `--limit 3` (after logging in): 2/3.
3. Full run, original rubric: 15/20 (below the bar). All 5 misses were gold-accept issues (issue-01, 04, 11, 14, 19) rejected on "Scope fits a newcomer". clear-accept category was 3/8.
4. `--only issue-01,issue-04,issue-11,issue-14,issue-19` after rewriting the scope check: 3/5 (issue-04, 11, 14 fixed).
5. Final full run with `--save-run eval-run.txt`: 18/20 (bar: 18/20: PASS). Categories: claimed 4/4, clear-accept 6/8, dead-repo 3/3, policy 1/1, scope 4/4.

### Issue analysis
issue-04. Gold label: accept. My original rubric decided reject (failed: "Scope fits a newcomer"); my final rubric decided accept.
The original scope check required "estimated change is under 200 lines across fewer than 5 files." The issue body gave no line or file counts, so the grader could not confirm the threshold, and my verdict rule says "Unclear on any required check counts as fail." The issue was a bounded fix, but the missing estimate alone sank it. After I rewrote the check to fail only on explicit evidence of large or open-ended work, and to state that missing size estimates do not count as unclear, the grader accepted issue-04, matching the gold label.

### Check rationale
"| Scope fits a newcomer | Issue body, labels, and comments | Passes unless there is explicit evidence the work is large or open-ended: a redesign, refactor, or migration; changes across multiple subsystems; an "epic"/tracking issue; or a maintainer saying the approach still needs design or discussion. Missing size estimates do not count as unclear. | required |"
The first version asked for line and file counts that issue bodies almost never contain, and combined with "Unclear on any required check counts as fail" it rejected 5 good issues. The new form uses evidence that actually appears in issues (labels, wording like refactor/migration/epic, maintainer comments) and only fails on positive signs of large scope, so an ordinary small bug is not rejected just for lacking a size estimate.

### Trade-offs
The check now defaults to pass, so it gives up catching a large issue that does not say it is large. I checked that it did not loosen too far: in the final full run the scope category stayed at 4/4, the same as before the change. It also still misses issue-01 and issue-19 (gold accept, rejected on "Scope fits a newcomer"); I accept those as arguable scope calls rather than loosen the check further and risk the scope category.

## Selection rationale

1. I picked #73 because it is a docs/config fix (README.md and .env.example) with an estimated effort of 1–2 hours, which fits my time this week and is a good first step into the codebase.
2. The verdict correctly found the issue open, unclaimed, with no linked PR, and opened by an active maintainer. What I weighed that the rubric could not: whether I can confirm which API key the code actually reads, since the fix depends on knowing the correct one, not just making two files match.
3. The main difficulty is timing: it is a good first issue with no comments yet, so a classmate could claim it first. I will follow the house rules in scope.md and Unit 2's guidance when I write the claim comment.
