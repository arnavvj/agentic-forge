# REVIEW: Inspect an Implementation

## Objective

Review the implementation against approved requirements, architecture, task acceptance criteria, and engineering standards. Identify actionable findings. Do not modify code during a review unless the user explicitly asks you to fix findings.

## Review inputs

Read `CLAUDE.md`, the relevant task and acceptance criteria, related approved design sections and decisions, implementation diff, affected code, and test results / test code.

## Review dimensions

### 1. Requirements and behavior
- Does the change satisfy the approved task?
- Are expected user journeys and edge cases covered?
- Has scope changed without approval?

### 2. Architecture and maintainability
- Are component and service boundaries respected?
- Is the implementation consistent with the approved design?
- Are abstractions and dependencies justified?
- Are errors, state, and side effects handled clearly?

### 3. Security and data handling
- Are authentication and authorization enforced at trusted boundaries?
- Are tenant, user, and resource boundaries preserved?
- Are secrets or sensitive data exposed in logs, errors, prompts, or source control?
- Are untrusted input and external content handled safely?

### 4. Agent and tool behavior (when applicable)
- Do agents follow assigned responsibilities?
- Are tools limited and authorized outside the model?
- Are tool inputs and outputs validated?
- Are retries, timeouts, cancellation, duplicate actions, and partial failures handled?
- Are handoffs and shared context correct?
- Are human approval requirements enforced?
- Are token, latency, and cost limits respected where required?

### 5. Tests and verification
- Do tests cover critical behavior and failure paths?
- Are tests meaningful rather than coupled to implementation details?
- Were required checks actually run?
- Are important behaviors untested?

### 6. User experience and operations
- Are loading, progress, empty, error, and retry states understandable?
- Are logs and traces sufficient to diagnose failures?
- Are operational limitations documented?

## Finding severity

- **Critical:** Serious security, data-loss, unauthorized-action, or system-integrity risk. Must be resolved before acceptance.
- **High:** Major requirement failure or significant reliability / security issue.
- **Medium:** Incorrect or incomplete behavior, maintainability issue, or important test gap.
- **Low:** Minor issue with limited impact.
- **Informational:** Observation or improvement suggestion, not a blocker.

## Output format

For each finding, include severity, file / component and relevant location, what is wrong, why it matters, recommended correction, and whether it blocks task acceptance.

Also report what was reviewed, requirements and acceptance criteria checked, tests examined and actual status, positive observations, open questions / limitations, and overall result: `Pass`, `Pass with follow-ups`, or `Changes required`.

Prioritize findings. Avoid speculative findings and style-only comments that do not improve correctness or maintainability.

## Stop condition

Do not fix findings during review unless explicitly instructed. Present findings and wait for the user's direction.
