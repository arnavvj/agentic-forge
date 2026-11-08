# FEEDBACK: Manual-Test Results and Requested Changes

Turn the user's notes, observations, or requested changes into traceable entries in section 3 of `docs/04`. For a change to the requirements or design itself, see "Design changes in chat" below. Preserve the user's intent. Implement a fix only after explicit approval, or when the user clearly asks for it.

## Procedure (`FEEDBACK: ...`)

1. Read the related task and the affected design and decision records.
2. Pin down the observed behavior: user action, expected, actual, reproducibility. Ask if unclear.
3. Inspect logs, code, and tests where available. Do not assume the user's suggested cause; separate a confirmed cause from a hypothesis.
4. Classify: bug, missing requirement, usability, performance / reliability, design change, or new scope.
5. Propose the smallest correction that fixes the underlying issue, with the tests to add or update.
6. Add an `FB-XXX` row to section 3 as `Proposed`. For a material design or scope change, also add a `Proposed` decision to section 4.
7. Present the analysis and proposal, then stop. Reporting a problem is not approval of a solution.

## Implementing a fix (`APPROVE FIX FB-XXX`, or an explicit instruction to fix)

If the fix conflicts with the approved design or creates a material security or data risk, stop and surface it before changing anything.

1. Record the approval in section 3 (`CLAUDE.md` section 5).
2. Confirm the scope you understood; implement only the approved fix.
3. Add regression coverage where practical. Run the relevant checks; record actual results.
4. Update "Now". The item stays `Approved` until accepted.
5. Leave the change uncommitted for `REVIEW FB-XXX` and `ACCEPT FB-XXX`; on acceptance it becomes `Fixed` and is committed.
6. Report the change, verification, limitations, and the manual test to repeat.

---

## Design changes in chat (`CHANGE: ...`)

Lets the user change requirements or design in chat instead of editing files. `CHANGE:` is the user's explicit permission to edit `docs/00` to `docs/03` for that change.

1. Restate the change in one line. If it is ambiguous, ask when the answer changes scope or security; otherwise state your assumption in the decision and flag it in the report.
   If it conflicts with a `P1` intake row, a non-negotiable, or a security standard, surface that before editing anything.
2. Record the user's rule in `docs/04` section 4 as `Approved`, with the approval record (`CLAUDE.md` section 5) and the design section or intake row it supersedes. If it implies a non-routine decision the user did not state (an auth, tenancy, data, or new-service mechanism; see `00-STANDARDS.md` section 2), record that mechanism separately as `Proposed` with a recommendation.
3. Make the smallest matching edit to the affected design document and intake row, so the documents stay the source of truth. Also correct any existing cell the change directly contradicts. In a diagram, change only labels and nodes; if you add a component, add its row to the build scope table.
4. Assess the impact on tasks. Update affected `Proposed` and `Approved` tasks in `docs/04`. A changed `Approved` task and every new task are `Proposed` unless the user approved them in the same message. Never change `Done` tasks; propose follow-ups.
5. Report the impact in a few lines and any approval needed. If the change reshapes milestones or the core journey, recommend `REPLAN`.
