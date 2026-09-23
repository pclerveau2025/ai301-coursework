## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| Maintainer is alive | Date of most recent maintainer comment or merged PR on any issue/PR | A maintainer commented or merged within 90 days | required |
| Repo is in use | Date of most recent commit to the default branch | A commit was pushed within 180 days | required |
| Scope fits a newcomer | Issue body, labels, and comments | Passes unless there is explicit evidence the work is large or open-ended: a redesign, refactor, or migration; changes across multiple subsystems; an "epic"/tracking issue; or a maintainer saying the approach still needs design or discussion. Missing size estimates do not count as unclear. | required |
| Not already claimed | Assignees field and comments: look for "I'll take this", "assigned", or an open linked PR | No assignee, no open linked PR, and no comment claiming the issue within the last 30 days | required |
| Issue is open and unresolved | Issue state and whether a merged PR references it | Issue is open and no merged PR closes it | required |
| Maintainer engagement on issue | Comments from a maintainer directly on this issue | At least one maintainer comment on the issue, or the issue was opened by a maintainer | preferred |

## Verdict rule

Accept if every required check passes. Preferred checks never change the verdict; they rank accepted issues above others with equal required scores. Unclear on any required check counts as fail.
