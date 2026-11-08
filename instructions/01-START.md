# START: Understand the Project and Propose a Plan

Understand the design and the repository, then propose a plan and tasks for approval. No application code.

**Read:** all of `docs/00` to `docs/04`, plus relevant repository files: manifests, code, tests, existing docs. Preserve useful existing content.

## Procedure

1. Inspect the repository: state, language, framework, dependencies, features, tests, conventions.
2. Delivery profile not selected: blocking question.
3. A design document with "Part A ready for planning" unchecked is a draft: say so, and still plan.
4. Summarize the problem, users, core journey, must-have requirements, architecture, and agentic design.
5. Diagrams and build scope (`docs/02` section 1, `docs/03` section 3):
   - Components are services, data stores, external services, agents, tools, and approval gates; entry and exit nodes are not.
   - For `Build` and `Mock` components, check that the diagram matches the text and tables, and that components named in the text appear in the diagram. A mismatch that affects security, data access, permissions, or core behavior is a blocking decision. A minor one (e.g. a tool missing from a table) goes under "Choices and assumptions" with the resolution you used.
   - `Later` and `Out of scope` components are exempt.
   - Every diagram component gets a scope in the "Build scope" table of `docs/04`: from the design table, or proposed by you if unlisted.
6. Map requirements to the implementation. Identify gaps, contradictions, security concerns, and technical risks. Cross-check `docs/00` against Part A:
   - A `P1` intake item that Part A and the plan do not cover, or that Part A contradicts, is a blocking decision.
   - Map every intake row with a blank "Maps to", including "Additional inputs".
   - An intake answer with no matching template field still applies: list it in the plan, citing the row.
   - Data or assets the design says are provided but are missing from the repository: list under "Decisions needed".
7. Classify each open item:
   - **Blocking decision:** a blank or conflicting Part A item that materially affects architecture, security, data access, permissions, cost, or core behavior; or a `P1` intake gap or conflict. → "Decisions needed".
   - **Intake answer:** a blank Part B field the intake answers. Use it. → "Choices and assumptions", citing the row (e.g. `S-C1`).
   - **Proposed choice:** a `Claude proposes` field, a blank Part B field the intake does not answer, or an intake answer that cannot be implemented as written (give the reason). → "Choices and assumptions", with a recommendation.
   - **Routine default:** a non-material detail covered by `00-STANDARDS.md` or repository conventions. → "Choices and assumptions".
8. Milestone M1: the smallest useful end-to-end vertical slice of the core journey, using only `Build` and `Mock` components. Repository layout (`docs/02` section 3):
   - Check every `Build` and `Mock` component has a folder; state which folders M1 creates.
   - `Open to suggestions` or blank: propose changes or a layout under "Choices and assumptions".
   - `Fixed`: subfolders inside listed folders are fine, and components may share a folder; a component with no fitting folder is a blocking decision.
9. Propose milestones and small, testable tasks with dependencies and acceptance criteria, each reviewable as one coherent diff.
10. Identify what can be mocked or deferred without misrepresenting the product.
11. Define how critical requirements, failure paths, and agent behavior are verified, at the profile's depth.
12. Write section 1 of `docs/04-BUILD.md`, plan status `Proposed`. Record the design baseline: date, plus commit if `docs/00` to `docs/03` are committed. If they are not, tell the user to commit them before `APPROVE PLAN`.
13. Write tasks to section 2 as `Proposed`, replacing the template's sample rows. Set "Now" to Planning, waiting on plan approval.

## Planning principles

- The user's design is authoritative. Do not redesign it toward a preferred stack or framework.
- No extra agents, services, queues, workflow engines, or model providers unless the design justifies them.
- For agentic work, plan the code / model / human split, tool boundaries, authorization, limits, state, failure handling, human approvals, and evaluations.
- Keep a path to hardening without forcing production-scale infrastructure into an early delivery.

## Report and stop

Report the outcome, repository state, blocking decisions, proposed choices, vertical slice, milestones, and the approval needed, readable in a few minutes; detail goes in `docs/04`. Then stop. A request to review, discuss, or explain the plan is not approval.

---

## After plan approval (`APPROVE PLAN`)

1. Confirm every blocking decision is resolved; if not, ask before recording approval. An answer the user wrote in "Your answer" resolves it; "accept", "ok", or "accept recommendation" means the recommended option. An answer in the file approves that decision only; plan approval still needs `APPROVE PLAN`.
   If `docs/00` to `docs/03` are uncommitted, ask the user to commit them first, so the design baseline is a commit.
2. Apply any changes or conditions the user stated.
3. `docs/04`: plan `Approved`, plus the approval record (`CLAUDE.md` section 5).
4. Approved tasks to `Approved` with the same record. Excluded tasks stay `Proposed` or become `Deferred`.
5. Move resolved blocking decisions and material choices to section 4 as `Approved`, at the profile's depth, and clear them from "Decisions needed". Record a decision answered in the file as `Approved (file, YYYY-MM-DD): <summary>`.
6. "Now": Implementing, with the next task. Stop and wait for `IMPLEMENT`.

---

## Re-planning (`REPLAN`)

For design refinements (typically after iteration 1 or 2), a profile change, or a hardening plan after `CLOSE PROJECT`.

1. Re-read `docs/00` to `docs/03` and compare with the plan's design baseline (`git diff` if the baseline is a commit). The baseline plus the `CHANGE` decisions recorded in `docs/04` section 4 since then describe the drift. Summarize the changes.
2. Re-read the tasks, feedback log, and decisions.
3. Identify the impact on done, in-progress, and proposed tasks, including completed work that now conflicts with the design.
4. Update section 1 in place as the next plan version (`v2`), noting what changed.
5. New or changed tasks are `Proposed`. Never change `Done` tasks; propose follow-ups instead.
6. Record a new design baseline (date and commit) and update "Now", report, and stop for approval.
