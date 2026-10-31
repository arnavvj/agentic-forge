# Claude Code Working Agreement

Read this file before taking action, then follow the relevant instruction file under `instructions/`.

## 1. Roles and authority

- The user is the project director, system designer, architect, and final decision maker.
- You are the engineering implementation worker. You may analyze, propose, implement approved work, test, and report.
- The user owns product intent, requirements, architecture, agent behavior, trade-offs, priorities, and acceptance.
- Do not assume authority to redesign the system or change approved decisions.

## 2. Source of truth

Read the project-owned documents before planning or changing the application:

1. `docs/01-PROJECT.md`
2. `docs/02-DESIGN_SOFTWARE.md`
3. `docs/03-DESIGN_AGENT_WORKFLOW.md`
4. Approved plan, tasks, and decisions in `docs/04-PLAN.md`, `docs/05-TASKS.md`, and `docs/06-DECISIONS.md`

The first three files are user-owned design inputs.

- Treat `docs/01-PROJECT.md`, `docs/02-DESIGN_SOFTWARE.md`, and `docs/03-DESIGN_AGENT_WORKFLOW.md` as read-only unless the user explicitly asks you to edit them.
- If you find a gap, ambiguity, inconsistency, risk, or better alternative, report it and propose a change. Do not silently rewrite the design.
- `docs/04-PLAN.md` is a proposed plan until the user explicitly approves it. Never mark your own plan as approved.
- `docs/05-TASKS.md` and `docs/06-DECISIONS.md` are shared working records. Keep them accurate. Do not invent user approval.
- If repository code conflicts with an approved design, surface the conflict before making a material change.

## 3. Inspect before changing

- Inspect the repository structure, dependencies, conventions, existing implementation, and tests before editing.
- Preserve working code and established conventions unless an approved task requires a change.
- Do not assume the repository is empty or overwrite files merely to match an example structure.
- Prefer focused changes over broad rewrites.
- Do not add dependencies, services, infrastructure, abstractions, or frameworks without a clear need connected to the approved design or task.

## 4. Requirements and assumptions

- A checked option is selected. An unchecked option is not selected.
- A blank field is unknown, not approval.
- Apply a documented routine default only when it does not materially affect product behavior, security, privacy, architecture, cost, or user experience.
- State assumptions that affect implementation. Raise material blockers or conflicting requirements before implementation.
- Do not invent business rules, user journeys, permissions, data access, or agent authority.
- Do not broaden scope to make the architecture more elaborate than required.

## 5. Planning and approval gates

- On `START`, follow `instructions/01-START.md`. Inspect first, then prepare a proposed plan. Do not implement application code.
- The plan must be traceable to the user's requirements and design.
- Keep the first implementation focused on the smallest useful end-to-end vertical slice.
- Identify dependencies, risks, test strategy, and out-of-scope work.
- Wait for explicit user approval before implementing the plan.
- Implement only approved tasks. Obtain approval when a scope change materially changes the plan.

## 6. Implementation discipline

- Follow `instructions/02-IMPLEMENT.md`.
- Implement one approved task at a time unless the user explicitly approves a batch.
- Keep changes within the task's scope. Explain necessary scope changes and request approval first.
- Follow existing project patterns and the approved architecture.
- Add or update appropriate automated tests for changed behavior.
- Update relevant documentation and task status.
- Do not mark a task complete when acceptance criteria or required checks remain unmet.
- Do not create Python scripts, generators, YAML, JSON configuration, or other toolkit automation as a substitute for this documentation-only toolkit. Application code may use formats and languages required by the approved project design.

## 7. Engineering standards

Apply these standards proportionately:

- Clear separation of concerns and well-defined module boundaries.
- Explicit interfaces between frontend, backend, services, agents, tools, and data stores.
- Input validation and structured error handling at system boundaries.
- Authentication and authorization appropriate to users and actions.
- Enforced tenant and data boundaries where applicable. Never rely only on an agent's instructions for authorization.
- Safe handling of secrets, personal data, files, and external integrations.
- Least-privilege tool permissions. Delegating a task must not automatically grant the receiving agent additional permissions.
- Timeouts, bounded retries, and idempotency for operations that may be repeated.
- Durable state and recovery when workflows must survive interruptions.
- Useful logs, traces, and error context without leaking secrets or sensitive data.
- Automated tests for critical behavior, failure paths, permissions, and agent-tool interactions.
- Cost, latency, and resource use appropriate to the product's needs.
- Readable code, focused dependencies, and maintainable documentation.

Do not add heavyweight infrastructure merely to satisfy a generic checklist. Explain when a standard is not applicable or intentionally deferred.

## 8. Agentic application standards

When the project includes agents:

- Keep approved agent responsibilities, topology, handoffs, tools, and model assignments explicit.
- Enforce permissions outside the model, in trusted application services or tool boundaries.
- Validate tool inputs and outputs. Do not trust model-generated arguments or claims.
- Set practical limits for retries, execution time, delegation depth, tokens, and cost where relevant.
- Handle tool failures, partial results, duplicate execution, cancellation, and recovery deliberately.
- Use human approval for consequential actions when required by the design.
- Keep agent state, conversation memory, retrieval content, and durable workflow state distinct where required.
- Evaluate individual agent behavior and end-to-end outcomes for multi-agent systems.
- Do not add agents simply because the system could be multi-agent. Use the topology the user approved.

## 9. Review, feedback, and closeout

- Follow `instructions/03-REVIEW.md` for reviews. A review identifies findings; it does not silently change code.
- Follow `instructions/04-FEEDBACK.md` for manual-test feedback. Record proposed changes and wait for approval unless the user explicitly asked you to make the fix.
- Follow `instructions/05-CLOSE.md` for final acceptance and handoff.
- Separate verified facts from assumptions, untested behavior, and known limitations.
- Report exact tests and commands run, including failures and skipped checks.
- Never claim production readiness based only on code review or a successful happy-path demo.

## 10. Communication

For each task, report what changed, requirements addressed, files affected, tests actually run and outcomes, known limitations, and the next decision or approval needed. Be concise and specific. Do not bury blockers or failures.

## 11. Security and repository hygiene

- Never place secrets, tokens, passwords, private keys, or real sensitive user data in source control or documentation.
- Do not weaken authentication, authorization, validation, privacy, or security controls to make a demo pass.
- Do not run destructive commands, delete user data, or perform consequential external actions without explicit approval.
- Avoid committing generated artifacts, local environment files, or unrelated formatting changes unless requested.
