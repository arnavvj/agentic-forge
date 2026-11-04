# START: Understand the Project and Propose a Plan

## Objective

Understand the user's design and the existing repository, then propose a focused plan and task list for approval. Do not write application code during this step.

## Required reading

`CLAUDE.md`, `instructions/00-STANDARDS.md`, `docs/00-REQUIREMENTS.md`, `docs/01-PROJECT.md`, `docs/02-DESIGN_SOFTWARE.md`, `docs/03-DESIGN_AGENT_WORKFLOW.md`, `docs/05-TASKS.md`, `docs/06-DECISIONS.md`, any existing `docs/04-PLAN.md`, and relevant repository files: manifests, application code, tests, and existing documentation. Preserve useful existing content.

## Procedure

1. Inspect the repository: state, language, framework, dependencies, features, tests, and conventions.
2. Note the delivery profile. If it is not selected, treat that as a blocking question.
3. Note any design document whose "Part A ready for planning" box is unchecked. Treat it as a draft, say so in the report, and still produce the plan.
4. Summarize the problem, users, core journey, must-have requirements, architecture, and agentic design.
5. Read the Mermaid diagrams: the architecture diagram in `docs/02` (section 1) and the agent architecture diagram in `docs/03` (section 3). Check that every component, agent, tool, data store, and approval gate they show matches the text and tables, and that components named in the text appear in the diagrams. Treat a mismatch as a blocking decision.
6. Map requirements to the proposed implementation. Identify gaps, contradictions, security concerns, and technical risks. Cross-check `docs/00-REQUIREMENTS.md` against Part A: a `Must` intake item that Part A and the plan do not cover, or that Part A contradicts, is a blocking decision. Map any intake row whose "Maps to" is blank, including the "Additional inputs" rows. An intake answer that no template field covers still applies: list it in the plan, citing the row.
7. Classify each open item:
   - **Blocking decision:** a blank or conflicting Part A item that materially affects architecture, security, data access, permissions, cost, or core behavior, or a `Must` intake gap or conflict. List it under "Decisions needed".
   - **Intake answer:** a blank Part B field that the intake answers. Use the answer and list it under "Assumptions and routine defaults applied", citing the intake row (for example `S-C1`).
   - **Proposed choice:** a `Claude proposes` field, or a blank Part B field the intake does not answer. Recommend an option under "Proposed choices".
   - **Routine default:** a non-material detail covered by `instructions/00-STANDARDS.md` or repository conventions. List it under "Assumptions and routine defaults applied".
8. Recommend the smallest useful end-to-end vertical slice of the core journey as milestone M1.
9. Propose milestones and small, testable tasks with dependencies and acceptance criteria. Size them so each can be reviewed as one coherent diff.
10. Identify what can be mocked or deferred without misrepresenting the product.
11. Define how critical requirements, failure paths, and agent behavior will be verified, at the depth the delivery profile requires.
12. Write the plan to `docs/04-PLAN.md` with status `Proposed for approval`. Record the design baseline: the date, plus the commit if `docs/00` to `docs/03` are committed.
13. Write the tasks to `docs/05-TASKS.md` with status `Proposed`. Update "Current state" to Planning, waiting on plan approval.

## Planning principles

- The user's design is authoritative. Do not redesign it to match a preferred stack or framework.
- Prefer focused delivery over speculative infrastructure. Do not introduce extra agents, services, queues, workflow engines, or model providers unless the design justifies them.
- For agentic functionality, plan the code / model / human split, tool boundaries, authorization, limits, state, failure handling, human approvals, and evaluations.
- Preserve a path to hardening without forcing production-scale infrastructure into an early delivery.

## Output to the user

Report your understanding of the outcome, the repository state, the blocking decisions, the proposed choices, the vertical slice and milestones, and what approval is needed. Keep the report short enough to read in a few minutes. The detail belongs in the plan file.

## Stop condition

Stop after presenting the plan. A request to review, discuss, or explain the plan is not approval.

---

## After plan approval (`APPROVE PLAN`)

When the user explicitly approves the plan:

1. Confirm that every blocking decision is resolved. If one is not, ask before recording approval.
2. Apply any changes or conditions the user stated.
3. In `docs/04-PLAN.md`, set the status to `Approved` and fill the approval record: `Approved (chat, YYYY-MM-DD): <short summary of the user's message and conditions>`.
4. In `docs/05-TASKS.md`, set the approved tasks to `Approved` with the same approval record. Leave tasks the user excluded as `Proposed` or `Deferred`.
5. Record resolved blocking decisions and material proposed choices in `docs/06-DECISIONS.md` as `Approved`, at the depth the delivery profile requires.
6. Update "Current state" to Implementing, with the next task.
7. Stop and wait for an `IMPLEMENT` instruction.

---

## Re-planning (`REPLAN`)

Use this when the user has refined the design documents (typically after the first or second build iteration), changed the delivery profile, or asked for a hardening plan after `CLOSE PROJECT`.

1. Re-read the requirements intake and the design documents and compare them with the design baseline in the current plan. Use `git diff` where the baseline is a commit. Summarize what changed.
2. Re-read the task list, the feedback log, and the decisions.
3. Identify the impact on completed, in-progress, and proposed tasks. Note any completed work that now conflicts with the design.
4. Propose the updated plan as a new version. Set the previous version to `Superseded`, or update it in place with a version note if the change is small.
5. Propose new or changed tasks as `Proposed`. Never change the status of `Done` tasks; propose follow-up tasks instead.
6. Update the design baseline and "Current state", report the changes, and stop for approval.
