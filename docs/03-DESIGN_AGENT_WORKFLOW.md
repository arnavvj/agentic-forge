# 03. Agent and Agentic Workflow Design

> **Owner:** User / project director. **Purpose:** Define what the agentic system does, how it is structured, and the boundaries under which it operates. Supports single-agent, multi-agent, and hybrid systems. **Editing rule:** Claude must treat this file as read-only unless explicitly asked to edit it.

Complete applicable sections. Sections marked **Multi-agent / Hybrid** are required only when that architecture is selected. Do not add agents or frameworks merely because they are available.

## 1. Agentic system purpose

- **Purpose and desired outcome:** What should the system accomplish for the user?
- **Trigger / entry point:** [ ] User chat [ ] API request [ ] Scheduled trigger [ ] Event / webhook [ ] Internal workflow [ ] Other:
- **Who or what can trigger it?**
- **Input received:**
- **Expected output or action:**

_Write the intended behavior and outcome here:_

## 2. Agent architecture type

Select one:
- [ ] Single-agent
- [ ] Multi-agent
- [ ] Hybrid (some tasks use one agent, other tasks use multiple agents)
- [ ] Other:

**Why this structure is appropriate:**

## 3. Agent inventory

**Multi-agent / Hybrid:** Define each agent and its boundary. For a single-agent system, use one row or mark this section not applicable.

| Agent name / ID | Responsibility | Inputs | Outputs | Permitted tools / actions | Model or model profile |
|---|---|---|---|---|---|
| | | | | | |
| | | | | | |
| | | | | | |

For each agent, clarify its responsibilities, what is outside its scope, whether it recommends or acts, and when it may hand off or finish.

## 4. Multi-agent topology

**Multi-agent / Hybrid:** Select the intended coordination structure.
- [ ] Supervisor / worker: one coordinator assigns work to specialist agents.
- [ ] Hierarchical: coordinators may delegate to other coordinators or specialists.
- [ ] Sequential pipeline: agents work in a defined order.
- [ ] Parallel: independent agents work simultaneously and results are combined.
- [ ] Collaborative: agents exchange information over multiple turns.
- [ ] Router-based: a router selects the relevant specialist.
- [ ] Dynamic delegation: agents may select or create additional work within explicit limits.
- [ ] Other:

**Describe the flow, including branch and handoff conditions:**

_Write here:_

### Agent interaction map

```text
Describe the agent-to-agent flow here, or add a Mermaid diagram.
Include the entry point, routing / coordinator, agents, handoffs,
aggregation, and final response or action.
```

## 5. Coordination and shared context

**Multi-agent / Hybrid:**

### Coordination method
- [ ] Direct handoff
- [ ] Shared workflow state
- [ ] Message passing
- [ ] Event-driven coordination
- [ ] Shared task queue
- [ ] Other:

### Shared context scope
- [ ] No shared context
- [ ] Conversation-level context
- [ ] Task-level context
- [ ] Shared memory / knowledge
- [ ] Other:

### Result aggregation
- [ ] Supervisor synthesis
- [ ] Sequential output passed to next agent
- [ ] Parallel result merge
- [ ] Voting / consensus
- [ ] Rule-based selection
- [ ] Human selection / approval
- [ ] Custom:

**What information must be passed between agents? What must not be shared?**

_Write here:_

## 6. Agent planning and execution

- **Execution style:** [ ] Fixed workflow [ ] Dynamic planning [ ] ReAct / tool-use loop [ ] Hybrid [ ] Other:
- **Planning:** [ ] No explicit planner [ ] Single agent plans [ ] Dedicated planner [ ] Supervisor plans [ ] Other:
- **Task decomposition:** [ ] Not needed [ ] Fixed steps [ ] Dynamic subtasks [ ] Other:
- **Execution order:** [ ] Sequential [ ] Parallel [ ] Conditional [ ] Mixed
- **Dynamic agent creation:** [ ] Not allowed [ ] Allowed within limits [ ] Other:
- **Maximum delegation depth:**
- **Maximum agents per task:**
- **Stop / completion conditions:**

## 7. Model strategy and mapping

- **Model provider(s):** [ ] OpenAI [ ] Anthropic [ ] Google [ ] Azure-hosted models [ ] Local / self-hosted [ ] Multiple providers [ ] Other:
- **Initial model strategy:** [ ] One model for all agents [ ] Model per role [ ] Model chosen by task [ ] Other:
- **Model selection / routing policy:**
- **Fallback model or behavior:**
- **Required capabilities:** [ ] Tool calling [ ] Structured output [ ] Vision [ ] Audio [ ] Long context [ ] Other:

| Agent / role | Model or model profile | Reason | Fallback |
|---|---|---|---|
| | | | |
| | | | |

Model choice may be configuration-driven, but the application must enforce permissions and resource limits independently of model choice.

## 8. Tools and external actions

| Tool / capability | Purpose | Available to which agent(s)? | Read / write / consequential? | Approval required? |
|---|---|---|---|---|
| | | | | |
| | | | | |

- **Tool interface:** [ ] Internal functions [ ] API / SDK [ ] MCP [ ] Workflow activities [ ] Other:
- **MCP servers / tools, if any:**
- **Tool input validation:**
- **Tool output validation:**
- **Timeout and retry behavior:**
- **Idempotency / duplicate action prevention:**
- **External actions that must never happen without human approval:**

## 9. Retrieval and knowledge (RAG)

- **Retrieval required:** [ ] No [ ] Yes [ ] Under consideration
- **Knowledge sources:** [ ] Documents [ ] Database [ ] Search index [ ] APIs [ ] User-provided files [ ] Other:
- **Retrieval method:** [ ] Keyword [ ] Semantic / vector [ ] Hybrid [ ] Structured queries [ ] Other:
- **Ingestion / update approach:**
- **Chunking / metadata needs:**
- **Source attribution / citations required:** [ ] Yes [ ] No [ ] Depends
- **Access control during retrieval:**
- **Behavior when relevant information is not found:**

## 10. Memory and context management

- **Conversation history:** [ ] None [ ] Current session [ ] Persistent
- **Working memory:** [ ] None [ ] Per request [ ] Per task / workflow
- **Long-term memory:** [ ] None [ ] User-specific [ ] Shared / organizational [ ] Other:
- **Memory store / mechanism:**
- **What may be stored:**
- **What must not be stored:**
- **Retention, correction, and deletion behavior:**
- **Context window / summarization strategy:**
- **How context is passed between agents:**

Keep conversational context, retrieved knowledge, agent working state, and durable workflow state distinct where required.

## 11. Workflow durability and execution lifecycle

- **Execution duration:** [ ] Short request [ ] Streaming interaction [ ] Long-running job [ ] Human-waiting workflow [ ] Mixed
- **Orchestration framework:** [ ] LangGraph [ ] Custom state machine [ ] Framework-native agent loop [ ] Other:
- **Durable workflow engine:** [ ] Not needed [ ] Temporal [ ] Inngest [ ] Trigger.dev [ ] Cloud workflow service [ ] Other:
- **Queue / worker approach:** [ ] Not needed [ ] Framework-native [ ] Managed queue [ ] Redis-backed [ ] Other:
- **State persistence:** [ ] In-memory only [ ] Persist task state [ ] Durable checkpoints [ ] Full execution history [ ] Other:
- **Resume after interruption:** [ ] Not needed [ ] Required [ ] Depends on workflow
- **Retries / timeouts / cancellation:**
- **Duplicate execution prevention / idempotency:**
- **Human wait states / timers:**

**Ownership boundary:** An agent graph or state machine governs agent steps and transitions. A durable workflow engine, when used, governs job lifecycle, workers, retries, timers, waiting, cancellation, and recovery. Do not add both layers unless their responsibilities are justified.

## 12. Streaming and user interaction

- **Response mode:** [ ] Standard request / response [ ] Token streaming [ ] Progress events [ ] Background status updates [ ] Mixed
- **Streaming mechanism:** [ ] SSE [ ] WebSockets [ ] Polling [ ] Other:
- **Progress visibility:**
- **Pause / cancel / resume controls:**
- **Reconnect / resume behavior:**
- **What users see when a workflow is running or fails:**

## 13. Human-in-the-loop (HITL)

- **Human involvement:** [ ] Not required [ ] Review output [ ] Approve tool action [ ] Supply missing information [ ] Resolve exception [ ] Other:
- **Approval triggers:**
- **Who may approve:**
- **What information is shown to the approver:**
- **Reject / edit / timeout behavior:**
- **What happens after approval or rejection:**

## 14. Agent permissions, boundaries, and safety

Define permissions for each agent and consequential tool. Do not rely on prompts alone to enforce access.

| Agent / role | Data it may access | Tools / actions it may use | Restricted actions | Human approval needed for |
|---|---|---|---|---|
| | | | | |
| | | | | |

- **Authorization enforcement point:** [ ] Backend service [ ] Tool gateway [ ] Policy layer [ ] Other:
- **Are permissions checked on every tool / action call?**
- **Can an agent delegate? If yes, to whom and within what limits?**
- **Delegation rule:** Delegation must not silently grant the receiving agent new permissions.
- **Handling of untrusted user input and retrieved content:**
- **Prompt injection / malicious tool output handling:**
- **Sensitive data handling:**
- **Refusal / escalation conditions:**
- **Actions that are prohibited:**

## 15. Multi-agent failure handling

**Multi-agent / Hybrid:**
- **Agent timeout behavior:**
- **Retry policy and maximum attempts:**
- **Fallback when a specialist is unavailable:**
- **Partial result behavior:**
- **Conflicting agent result behavior:**
- **Duplicate task / action prevention:**
- **Maximum delegation depth and total agent budget:**
- **Cancellation propagation:**
- **Human escalation conditions:**

## 16. Evaluation and quality

- **Evaluation approach:** [ ] Manual tests [ ] Curated test cases [ ] Automated evaluations [ ] Online monitoring [ ] Other:
- **Expected answer / action quality:**
- **Grounding / citation expectations:**
- **Tool selection and argument correctness:**
- **Failure and refusal behavior:**
- **Regression test cases:**
- **Evaluation dataset / source:**

**Multi-agent / Hybrid:** include checks for:
- [ ] Individual agent quality
- [ ] Routing accuracy
- [ ] Handoff correctness
- [ ] Context transfer and missing information
- [ ] Result aggregation quality
- [ ] Conflicting or duplicate actions
- [ ] End-to-end task completion
- [ ] Latency and cost across the full agent group

## 17. Cost and performance budgets

- **Maximum task duration:**
- **Target response latency:**
- **Maximum model calls per task:**
- **Token / context budget:**
- **Cost budget per task or user:**
- **Maximum parallel agents:**
- **Rate limits / concurrency limits:**
- **Behavior when a budget is reached:**

## 18. MVP agentic scope

### Required for MVP
- [ ]
- [ ]
- [ ]

### Deferred until later
- [ ]
- [ ]
- [ ]

### Explicitly not allowed
- [ ]
- [ ]
- [ ]

---

**Director sign-off:** [ ] This agent workflow design is ready for planning.

Agent frameworks and model providers are options, not mandatory defaults. The approved behavior and trust boundaries take priority over framework convenience.
