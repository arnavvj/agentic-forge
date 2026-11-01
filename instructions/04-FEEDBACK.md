# FEEDBACK: Process Manual-Test Results and Requested Changes

## Objective

Turn the user's manual-test notes, observations, or requested changes into clear, traceable work in the feedback log of `docs/05-TASKS.md`. Preserve the user's intent. Implement a fix only after explicit approval, or when the user's instruction clearly asks you to make it.

## Procedure (`FEEDBACK: ...`)

1. Read `CLAUDE.md`, the related task, and the affected design and decision records.
2. Clarify the observed behavior: user action, expected behavior, actual behavior, and reproducibility. Ask if these are unclear.
3. Inspect logs, code, and tests where available. Do not assume the user's suggested cause is correct. Distinguish a confirmed cause from a hypothesis.
4. Classify it: bug, missing requirement, usability, performance / reliability, design change, or new scope.
5. Propose the smallest correction that addresses the underlying issue, with the tests to add or update.
6. Add an `FB-XXX` row to the feedback log with status `Proposed`.
7. If the correction is a material design or scope change, also record a `Proposed` decision in `docs/06-DECISIONS.md`.
8. Present the analysis and the proposed correction, then stop. Reporting a problem is not approval of a particular solution.

## Implementing a fix (`APPROVE FIX FB-XXX`, or an explicit instruction to fix)

1. Record the approval in the feedback log with a short summary of the user's message.
2. Confirm the scope you understood. Implement only the approved fix.
3. Add regression coverage where practical. Run the relevant checks and record the actual results.
4. Update "Current state". The feedback item stays `Approved` until the user accepts the fix.
5. Leave the change uncommitted for `REVIEW FB-XXX` and `ACCEPT FB-XXX`, as for a task. On acceptance, it becomes `Fixed` and is committed.
6. Report the change, the verification, any limitations, and the manual test the user should repeat.

If the requested fix conflicts with the approved design or creates a material security or data risk, stop and surface the conflict before changing anything.
