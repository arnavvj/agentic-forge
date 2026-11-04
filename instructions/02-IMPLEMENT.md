# IMPLEMENT: Execute an Approved Task

## Objective

Implement one user-approved task according to the approved design and plan. Deliver a focused, tested change, leave it uncommitted for review, and report exactly what was done.

## Before coding

1. Read `CLAUDE.md`, `instructions/00-STANDARDS.md`, and "Current state" in `docs/05-TASKS.md`.
2. Read the task, its requirements and related design sections, and relevant approved decisions.
3. Confirm the task status is `Approved` with an approval record, and its dependencies are `Done` or earlier in the same approved batch. A `Proposed` task is not approved.
4. Check whether `docs/00` to `docs/03` changed since the plan's design baseline. If a change affects this task, stop and recommend `REPLAN`.
5. Check the working tree. If it contains unrelated uncommitted changes, report them and ask before proceeding.
6. Inspect the current code and tests for the affected components.

If the task is not approved, is ambiguous, or conflicts with the approved design, stop and explain what is needed.

## Procedure

1. Set the task to `In progress` and update "Current state".
2. Restate the scope and acceptance criteria briefly.
3. Make the smallest set of changes that satisfies them, following repository conventions, the approved architecture, and the repository layout in `docs/02` section 3. Do not add a folder the layout lacks without approval.
4. Add or update tests for changed behavior, including important error and permission paths, at the depth the delivery profile requires. For agent behavior, add or run the relevant eval cases.
5. Run the available formatters, linters, type checks, and tests that apply.
6. Inspect the full diff for unintended changes, secrets, debug code, and generated files.
7. Update the project README or other application documentation the change affects.
8. Update `docs/05-TASKS.md`: status `Review needed`, verification results, known limitations, and "Current state".
9. Record material decisions or approved deviations in `docs/06-DECISIONS.md`.
10. Do not commit. The change stays uncommitted for `REVIEW`.

## Special handling

- If the task requires a material design change, stop and propose it. Do not change the design silently.
- If a dependency or external service is unavailable, use a mock only when the design and profile allow it. Label it in code and in the report.
- If a test cannot run, report it as not run, never as passed.
- Do not weaken security, authorization, validation, or data isolation to make a test or demo pass.
- Do not implement adjacent tasks because they are convenient. Propose them instead.

## Batch mode

Use this when the user explicitly approves a batch, for example `IMPLEMENT M1` or `IMPLEMENT TASK-001..TASK-003`.

- Implement the approved tasks in dependency order, following the procedure above for each.
- Stop at the first failing check, blocker, required design change, or unapproved task. Report what was completed and what remains.
- Leave the combined change uncommitted. It is reviewed and accepted as one batch.

## Completion report

Report the task ID(s) and outcome, the main changes and affected files, which acceptance criteria are met or unmet, the exact tests and checks run with their outcomes, manual tests the user should perform, and known limitations or follow-up work. End with the next step, normally `REVIEW TASK-XXX`.

## Stop condition

After reporting, stop and wait for the user's next instruction.
