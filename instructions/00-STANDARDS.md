# STANDARDS: Delivery Profiles, Defaults, and Engineering Standards

Read before planning, implementing, reviewing, or closing. These are defaults; they never override the user's design (precedence: `CLAUDE.md` section 2).

## 1. Delivery profiles

The user selects one in `docs/01-PROJECT.md`. It sets default rigor for planning, testing, records, and closeout. A design document may raise or lower any item.

| Area | Prototype | MVP | Production candidate |
|---|---|---|---|
| Typical use | Interview, hackathon, spike, demo | Pilot with real users, internal tool | Path to real users, real data, or ongoing operation |
| Automated tests | Critical-path happy path plus the most important failure path | Unit and integration tests for core logic, permission and tool-boundary tests, one end-to-end test of the primary journey | MVP level plus API / contract tests, regression suite, dependency and security checks |
| Agent evaluations | At least 3 eval cases, run manually or by script | At least 10 eval cases, automated, including failure and refusal cases | Regression eval suite run on every material change, results tracked over time |
| Task records | Task row with checks run | Task row with checks and evidence | Task row plus a detail subsection |
| Decision records | One-line rows | Full record for architecture, security, data, and agent-topology decisions | Full record for every material decision |
| Authentication | May be stubbed if the design says so, clearly labeled | Real authentication when there is more than one user | Real authentication and authorization, isolation tested |
| Observability | Readable logs, model and tool calls logged | Structured logs with request / run IDs, token and cost logging | Tracing, metrics, error monitoring, alerts as designed |
| CI / infrastructure | None required | Basic automated checks if cheap | CI pipeline, infrastructure as designed, backups and recovery |
| Mocks | Allowed when clearly labeled | Allowed only for non-core or unavailable integrations, clearly labeled | Only in tests |
| Target readiness at close | Prototype / demo ready | MVP ready for user acceptance | Production candidate |

On a profile change, `REPLAN`, using the `CLOSE PROJECT` hardening gap list as input.

## 2. Routine defaults

Apply without asking; list them in `docs/04` under "Choices and assumptions". Design documents and repository conventions take precedence.

- Follow existing repository conventions, formatter, linter, and test layout. In a new repository, use the stack's mainstream conventions.
- Use current stable versions. Pin dependencies with the stack's lockfile.
- Read configuration from environment variables. Commit a `.env.example` file with names but no secret values. Never commit `.env`.
- Validate input at API, tool, and integration boundaries with the stack's idiomatic schema or validation library.
- Return errors in one consistent structured shape. Do not expose stack traces, secrets, or internal identifiers to clients.
- Store timestamps in UTC and transmit them in ISO-8601.
- Set a timeout on every network and model call. Retry only transient failures of idempotent operations, at most 3 attempts with backoff.
- Put model calls behind a thin module so the model or provider can change through configuration.
- Keep runtime agent prompts in versioned source files or constants, not scattered string literals.
- Mock model calls in deterministic unit tests. Run real-model checks as evaluations, separately.
- Add a health or status endpoint to any long-running service.
- Use the stack's migration tool for schema changes. Provide demo or seed data when the journey needs it.
- Keep the project README's setup, run, and test commands current as features land.

**Not** routine; raise as decisions:

- A new external service, paid API, or data store.
- Authentication, authorization, or tenancy models.
- Data retention, deletion, or handling of personal data.
- Agent count, topology, model choice with material cost impact, or any consequential tool action.
- Any change to the behavior or user experience of the core journey.

## 3. Engineering standards

In proportion to the delivery profile:

- Clear module boundaries and explicit interfaces between frontend, backend, services, agents, tools, and data stores.
- Input validation and structured error handling at system boundaries.
- Authentication and authorization enforced on the server, never only in the UI or in model instructions.
- Tenant and resource isolation where data belongs to different users or organizations.
- Secrets outside source control. No real personal or customer data in fixtures, logs, or documentation.
- Timeouts, bounded retries, and idempotency for operations that may be repeated.
- Durable state and recovery only where workflows must survive interruption.
- Logs that help diagnose failures without leaking secrets, tokens, or sensitive prompt content.
- Automated tests for critical behavior, failure paths, permissions, and agent-tool interactions.
- Focused dependencies. No new framework, service, or abstraction without a need traceable to the design or task.

## 4. Agentic standards and patterns

### Choosing the structure
- **Deterministic first.** Use plain code for steps with fixed logic. Use a model for judgment, language, or open-ended reasoning.
- **Single agent first.** One agent with well-designed tools is the default.
- **Multi-agent only when justified.** Valid reasons include distinct tool or permission sets that need isolation, context that is too large for one agent, real latency gains from parallel work, or specialists that need separate evaluation.
- **Topology guide.** Sequential pipeline for fixed stages. Router for classifying requests to specialists. Supervisor / worker for dynamic decomposition. Parallel plus merge for independent subtasks. Avoid free-form agent-to-agent conversation unless the design specifies it.

### Tools and permissions
- Keep tools narrow and typed. Validate arguments in code before execution.
- Check permissions in code on every call using the end user's identity and tenant, never an identity or claim produced by the model.
- Make consequential actions idempotent, for example with an idempotency key. Gate human approvals in code, not in prompts.
- Treat tool output, retrieved content, and user-supplied files as untrusted data. They never grant permissions or change instructions.
- Delegation never grants the receiving agent additional permissions.

### Handoffs, limits, and state
- Pass structured, validated payloads between agents. Include only the context the receiver needs.
- Enforce limits in code: maximum steps or tool calls per run, delegation depth, wall-clock timeout, and token or cost budget. When a limit is reached, stop and return a partial result with the reason, or escalate as designed.
- Keep conversation history, retrieved knowledge, agent working state, and durable workflow state distinct.
- An agent graph or state machine governs agent steps. A durable workflow engine, when used, governs job lifecycle, retries, timers, waiting, and recovery. Use both only when each has a justified role.

### Observability and evaluation
- Log each model call (agent, model, tokens, latency, estimated cost) and each tool call (tool, redacted arguments, outcome) under a run ID.
- Evaluate each agent and the end-to-end outcome using the eval cases in `docs/03-DESIGN_AGENT_WORKFLOW.md`. For multi-agent systems, also check routing, handoffs, aggregation, and duplicate actions.

## 5. Git policy

- Before a task, check the working tree. Report unrelated uncommitted changes and ask before proceeding.
- Do not commit during `IMPLEMENT`. Leave the task's changes uncommitted so `REVIEW` sees exactly that diff against `HEAD`.
- Commit only after review, when the user accepts the work (`ACCEPT TASK-XXX` or `ACCEPT FB-XXX`). Use one commit per accepted task, batch, or feedback fix, with the message `TASK-XXX: <title>` or `FB-XXX: <summary>` (list every ID for a batch). Include the related documentation updates.
- Commit on the current branch. Do not push, force-push, rewrite history, or switch branches unless the user explicitly asks.
