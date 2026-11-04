# 00. Requirements Intake

> **Owner:** User / project director. **Purpose:** Raw input gathered in the requirements round (interview, stakeholder call, brief), captured before Part A is filled. **Editing rule:** Claude treats this file as read-only unless explicitly asked to edit it.
>
> **Two parts:** **Part 1, Requirements** holds what the interviewer or stakeholder told you. **Part 2, Systems Design** holds your own design calls on the same topics. If you're unsure where something goes, put it in Part 1.
>
> **How to fill:** Answer during the requirements round. Pasting from a spreadsheet is fine; tab-separated text or bullets are read the same as a table. An item's text is only a prompt: tools named in it (for example Presidio) are not choices until the **Answer / Notes** column says so.
> **Priority:** `Must` · `Should` · `Later` (record, don't build now) · `N/A`
>
> **How Claude uses it:** Part A and the design documents (`01` to `03`) are your curated design and win on conflict. Claude raises a conflict on a `Must` item, and a `Must` item that Part A and the plan don't cover. A blank Part B field takes the intake answer here before falling back to `Claude proposes`. **Maps to** shows the template section each answer feeds; Claude maps a row whose **Maps to** is blank.

## Adding inputs not listed here

- **Fits an existing section:** add a row at the end of that section with the next number (for example `R-C7`). Leave **Maps to** blank.
- **Fits no section** (a hint, an evaluation criterion, a constraint, an open question): add it to **Additional inputs** at the end.
- **Wording matters:** quote the interviewer verbatim in **Answer / Notes**.
- **IDs are permanent.** The plan cites them. Don't renumber; to drop a row, set its Priority to `N/A`.
- **After `START`:** edit this file, then say `REPLAN`.

---

# Part 1: Requirements

## A. Business problem

| # | Item | Answer / Notes | Priority | Maps to |
|---|---|---|---|---|
| R-A1 | Target persona and pain points | | | 01 §2, §3, §10 |
| R-A2 | Core user journey | | | 01 §4 |
| R-A3 | Success measure: outcome completion | | | 01 §1, §9; 03 §22 |
| R-A4 | Success measure: answer safety / quality | | | 01 §1, §9; 03 §22 |
| R-A5 | Success measure: tool-call accuracy | | | 01 §9; 03 §22 |
| R-A6 | Assumption: types of inputs | | | 03 §1; 01 §15 |
| R-A7 | Assumption: operating constraints | | | 01 §8 |
| R-A8 | Assumption: risky actions to be controlled | | | 01 §7; 03 §5, §7, §18 |

## B. Architecture requirements

| # | Item | Answer / Notes | Priority | Maps to |
|---|---|---|---|---|
| R-B1 | RAG / tools: real or mocked? | | | 02 §5; 03 §5, §14 |

## C. Agent requirements

| # | Item | Answer / Notes | Priority | Maps to |
|---|---|---|---|---|
| R-C1 | Chat horizon / long chats | | | 03 §15 |
| R-C2 | System agency: autonomous vs. human-in-the-loop conditions | | | 03 §4, §5, §18 |
| R-C3 | Model preference: third-party (OpenAI, Anthropic) | | | 02 §3; 03 §12 |
| R-C4 | Model preference: self-hosted / local | | | 02 §3; 03 §12 |
| R-C5 | Specialist agents in future? | | | 03 §3, §8 |
| R-C6 | Router scope: cheap front model + few heavyweight specialist models | | | 03 §9, §12 |

## E. Persistent storage

| # | Item | Answer / Notes | Priority | Maps to |
|---|---|---|---|---|
| R-E1 | Data / chats collected for evaluations or post-training | | | 01 §13; 03 §15 |

## F. Middleware

| # | Item | Answer / Notes | Priority | Maps to |
|---|---|---|---|---|
| R-F1 | Batching / out-of-scope requests | | | 01 §6; 02 §6, §13 |

## G. Metrics

| # | Item | Answer / Notes | Priority | Maps to |
|---|---|---|---|---|
| R-G1 | Offline evaluations: golden dataset | | | 03 §22 |

## H. Demo

| # | Item | Answer / Notes | Priority | Maps to |
|---|---|---|---|---|
| R-H1 | Run / deploy: Streamlit, local | | | 02 §3, §14 |

---

# Part 2: Systems Design

## B. Architecture requirements

| # | Item | Answer / Notes | Priority | Maps to |
|---|---|---|---|---|
| S-B1 | Tenant isolation | | | 02 §4, §11 |
| S-B2 | API versioning | | | 02 §9 |

## C. Agent requirements

| # | Item | Answer / Notes | Priority | Maps to |
|---|---|---|---|---|
| S-C1 | Level of determinism / temperature | | | 03 §12 |
| S-C2 | Semantic caching | | | 02 §10; 03 §12 |
| S-C3 | Guardrail: PII (module: Presidio) | | | 03 §19 |
| S-C4 | Guardrail: prompt injection (local lightweight model) | | | 03 §19 |
| S-C5 | Guardrail: content safety (module: Detoxify) | | | 03 §19 |
| S-C6 | Guardrail: token limit | | | 03 §6 |
| S-C7 | Guardrail: input content filters | | | 03 §7, §19 |
| S-C8 | Guardrail: hallucination check | | | 03 §19, §22 |
| S-C9 | Agent constraint K, what to know: hybrid RAG | | | 03 §14 |
| S-C10 | Agent constraint A, how to act: APIs, permissions, trust, containment, failure handling | | | 03 §5, §13, §19, §20 |
| S-C11 | Agent constraint R, what to remember: chat, semantic, episodic, procedural memory | | | 03 §15 |
| S-C12 | Agent constraint C, how to coordinate: shallow, ReAct loop, router, DAG | | | 03 §3, §9, §11 |
| S-C13 | Shared state specification | | | 03 §9, §10, §16 |

## D. Software requirements

| # | Item | Answer / Notes | Priority | Maps to |
|---|---|---|---|---|
| S-D1 | Target latency / throughput | | | 02 §18; 03 §23 |
| S-D2 | Scaling: horizontal? | | | 02 §18 |

## E. Persistent storage

| # | Item | Answer / Notes | Priority | Maps to |
|---|---|---|---|---|
| S-E1 | Resumable chats: conversation history | | | 03 §15 |
| S-E2 | Resumable chats: in-session state | | | 03 §16 |
| S-E3 | Resumable chats: episodic long-term summary | | | 03 §15 |
| S-E4 | Data model specification | | | 01 §13; 02 §10 |
| S-E5 | Data retention policy | | | 01 §13; 02 §15; 03 §15 |

## F. Middleware

| # | Item | Answer / Notes | Priority | Maps to |
|---|---|---|---|---|
| S-F1 | Cache with TTL | | | 02 §10 |
| S-F2 | Authentication / authorization APIs, RBAC | | | 02 §4, §11 |
| S-F3 | Tool-call failures: retries with exponential backoff | | | 03 §13, §20 |
| S-F4 | Tool-call failures: idempotency | | | 02 §13; 03 §13 |
| S-F5 | Rate limit | | | 02 §9; 03 §23 |
| S-F6 | Circuit breaker | | | 03 §20 |

## G. Metrics

| # | Item | Answer / Notes | Priority | Maps to |
|---|---|---|---|---|
| S-G1 | Observability / tracing: prompts, agent calls and cost, tool calls | | | 02 §16 |
| S-G2 | Offline evaluations: LLM as judge | | | 03 §22 |
| S-G3 | Software metrics: CPU, memory, disk | | | 02 §16 |
| S-G4 | Tests: unit, agent, retrieval, tool-call | | | 02 §17; 03 §22 |

## H. Demo

| # | Item | Answer / Notes | Priority | Maps to |
|---|---|---|---|---|
| S-H1 | Which of these components to include in the demo | | | 01 §6, §9; 03 §8 |

---

# Additional inputs

Anything else from the requirements round that fits no row above: hints, evaluation criteria, constraints, open questions. Leave **Maps to** blank if unsure.

| # | Input | Answer / Notes | Priority | Maps to |
|---|---|---|---|---|
| X1 | | | | |
