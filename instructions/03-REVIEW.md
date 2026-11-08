# REVIEW: Inspect an Implementation

Review a task or feedback fix against its acceptance criteria, the approved design, and the standards. Report actionable findings. Do not change code unless the user explicitly asks you to fix findings.

**Inputs:** the task and acceptance criteria, related design sections and decisions, verification results, and the uncommitted diff against `HEAD` (`git diff HEAD` plus untracked files). Read the affected code around the diff, not only the diff. Where practical, review in a fresh session or a separate agent to reduce self-review bias.

## Review dimensions

1. **Requirements and behavior:** acceptance criteria met? Journeys, edge cases, and failure paths handled? Scope changed without approval?
2. **Architecture and maintainability:** component boundaries and approved design respected? New abstractions and dependencies justified? Errors, state, and side effects handled clearly?
3. **Security and data:** authentication and authorization enforced at trusted boundaries? Tenant, user, and resource boundaries preserved? Secrets or sensitive data exposed in logs, errors, prompts, or source control? Untrusted input (including retrieved content and tool output) handled safely?
4. **Agents and tools (if applicable):** each agent within its card in `docs/03`? Tools permission-checked and validated in code, outside the model? Limits, timeouts, retries, idempotency, and partial failures handled? Handoff payloads validated and human approvals enforced in code? Relevant eval cases pass?
5. **Tests:** critical behavior and failure paths covered at the profile's depth? Tests meaningful rather than coupled to implementation details? Required checks actually run?
6. **UX and operations:** loading, progress, empty, error, and limit-reached states understandable? Logs sufficient to diagnose failures?

## Severity

- **Critical:** security, data-loss, unauthorized-action, or integrity risk. Blocks acceptance.
- **High:** major requirement failure, or significant reliability or security issue. Blocks acceptance.
- **Medium:** incorrect or incomplete behavior, maintainability issue, or important test gap.
- **Low:** minor issue, limited impact.
- **Informational:** observation or suggestion.

## Output and stop

Per finding: severity, location, what is wrong, why it matters, recommended fix, and whether it blocks acceptance. Then: what was reviewed, test status, open questions, and the result (`Pass`, `Pass with follow-ups`, or `Changes required`). Prioritize; no speculative or style-only findings.

Stop and wait. Fix findings only on explicit request (e.g. "fix the High findings"); fixes join the same uncommitted diff. Re-run affected checks and re-review as needed.

---

## Acceptance and commit (`ACCEPT TASK-XXX` or `ACCEPT FB-XXX`)

1. Confirm no Critical or High findings remain open; if any do, say so and ask before proceeding.
2. `docs/04`: record the acceptance (`CLAUDE.md` section 5). A task becomes `Done`; a feedback item becomes `Fixed`. Add follow-ups as `Proposed` tasks.
3. Commit the changes with their documentation updates, per the git policy (`00-STANDARDS.md` section 5).
4. Update "Now" with the commit and next task. Report the commit hash and next step.
