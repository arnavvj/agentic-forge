# FEEDBACK: Process Manual-Test Results and Requested Changes

## Objective

Convert the user's manual testing notes, observations, or requested changes into clear, traceable work. Preserve the user's intent and obtain approval before implementing a proposed fix unless the user explicitly instructs you to make it.

## Procedure

1. Read `CLAUDE.md`, the relevant task, and affected design / decision records.
2. Review the user's feedback without assuming the proposed cause is correct.
3. Clarify observed behavior: user action, expected behavior, actual behavior, and reproducibility.
4. Inspect logs, code, and tests where available. Distinguish a confirmed cause from a hypothesis.
5. Classify as bug, missing requirement, usability issue, performance / reliability issue, design change, or new scope.
6. Propose the smallest correction that addresses the underlying issue.
7. Identify affected requirements, components, tests, risks, and design impact.
8. Add a proposed task or update the relevant task in `docs/05-TASKS.md`. Do not mark it approved.
9. If a material design or scope change is required, describe it and record it as a proposed decision in `docs/06-DECISIONS.md`.
10. Present the proposed change and wait for explicit user approval.

## When the user explicitly says to fix it

If the user's instruction clearly authorizes implementation:

1. Confirm the scope understood.
2. Implement only the requested fix.
3. Add regression coverage where practical.
4. Run relevant checks and record actual results.
5. Update task progress and the decision log if needed.
6. Report the change, verification, limitations, and any remaining manual test.

If the requested fix conflicts with the approved design or creates a material security or data risk, stop and surface the conflict before changing it.

## Feedback record

- **Feedback ID / date:**
- **User's observation:**
- **Expected behavior:**
- **Actual behavior:**
- **Reproduction steps:**
- **Likely cause:** [ ] Confirmed [ ] Hypothesis [ ] Unknown
- **Proposed correction:**
- **Affected requirement / task:**
- **Tests to add or update:**
- **Approval status:** [ ] Proposed [ ] Approved [ ] Rejected
- **Outcome:**

## Stop condition

When feedback has been analyzed but not approved for implementation, stop and wait. Reporting a problem is not approval for a particular solution.
