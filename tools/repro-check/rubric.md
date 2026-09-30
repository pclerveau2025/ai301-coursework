# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| claim-specific | Claim comment vs issue text | Claim names the issue's concrete files, keys, or behavior; could not be pasted onto another issue | required |
| claim-promise | Claim comment vs repro report | States a concrete next step in the investigation; never promises a fix, PR, or date. Saying it already reproduced is fine when the package's repro report shows it; fails only if the claim asserts a repro that no report backs | required |
| repro-env | Repro report | Records OS, runtime/tool versions, commit or branch, and setup taken from the repo's own docs | required (n/a on claim-only draft) |
| repro-steps | Repro report | Numbered steps a stranger could re-run from a clean clone | required (n/a on claim-only draft) |
| repro-target | Observed behavior vs issue text | Behavior shown is the one the issue describes, not an adjacent bug | required (n/a on claim-only draft) |
| repro-evidence | Repro report | Observed output (error, log, or output excerpt) is shown, not just asserted | required (n/a on claim-only draft) |
| honest-outcome | Repro report | Outcome matches the evidence; an evidenced cannot-reproduce passes; a confident claim with no evidence or on the wrong target fails | required (n/a on claim-only draft) |
| conventions-disclosure | The package's own repo-facts block (live: that repo's CONTRIBUTING) vs every comment | Only if that repo's stated policy requires AI-assistance disclosure, every comment must disclose it. No stated requirement means pass. Never apply another repo's policy | required |
| conventions-own-words | All comments | No piggybacking ("same as above", "+1"); proof is in the author's own words | required |
| voice | voice-guide.md vs all comments | Follows the voice guide's rules and never-post list | preferred |

## Verdict rule

Accept if every applicable required check passes. Checks marked n/a on a claim-only draft are reported as not yet applicable and do not affect the verdict. Preferred checks are reported but never change the verdict. Unclear counts as fail.
