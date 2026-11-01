# 05. Current State, Tasks, and Feedback

> **Ownership:** Shared by the user and Claude Code. Keep every status truthful. Claude reads "Current state" at the start of every session.

## Current state

- **Phase:** [ ] Design [ ] Planning [ ] Implementing [ ] Reviewing [ ] Closing
- **Plan version and status:**
- **Active task(s):**
- **Last accepted commit:**
- **Waiting on:** _For example: user approval of plan v1, review of TASK-002._
- **Next step:**

## Status definitions

- **Proposed:** Suggested by Claude; not approved.
- **Approved:** The user explicitly authorized it; the approval is recorded.
- **In progress:** Implementation has started.
- **Blocked:** Cannot safely continue; the reason is recorded.
- **Review needed:** Implemented and verified by Claude; waiting for review and acceptance.
- **Done:** The user accepted it and the change is committed.
- **Deferred:** The user postponed it.

## Task list

| ID | Task | Milestone | Requirement(s) | Status | Depends on | Acceptance criteria | Approval |
|---|---|---|---|---|---|---|---|
| TASK-001 | | M1 | | Proposed | | | |
| TASK-002 | | M1 | | Proposed | | | |

The **Approval** column holds `Approved (chat, YYYY-MM-DD): <summary>` once the user approves the plan, the task, or the fix. Claude fills it only from an explicit user approval.

### Verification notes

Record checks per task. For the Prototype profile, one line per task is enough.

| Task | Check | Command / method | Result | Notes |
|---|---|---|---|---|
| | | | Pass / Fail / Not run | |

## Feedback log

| ID | Date | Observation (summary) | Type | Proposed correction | Related task | Status | Approval |
|---|---|---|---|---|---|---|---|
| FB-001 | | | | | | Proposed | |

**Type:** Bug · Missing requirement · Usability · Performance / reliability · Design change · New scope
**Status:** Proposed · Approved · Rejected · Fixed · Deferred

## Task detail (Production candidate, or when useful)

Copy for a task that needs more than a table row.

### TASK-XXX: Title

- **Scope / out of scope:**
- **Related requirement(s) and design sections:**
- **Implementation notes:**
- **Known limitations:**
- **Progress log:**

## Rules

- Claude may propose tasks and fixes but never approves them.
- Implement one task at a time unless the user approves a batch.
- Keep scope and acceptance criteria specific. Record new work as a proposed task or a feedback item rather than expanding the current task.
- Mark `Done` only after the user accepts the task and the change is committed. Never mark `Done` while required checks were not run, acceptance criteria are unmet, or blockers remain.
- Update "Current state" whenever the phase, active task, or next step changes.
