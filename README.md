# agentic-forge
Your agentic app-building sidekick for `claude`

A reusable, documentation-only toolkit for directing Claude Code through the design, implementation, review, and refinement of full-stack applications that include AI agents or agentic workflows.

The toolkit is domain-agnostic. It captures your project-specific design while supplying reusable engineering guidance. It does not prescribe a fixed framework, model provider, database, cloud, agent topology, or application architecture.

## Core working agreement

- **You own the system design.** You define the problem, requirements, architecture, agent behavior, constraints, and final acceptance criteria.
- **The toolkit supplies reusable engineering guidance.** Its instructions help Claude implement consistently without replacing your design.
- **Claude Code is the implementation worker.** It reads your approved project context, proposes a plan, and implements approved work.
- **You remain the decision maker.** You review plans and changes, run manual tests, provide feedback, and decide when the result is accepted.

The project-specific design files are the source of truth. Claude may identify gaps, conflicts, risks, or alternatives, but must not silently rewrite your approved design.

## Repository contents

```text
agentic-engineering-toolkit/
│
├── README.md
├── CLAUDE.md
│
├── docs/
│   ├── 01-PROJECT.md
│   ├── 02-DESIGN_SOFTWARE.md
│   ├── 03-DESIGN_AGENT_WORKFLOW.md
│   ├── 04-PLAN.md
│   ├── 05-TASKS.md
│   └── 06-DECISIONS.md
│
└── instructions/
    ├── 01-START.md
    ├── 02-IMPLEMENT.md
    ├── 03-REVIEW.md
    ├── 04-FEEDBACK.md
    └── 05-CLOSE.md
```

## How to use the toolkit for a new project

1. Understand the problem and design the intended system.
2. Create an empty project repository.
3. Copy the **contents** of this toolkit repository into the project repository root. Do not place the files inside an extra nested `agentic-engineering-toolkit/` directory.
4. Open the project repository in Claude Code. Run Claude Code from the project root.
5. Fill in `docs/01-PROJECT.md`, `docs/02-DESIGN_SOFTWARE.md`, and `docs/03-DESIGN_AGENT_WORKFLOW.md`.
6. Ask Claude Code to follow `instructions/01-START.md` (or say `START`).
7. Review `docs/04-PLAN.md`. Approve it explicitly before implementation.
8. Ask Claude to implement one approved task at a time, unless you explicitly approve a batch.
9. Review the implementation, run the application, and perform your own manual tests.
10. Record feedback, approve fixes, and iterate.
11. Use `instructions/05-CLOSE.md` for final acceptance and handoff.

## What you need to fill in

Aim for a 10–15 minute first pass. You do not need to specify every technical detail before starting.

| File | Your input |
|---|---|
| `01-PROJECT.md` | Problem, target users, core journey, requirements, business rules, constraints, acceptance criteria |
| `02-DESIGN_SOFTWARE.md` | Full-stack architecture, technology choices, integrations, data, infrastructure, operational needs |
| `03-DESIGN_AGENT_WORKFLOW.md` | Agent purpose, single-agent or multi-agent design, tools, orchestration, state, safety, evaluation, budgets |

Use checkboxes for standard options and descriptive fields for project-specific behavior. Add `Other` details where needed.

### How to interpret fields

- A checked checkbox is a selected choice or requirement.
- An unchecked checkbox is not an approval.
- A blank field means the information has not been supplied. Claude must not treat it as a confirmed requirement or decision.
- Claude may use a documented routine default only when it does not materially affect product behavior, security, data handling, architecture, cost, or user experience. Material assumptions must be stated.
- Missing details that materially affect the system must be raised before implementation.
- You may mark a section `Not applicable` or `Decide during implementation` where appropriate.

## Working with Claude Code

These are suggested natural-language instructions, not built-in Claude Code slash commands:

| You say | Claude should |
|---|---|
| `START` | Read project context, inspect the repository, identify gaps, and propose a plan |
| `APPROVE PLAN` | Treat the current plan as approved and create the approved task backlog |
| `IMPLEMENT TASK-001` | Implement that approved task and report test results |
| `REVIEW TASK-001` | Review the implementation without changing code |
| `FEEDBACK: ...` | Analyze manual-test feedback and propose changes |
| `APPROVE FIX ...` | Implement the explicitly approved fix |
| `CLOSE PROJECT` | Run closeout checks and prepare the handoff report |

You can use different wording. Approval must be explicit.

## Recommended build approach

For short challenges, interviews, and hackathons:

- Build one complete, user-visible vertical slice before expanding scope.
- Prefer the simplest architecture that satisfies the approved requirements.
- A modular monolith is a starting option when it fits, not a mandatory rule.
- Mock unavailable external services when that enables a truthful end-to-end demonstration.
- Start with one model provider and the minimum necessary agent capabilities.
- Add queues, durable workflow infrastructure, multiple agents, or extra services only when justified by the design.
- Test critical paths and document what remains incomplete.

The toolkit supports later hardening. It does not require a full production platform before an MVP can be demonstrated.

## Important boundaries

- `CLAUDE.md` and `instructions/` guide Claude Code. They are **not** system prompts for agents inside your application.
- Application runtime prompts belong in your application source code or its own prompt-management system.
- Claude must not replace your project brief or approved design documents without your explicit instruction.
- Claude must not claim a test passed unless it actually ran the test and observed the result.
- A successful demo does not, by itself, establish production readiness.
- Keep secrets, access tokens, passwords, private keys, and real customer data out of toolkit documents and Git history.

## Reusing and improving the toolkit

Keep this repository as your canonical toolkit. Improve reusable instructions and templates here. For each new application, copy the current toolkit contents into the application repository and customize that project's `docs/` files. Project-specific changes should normally stay in the project repository. Promote a change back into the canonical toolkit only when it is genuinely reusable across projects.
