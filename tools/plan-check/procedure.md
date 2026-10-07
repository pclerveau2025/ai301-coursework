# Procedure: how this skill grades a plan package

## Read order

1. Read the repo-facts block (live: the repo's README, CONTRIBUTING, and issue/PR templates). Note any AI-use disclosure requirement and any other stated contribution rule, word for word.
2. Read the issue. Note the reported symptom and the expected behavior in one line each.
3. Read the thread highlights (live: every comment on the issue). Note every comment by a maintainer, owner, or collaborator that isolates a culprit, requests an approach or testing, posts a patched build, or links a PR. If there are none, write "no maintainer direction".
4. Read the repro evidence block (live: the student's posted repro comment, or the house repro pack as quoted in the drafts). List each step and each control run, and for each write what it shows is and is not responsible for the bug.
5. Only now read the candidate plan, then the candidate plan comment.

Why this order: the plan must be judged against what the evidence and thread already establish, so those facts are written down before the plan's own framing can anchor you.

## Evidence gathering

1. grounded-cause: copy the plan's stated cause in one line. Next to it, list every repro step or control from read-order step 4 that bears on that component.
2. bounded-scope: list every distinct change the plan commits to (including "also", "while I'm in there", and follow-up items stated as part of this work). Separately list what the plan explicitly defers or marks out of scope.
3. executable: copy every file, function, or code site the plan names, and copy the sentence that states the approach.
4. decisive-test: copy the test plan, and copy the repro step that showed the bug.
5. honest-unknowns: copy the plan's risks/unknowns lines and any deferral reasons.
6. thread-direction: take the notes from read-order step 3, then copy any sentence in the plan comment that refers to the thread, a maintainer, a PR, or a patched build.
7. policy-compliance: take the policy notes from read-order step 1, then copy any sentence in the plan comment that discloses AI use.

If a family's source is genuinely missing from the package (for example no thread comments), record "absent" rather than searching elsewhere. In eval mode, never fetch anything outside the bundle.

## Check execution

1. Run the checks in rubric order: grounded-cause, bounded-scope, executable, decisive-test, honest-unknowns, thread-direction, policy-compliance.
2. For each check, apply only that check's pass condition to the evidence gathered for it. Grade `pass`, `fail`, or `unclear`, and write the one fact or quote that decided it.
3. grounded-cause: if any listed step or control shows the bug with the blamed component excluded, or shows that component working correctly, grade `fail` and quote that step. Do not let a confident write-up or a thread suggestion override the evidence.
4. bounded-scope: grade `fail` if any listed change is not needed to fix the reproduced behavior, even when the core fix is right. Items on the deferred/out-of-scope list never cause a fail.
5. executable and decisive-test: judge the content, not the length. A three-line plan with a named file and a re-run repro step with its expected result passes both.
6. thread-direction and policy-compliance: if the evidence was recorded as "no maintainer direction" or "no disclosure requirement", grade `pass`.
7. Use `unclear` only when the package truly does not contain enough to decide. Grade every check even after one has failed; do not stop early.

## Verdict assembly

1. If any `required` check is `fail` or `unclear`, the verdict is `reject`. Otherwise it is `accept`.
2. Ignore `honest-unknowns` for the verdict; report its grade only.
3. In the summary, name the first failing required check in rubric order and quote its deciding evidence; if all pass, say so in one line.
4. Emit the JSON block exactly as SKILL.md specifies, with one entry per check, and put nothing after it.
