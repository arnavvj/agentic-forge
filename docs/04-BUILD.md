# 04. Build: Plan, Tasks, Decisions

> **Owner:** Shared. Claude writes and maintains this file. You may edit any part directly (answer a decision, reorder or defer a task, change a choice); Claude re-reads it at every command and follows your edits. One line per item.

## Now

- **Phase:** Planning · Implementing · Reviewing · Closing
- **Plan:** v1 · Proposed / Approved
- **Doing:**
- **Waiting on:**
- **Next:**
- **Last accepted commit:**
- **Design baseline:** _date, plus commit of `docs/00` to `docs/03`_

---

## 1. Plan

**Outcome:** _the working result this plan delivers, in one or two sentences._

**Plan approval:** _Not approved._

### Decisions needed

Blocking items. Answer in the last column ("accept" takes the recommendation), or in chat. Resolved rows move to section 4.

| # | Question | Options | Recommendation | Your answer |
|---|---|---|---|---|
| D1 | | | | |

### Build scope

Every component in the `docs/02` and `docs/03` diagrams.

| Component | Diagram | Scope | Source |
|---|---|---|---|
| | 02 / 03 | Build · Mock · Provided · Later · Out of scope | Design · Intake row · Claude proposes |

### Choices and assumptions

Approved with the plan unless you change them. Edit the Choice cell to override.

| Area | Choice | Source | Reason |
|---|---|---|---|
| | | Claude proposes · Intake row · Default · Assumption | |

### Milestones

| Milestone | Outcome | Tasks |
|---|---|---|
| M1 | Core journey end to end (thin slice) | |
| M2 | | |

**Top risks:**

---

## 2. Tasks

| ID | Task (requirements) | M | Depends | Acceptance criteria (one line) | Status | Checks run | Approval |
|---|---|---|---|---|---|---|---|
| TASK-001 | | M1 | | | | | |

**Status:** Proposed · Approved · In progress · Blocked · Review needed · Done · Deferred. `Done` means accepted and committed. **Checks run:** command and result, or `Not run`.

## 3. Feedback

| ID | Observation | Type | Proposed fix | Status | Approval |
|---|---|---|---|---|---|
| FB-001 | | | | | |

**Type:** Bug · Missing requirement · Usability · Reliability · Design change · New scope. **Status:** Proposed · Approved · Rejected · Fixed · Deferred.

## 4. Decisions

Approved decisions supersede the intake and design documents on the point they cover.

| ID | Date | Decision and reason | Supersedes | Status | Approval |
|---|---|---|---|---|---|
| ADR-001 | | | | | |

**Status:** Proposed · Approved · Rejected · Superseded. Never overwrite an approved decision: mark it `Superseded` and add a new one. Where the profile needs a full record, add a short subsection below the table: context, options, decision, consequences.

---

**Approval cells:** `Approved (chat, YYYY-MM-DD): <summary>` when you approve in chat, or write `Approved (you, YYYY-MM-DD)` yourself in the file. A "Your answer" you write counts as your approval of that decision; Claude records it as `Approved (file, YYYY-MM-DD)`. Claude never writes an approval you did not give.
