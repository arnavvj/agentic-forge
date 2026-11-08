# IMPLEMENT: Execute an Approved Task

Implement one approved task per the approved design and plan. Deliver a focused, tested change, leave it uncommitted for review, and report exactly what was done.

## Before coding

1. Read `docs/04` ("Now", the task, relevant decisions) and the task's requirements and design sections.
2. The task must be `Approved` with an approval record; `Proposed` is not approved. Dependencies must be `Done` or earlier in the same approved batch.
3. If `docs/00` to `docs/03` changed since the plan's design baseline and the change affects this task, stop and recommend `REPLAN`.
4. Check the working tree. Report unrelated uncommitted changes and ask before proceeding.
5. Inspect the current code and tests for the affected components.

If the task is unapproved, ambiguous, or conflicts with the approved design, stop and say what is needed.

## Procedure

1. Set the task `In progress`; update "Now".
2. Restate scope and acceptance criteria briefly.
3. Make the smallest change that satisfies them, following repository conventions, the approved architecture, and the repository layout (`docs/02` section 3). Add no folder the layout lacks without approval.
4. Add or update tests for changed behavior, including important error and permission paths, at the profile's depth. For agent behavior, add or run the relevant eval cases.
5. Run the applicable formatters, linters, type checks, and tests.
6. Inspect the full diff for unintended changes, secrets, debug code, and generated files.
7. Update the project README or other application docs the change affects.
8. `docs/04`: status `Review needed`, checks run, known limitations, "Now".
9. Record material decisions or approved deviations in `docs/04` section 4.
10. Do not commit.

## Special handling

- A material design change is needed: stop and propose it.
- A dependency or external service is unavailable: mock only if the design and profile allow it; label the mock in code and in the report.
- A test cannot run: report it as not run, never as passed.
- Never weaken security, authorization, validation, or data isolation to make a test or demo pass.
- Do not implement adjacent tasks for convenience; propose them.

## Batch mode

For an explicitly approved batch (`IMPLEMENT M1`, `IMPLEMENT TASK-001..TASK-003`):

- Implement tasks in dependency order, each per the procedure above.
- Stop at the first failing check, blocker, required design change, or unapproved task. Report what is done and what remains.
- Leave the combined change uncommitted; it is reviewed and accepted as one batch.

## Report and stop

Report: task ID(s) and outcome; main changes and files; acceptance criteria met or unmet; exact tests and checks run with outcomes; manual tests for the user; limitations and follow-ups. End with the next step (normally `REVIEW TASK-XXX`), then stop.
