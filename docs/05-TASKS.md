# 05. Task Backlog and Progress

> **Ownership:** Shared by user and Claude Code. Track only approved implementation work and keep status truthful.

## Status definitions

- **Proposed:** Suggested but not approved.
- **Approved:** User explicitly authorized the task.
- **In progress:** Implementation has started.
- **Blocked:** Work cannot safely continue; reason is recorded.
- **Review needed:** Implementation is ready for review.
- **Done:** Acceptance criteria and required checks are satisfied.
- **Deferred:** User chose to postpone the task.

## Task list

| ID | Task | Priority | Status | Dependencies | Acceptance criteria |
|---|---|---|---|---|---|
| TASK-001 | | [ ] Must [ ] Should [ ] Could | Proposed | | |
| TASK-002 | | [ ] Must [ ] Should [ ] Could | Proposed | | |
| TASK-003 | | [ ] Must [ ] Should [ ] Could | Proposed | | |

## Active task detail

Copy this section for an active task when more detail is useful.

### TASK-XXX: Task title

- **Status:**
- **Approved by / date:**
- **Related requirement(s):**
- **Scope:**
- **Out of scope:**
- **Dependencies:**

#### Acceptance criteria
- [ ]
- [ ]
- [ ]

#### Implementation notes
_Write here:_

#### Verification

| Check | Command / method | Result | Evidence / notes |
|---|---|---|---|
| | | [ ] Pass [ ] Fail [ ] Not run | |

#### Progress log

| Date | Update |
|---|---|
| | |

#### Review and closure
- **Review status:** [ ] Not reviewed [ ] Findings open [ ] Accepted
- **Known limitations:**
- **Completed date:**

## Rules

- Only user-approved tasks may be marked `Approved` or `In progress`.
- Claude may propose tasks, but must not approve them.
- Implement one task at a time unless the user explicitly approves a batch.
- Keep task scope and acceptance criteria specific.
- Do not mark a task `Done` if required tests were not run, acceptance criteria are unmet, or unresolved blockers remain.
- Record deferred work rather than silently expanding the current task.
