# 06. Decision Log

> **Ownership:** Shared record. The user is the final decision maker. Record material product, architecture, data, security, agent, and scope decisions.
>
> An approved decision supersedes the design documents (`docs/01` to `docs/03`) on the specific point it covers. The user may update the design document later to match.

## Decision register

For the Prototype profile, a register row is a complete record. For MVP and Production candidate, see `instructions/00-STANDARDS.md` for which decisions need a full record.

| ID | Date | Decision | Area | Status | Supersedes (design section or ADR) | Approval |
|---|---|---|---|---|---|---|
| ADR-001 | | | | Proposed | | |

**Area:** Product · Architecture · Data · Security · Agent workflow · Infrastructure · Scope · Other
**Status:** Proposed · Approved · Rejected · Superseded

The **Approval** column holds `Approved (chat, YYYY-MM-DD): <summary of the user's message>`. Claude fills it only from an explicit user approval.

## Full decision record

Copy for each decision that needs one.

### ADR-XXX: Title

- **Date / raised by / area:**
- **Related requirement, task, or design section:**
- **Context:** What problem or trade-off requires a decision?
- **Options considered:**

| Option | Benefits | Costs / risks |
|---|---|---|
| | | |

- **Recommendation:**
- **Final decision and rationale:**
- **Consequences and follow-up:**
- **Approval:**

## Changing a decision

Do not overwrite an approved decision. Mark it `Superseded` and add a new decision that explains what changed and why.
