# START: Understand the Project and Propose a Plan

## Objective

Understand the user's approved project context and the existing repository. Produce a focused implementation plan for user approval. Do not begin application implementation during this step.

## Required reading

Read `CLAUDE.md`, `docs/01-PROJECT.md`, `docs/02-DESIGN_SOFTWARE.md`, `docs/03-DESIGN_AGENT_WORKFLOW.md`, `docs/06-DECISIONS.md` if populated, and relevant existing repository files, manifests, application code, and tests. Read the existing plan and task files if they already contain work. Preserve useful content.

## Procedure

1. Inspect the repository. Identify its state, language, framework, dependencies, existing features, tests, and conventions.
2. Summarize the problem, users, primary journey, MVP scope, architecture, and (if applicable) agent workflow.
3. Map requirements to the proposed implementation. Identify missing requirements, contradictions, security concerns, and technical risks.
4. Separate blocking questions (materially affecting architecture, security, data access, permissions, cost, or core behavior) from non-blocking details that can safely use an established convention or documented routine default.
5. Do not treat blank or unchecked fields as approved choices.
6. Recommend the smallest useful end-to-end vertical slice.
7. Propose milestones and small, testable tasks. Include dependencies and acceptance criteria.
8. Identify what can be mocked or deferred without misrepresenting the product.
9. Define how critical requirements and failure paths will be verified.
10. Write the proposal to `docs/04-PLAN.md` with status `Proposed for approval`.
11. Do not mark tasks approved. Do not create or modify application code.

## Planning principles

- The user's design is authoritative. Do not redesign it to match your preferred stack or framework.
- Prefer focused delivery over speculative infrastructure.
- Do not introduce multiple agents, microservices, a queue, a durable workflow engine, or extra model providers unless justified by the approved design and requirements.
- Preserve a path to future hardening without forcing production-scale infrastructure into the MVP.
- For agentic functionality, explicitly plan tool boundaries, authorization, state, failure handling, human approval where applicable, and evaluations.
- Distinguish agent graph state / transitions from durable job lifecycle management when both are present.
- Plan automated checks and identify manual tests the user must perform.

## Output to the user

Report your understanding of the intended outcome, repository state, blockers / conflicts / risks / assumptions, proposed vertical slice and milestones, where the plan was written, and the explicit approval needed before implementation.

## Stop condition

Stop after presenting the proposed plan. Wait for the user to approve it or request changes. A request to review, discuss, or explain the plan is not approval to implement it.
