# 01. Project Definition

> **Owner:** User / project director. **Purpose:** Define what is being built and why. **Editing rule:** Claude treats this file as read-only unless explicitly asked to edit it.
>
> **How to fill:** Complete Part A first. Aim for 15–20 minutes across Part A of `01`, `02`, and `03` together, then say `START`. Refine Part B in later iterations and say `REPLAN`.
> **Values:** `[x]` selected · blank = unknown · `Claude proposes` = delegated to the plan · `N/A` = not applicable · `Later` = deferred.

---

# Part A: Essentials

## 1. Snapshot

- **Project name:**
- **One-line description:**
- **Delivery profile (one):** [ ] Prototype [ ] MVP [ ] Production candidate. See `instructions/00-STANDARDS.md`.
- **Timebox / deadline:**
- **Primary success measure:**

## 2. Problem

In 2–4 sentences: the problem, who has it, and why it matters.

_Write here:_

## 3. Users

| User type / role | Goal | Access or restrictions |
|---|---|---|
| | | |
| | | |

## 4. Core user journey

The single most important journey, as numbered steps from start to useful outcome. Include what the user sees and the main failure path.

1.
2.
3.

## 5. Must-have requirements

Observable, testable behaviors required for this delivery.

| ID | Requirement / behavior | Acceptance condition |
|---|---|---|
| FR-001 | | |
| FR-002 | | |
| FR-003 | | |

## 6. Explicitly out of scope

-
-

## 7. Business rules

Rules that cannot be inferred from generic practice: eligibility, approvals, calculations, workflow conditions, data visibility, domain constraints.

-
-

## 8. Hard constraints

Mandated technologies, allowed services, budget, deployment restrictions, team size, other hard limits.

-

## 9. Project-specific acceptance criteria

These are in addition to the default criteria at the end of this file.

-
-

**Part A ready for planning:** [ ]

---

# Part B: Detail (fill when relevant; blank fields use `00-REQUIREMENTS.md` answers, otherwise `Claude proposes`)

## 10. Context

How the problem is handled today and what is slow, difficult, expensive, unreliable, or missing.

_Write here:_

## 11. Additional journeys

| Journey | Priority | Brief description |
|---|---|---|
| | [ ] Must [ ] Later | |

## 12. Further requirements

| ID | Requirement / behavior | Priority | Acceptance condition |
|---|---|---|---|
| FR-101 | | [ ] Should [ ] Could | |

## 13. Data and information

| Information / entity | What it represents | Source | Sensitivity / access notes |
|---|---|---|---|
| | | | |

- **Existing data to import or migrate:**
- **Data retention / deletion requirements:**
- **Data quality constraints:**

## 14. Non-functional expectations

- **Availability (one):** [ ] Best effort / demo [ ] Business hours [ ] High availability [ ] Other:
- **Performance (one):** [ ] Normal interactive [ ] Low latency [ ] High throughput [ ] Other:
- **Scale (one):** [ ] Single user [ ] Small team [ ] Many users / multi-tenant [ ] Other:
- **Accessibility (one):** [ ] Basic [ ] Named standard: [ ] Not in scope
- **Auditability (one):** [ ] Basic logs [ ] Traceable user actions [ ] Formal audit trail [ ] Other:
- **Privacy / compliance needs:**
- **Other quality requirements:**

## 15. Assumptions to validate

-

## 16. Open questions

| Question | Why it matters | Status |
|---|---|---|
| | | [ ] Open [ ] Resolved |

---

## Default acceptance criteria

These apply to every project unless you remove them. `CLOSE PROJECT` verifies them against the delivery profile.

- The core user journey works end to end.
- Must-have requirements are met, or explicitly deferred by the user.
- Critical failure paths are tested.
- Required permissions and data boundaries work as designed.
- Automated tests required by the delivery profile pass.
- The user has completed manual testing.
- Known limitations and unfinished work are documented.
- Run and demo instructions are usable.
