# IMPLEMENT: Execute an Approved Task

## Objective

Implement one user-approved task according to the approved design and plan. Deliver a focused, tested change and report exactly what was done.

## Before coding

1. Read `CLAUDE.md`.
2. Read the relevant approved task in `docs/05-TASKS.md`.
3. Read related requirements and design sections in the project and design documents.
4. Read relevant approved decisions in `docs/06-DECISIONS.md`.
5. Inspect current code and tests for affected components.
6. Confirm the task is explicitly approved and dependencies are satisfied.

If the task is not approved, is ambiguous, or conflicts with an approved design, stop and explain what is needed. Do not infer approval from a proposed task.

## Implementation procedure

1. Restate the task scope and acceptance criteria briefly.
2. Identify the smallest set of changes that can satisfy them.
3. Follow existing repository conventions and approved architecture.
4. Implement without unrelated refactoring or scope expansion.
5. Add or update tests for changed behavior, including important error and permission paths.
6. Run relevant formatters, linters, type checks, and tests that are available and appropriate.
7. Inspect the final diff for unintended changes, secrets, debug code, or generated files.
8. Update relevant application documentation.
9. Update task status, progress log, verification results, and known limitations in `docs/05-TASKS.md`.
10. Record material decisions or approved deviations in `docs/06-DECISIONS.md`.

## Special handling

- If implementation requires a material design change, stop and propose it. Do not silently change the design.
- If a dependency or external service is unavailable, use a mock only when consistent with approved scope and clearly identify it.
- If a test cannot run, report it as not run. Do not report it as passed.
- Do not weaken security, authorization, validation, or data isolation to make a test or demo pass.
- Do not implement adjacent tasks simply because they are convenient.

## Completion report

Report task ID and outcome, main changes and affected files, acceptance criteria met or unmet, tests actually run and exact outcomes, manual tests the user should perform, known limitations / assumptions / follow-up work, and whether the task is ready for review.

Set the task to `Review needed`, not `Done`, when user review or manual acceptance is still required.

## Stop condition

After completing the approved task and reporting the result, stop. Wait for the user's next instruction before starting another task.
