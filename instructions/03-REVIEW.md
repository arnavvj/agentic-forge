# REVIEW: Inspect an Implementation

## Objective

Review a task's implementation against its acceptance criteria, the approved design, and the standards. Identify actionable findings. Do not modify code during a review unless the user explicitly asks you to fix findings.

## Review inputs

Read `CLAUDE.md`, `instructions/00-STANDARDS.md`, the task and its acceptance criteria, the related design sections and decisions, and the verification results. The diff under review is the uncommitted change against `HEAD` (`git diff HEAD`, plus untracked files). Read the affected code around the diff, not only the diff itself.

Where practical, run the review in a fresh session or a separate reviewing agent, to reduce the bias of reviewing your own work.

## Review dimensions

### 1. Requirements and behavior
- Does the change satisfy the task's acceptance criteria?
- Are the expected journeys, edge cases, and failure paths handled?
- Has scope changed without approval?

### 2. Architecture and maintainability
- Are component boundaries and the approved design respected?
- Are new abstractions and dependencies justified?
- Are errors, state, and side effects handled clearly?

### 3. Security and data handling
- Are authentication and authorization enforced at trusted boundaries?
- Are tenant, user, and resource boundaries preserved?
- Are secrets or sensitive data exposed in logs, errors, prompts, or source control?
- Is untrusted input, including retrieved content and tool output, handled safely?

### 4. Agent and tool behavior (when applicable)
- Does each agent stay within its card in `docs/03-DESIGN_AGENT_WORKFLOW.md`?
- Are tools permission-checked and validated in code, outside the model?
- Are limits, timeouts, retries, idempotency, and partial failures handled?
- Are handoff payloads validated, and are human approvals enforced in code?
- Do the relevant eval cases pass?

### 5. Tests and verification
- Do tests cover critical behavior and failure paths at the depth the profile requires?
- Are the tests meaningful rather than coupled to implementation details?
- Were the required checks actually run?

### 6. User experience and operations
- Are loading, progress, empty, error, and limit-reached states understandable?
- Are logs sufficient to diagnose failures?

## Finding severity

- **Critical:** Security, data-loss, unauthorized-action, or integrity risk. Blocks acceptance.
- **High:** Major requirement failure or significant reliability or security issue. Blocks acceptance.
- **Medium:** Incorrect or incomplete behavior, a maintainability issue, or an important test gap.
- **Low:** Minor issue with limited impact.
- **Informational:** Observation or suggestion, not a blocker.

## Output

For each finding: severity, location, what is wrong, why it matters, the recommended correction, and whether it blocks acceptance. Then summarize what was reviewed, the test status, open questions, and the result: `Pass`, `Pass with follow-ups`, or `Changes required`.

Prioritize. Avoid speculative findings and style-only comments.

## Stop condition

Present the findings and wait. Fix findings only when the user explicitly asks (for example "fix the High findings"). Fixes become part of the same uncommitted diff. Re-run the affected checks and review again as needed.

---

## Acceptance and commit (`ACCEPT TASK-XXX` or `ACCEPT FB-XXX`)

When the user explicitly accepts a reviewed task, batch, or feedback fix:

1. Confirm that no Critical or High findings remain open. If any remain, say so and ask before proceeding.
2. Record the acceptance in `docs/05-TASKS.md` with an approval record summarizing the user's message: a task becomes `Done`; a feedback item becomes `Fixed`. Record any follow-ups as `Proposed` tasks.
3. Commit the changes, including their documentation updates, following the git policy in `instructions/00-STANDARDS.md`: message `TASK-XXX: <title>` or `FB-XXX: <summary>`, current branch, no push.
4. Update "Current state" with the commit and the next task.
5. Report the commit hash and the next step.
