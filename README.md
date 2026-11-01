# agentic-forge
Your agentic app-building sidekick for `claude`

A reusable, documentation-only toolkit for directing Claude Code through the design, implementation, review, and refinement of full-stack applications that include AI agents or agentic workflows.

The toolkit is domain-agnostic and technology-agnostic. It captures your project-specific design and supplies reusable engineering guidance. It does not prescribe a framework, model provider, database, cloud, agent topology, or architecture.

## Core working agreement

- **You own the system design.** You define the problem, requirements, architecture, agent behavior, constraints, and acceptance criteria.
- **The toolkit supplies engineering guidance.** Standards and defaults help Claude make sound choices without replacing your design.
- **Claude Code is the implementation worker.** It reads your design, proposes a plan, and implements approved work.
- **You remain the decision maker.** You approve plans, review changes, run manual tests, give feedback, and accept the result.

## Contents

```text
agentic-forge/
├── README.md                         This guide (toolkit only; do not copy)
├── CLAUDE.md                         Claude's working agreement, precedence, commands, approvals
├── docs/
│   ├── 01-PROJECT.md                 You: problem, users, journey, requirements, delivery profile
│   ├── 02-DESIGN_SOFTWARE.md         You: architecture, stack, identity, integrations, execution
│   ├── 03-DESIGN_AGENT_WORKFLOW.md   You: agents, tools, limits, safety, evaluation
│   ├── 04-PLAN.md                    Claude proposes; you approve
│   ├── 05-TASKS.md                   Shared: current state, tasks, feedback log
│   └── 06-DECISIONS.md               Shared: decision log
└── instructions/
    ├── 00-STANDARDS.md               Delivery profiles, routine defaults, engineering and agent standards, git policy
    ├── 01-START.md                   START, APPROVE PLAN, REPLAN
    ├── 02-IMPLEMENT.md               IMPLEMENT (single task or batch)
    ├── 03-REVIEW.md                  REVIEW, ACCEPT
    ├── 04-FEEDBACK.md                FEEDBACK, APPROVE FIX
    └── 05-CLOSE.md                   CLOSE PROJECT
```

## Setup for a new project

1. Create and clone the project repository.
2. Copy **only** `CLAUDE.md`, `docs/`, and `instructions/` into the project root. Do not copy this README, `LICENSE`, or `.gitignore`; the project needs its own.
3. If the project already has a `CLAUDE.md` or a `docs/` folder, merge them instead of overwriting. Append the toolkit's `CLAUDE.md` to the existing one, and place the toolkit's files beside any existing docs.
4. Open Claude Code from the project root.

## Workflow and time budget

| When | You | Claude |
|---|---|---|
| **0–20 min** | Fill **Part A** of `01`, `02`, and `03`. Mark anything you don't want to decide as `Claude proposes`. Say `START`. | Inspects the repo, writes the plan and proposed tasks, lists blocking decisions. |
| | Resolve the blocking decisions. Say `APPROVE PLAN`. | Records the approval, marks the tasks approved. |
| **Iteration 1** | `IMPLEMENT TASK-001` (or `IMPLEMENT M1`), then `REVIEW TASK-001`, then `ACCEPT TASK-001`. | Implements, tests, and reports; reviews the diff; commits on acceptance. |
| **By ~1 hour** | Run the app, test it manually, give `FEEDBACK: ...`. Refine **Part B** and Part A from what you learned. Say `REPLAN`. | Logs the feedback, proposes fixes, diffs the design changes, proposes plan v2. |
| **Iterations 2+** | Repeat: implement, review, accept, feedback, refine. | |
| **End** | `CLOSE PROJECT`, then your final acceptance. | Verifies, reports readiness, writes the handoff and hardening gap list. |

Part A is the minimum Claude needs to plan a first vertical slice. Part B adds precision; fill it as the design matures. You don't need it before the first build.

## Commands

These are natural-language conventions defined in `CLAUDE.md`, not built-in Claude Code commands. Equivalent wording works. Approval must be explicit.

| You say | Claude |
|---|---|
| `START` | Inspects, identifies gaps, proposes a plan and tasks. No application code. |
| `APPROVE PLAN` | Records your approval; marks the plan's tasks `Approved`. |
| `REPLAN` | Proposes plan and task updates after design refinement, a profile change, or closeout. |
| `IMPLEMENT TASK-001` | Implements one approved task, leaves it uncommitted, reports test results. |
| `IMPLEMENT M1` / `IMPLEMENT TASK-001..TASK-003` | Implements an approved batch; stops at the first failure or blocker. |
| `REVIEW TASK-001` | Reviews the uncommitted diff without changing code. |
| `ACCEPT TASK-001` | Marks the task `Done` and commits it. |
| `FEEDBACK: ...` | Analyzes your manual-test notes, logs `FB-XXX`, proposes a fix. |
| `APPROVE FIX FB-001` | Implements the approved fix, leaves it uncommitted. Then `REVIEW FB-001` and `ACCEPT FB-001`. |
| `STATUS` | Reports the current state. Changes nothing. |
| `CLOSE PROJECT` | Runs closeout checks and prepares the handoff. |

## Filling in the templates

| Value | Meaning |
|---|---|
| `[x]` | Selected choice or requirement. |
| `[ ]` | Not selected. Never treated as approval. |
| Blank | Unknown. A material blank in Part A becomes a blocking question at `START`. |
| `Claude proposes` | You delegate the choice. Claude recommends it in the plan; it is approved with the plan. |
| `N/A` | Not applicable. |
| `Later` | Deliberately deferred. Claude will not implement it now. |

A blank Part B section is treated as `Claude proposes`. Routine, non-material details use the defaults in `instructions/00-STANDARDS.md`. Claude lists every default it applied in the plan.

### Delivery profile

Choose **Prototype**, **MVP**, or **Production candidate** in `01-PROJECT.md`. The profile sets the default depth of testing, evaluation, records, observability, and infrastructure, and the target readiness at close. To harden later, change the profile and say `REPLAN`. The `CLOSE PROJECT` hardening gap list feeds that plan.

## Approvals and records

- Claude never approves anything. When you approve in chat, Claude records it in the relevant file with a short summary of your message: `Approved (chat, YYYY-MM-DD): <summary>`. That record lets a new session see what is approved.
- `docs/05-TASKS.md` starts with **Current state**. Claude reads it at the start of every session.
- An approved decision in `docs/06-DECISIONS.md` supersedes the design documents on the point it covers. You may update the design document later to match.
- Claude commits only after review, on `ACCEPT`, one commit per task or batch. It never pushes unless you ask.

## Important boundaries

- `CLAUDE.md` and `instructions/` guide Claude Code. They are **not** system prompts for agents inside your application. Runtime prompts belong in the application's source code.
- Claude must not claim a test passed unless it ran the test and saw the result.
- A successful demo does not, by itself, establish production readiness.
- Keep secrets, tokens, passwords, private keys, and real customer data out of these documents and out of Git history.

## Maintaining the toolkit

Keep this repository as the canonical toolkit. Improve the reusable instructions and templates here. Promote a change from a project back into the toolkit only when it is genuinely reusable across projects.

The toolkit stays documentation-only. Do not add Python scripts, generators, YAML or JSON configuration, or other automation to it. (Applications built with it may use whatever their design requires.) When asking Claude to edit the toolkit itself, say so explicitly; in this repository, the `docs/` files are templates.
