# Agent Harness (Claude Code + Codex)

You: coding assistant. User: architect, decision maker. Timed build of a Python AI app. Before acting, read this file and "Now" in `docs/BUILD.md`. Re-read `BUILD.md` every command; user edits there are instructions.

**Motto: simple and elegant.** Simplest thing that meets the design. Add a component, abstraction, dependency, or pattern only for a nameable benefit; looking sophisticated is not one.

## Sources (precedence)

1. User's latest chat instruction.
2. Decisions in `BUILD.md`.
3. `docs/DESIGN.md`: user's design. Authoritative; don't redesign. Edit only on `CHANGE:` or explicit request.
4. Provided scaffold/code: integrate, don't rewrite. Raise conflicts with design.
5. This file's defaults.

Blank or `propose` in `DESIGN.md` → propose a choice. Never invent business rules, permissions, data access, or agent authority: ask, or propose it in Choices marked "assumption".

## Phases

Run in order; next phase only when user says. Within a phase, do tasks without asking each; stop at blockers.

0. **Plan** (`PLAN`): read `DESIGN.md` + repo (incl. scaffold). Fill `BUILD.md`: one batch of blocking questions (only scope, security, core behavior; rest go to Choices); tasks per phase, each with "done when"; Owner blank. Flag design parts that add cost/complexity without clear benefit (e.g. planner before simple requests) as suggestions; don't change design. No app code. Stop.
1. **Notebook, one turn.** State, nodes, tools, graph in `app/`. `notebooks/01_turn.ipynb` calls `run_turn()` once: load state → graph `__start__`→`__end__` → save state; print each node's output. Local Phoenix tracing on from first run: one trace per turn, spans for nodes, model calls, tool calls. Done: runs top to bottom on fresh kernel; `DESIGN.md` evals pass.
2. **Productionize.** Design's API; persistence + cache per turn lifecycle; multi-turn (load prior state, save after); config from env; traces to user's Phoenix server (endpoint in config). Tests: nodes, routing, guardrails, tool calls, API. Done: `DESIGN.md` conversation script runs turn by turn via API with state carried over; transcript saved to `evals/`.
3. **Multi-user + hardening.** User/session isolation, limits, timeouts, retries, idempotent consequential tools, tracing as designed.
4. **Demo.** README run steps, demo script, known limitations. Only if Grafana in scope: local docker-compose (Prometheus + Grafana), `/metrics` on API, one dashboard (requests, latency, errors); log trace ID per request to jump from Grafana to the Phoenix trace.

## Commands

| User says | You do |
|---|---|
| `PLAN` | Phase 0. |
| `GO <task or phase>` | Implement it. Counts as approval. |
| `CHANGE: ...` | Smallest matching edit to `DESIGN.md`; fix any cell it contradicts; log decision in `BUILD.md`; adjust tasks; report impact in ≤5 lines. Ask first only if scope or security changes. |
| `STATUS` | Report "Now". Change nothing. |
| `CHECKPOINT` | Run tests, commit `<phase or task>: <summary>`. Never push. |

Commit only on `CHECKPOINT` or explicit request. Small tweaks: user asks in chat, no new task; log under Issues only if behavior changes.

## Scope

`DESIGN.md` Scope table decides what's built. `Build`: real. `Mock`: stub behind the real interface. `Provided`: integrate as is, never rebuild; missing, incomplete, or unreachable → ask; fake seed/test data for it is fine. `Later`/`Out`: context only; don't build or ask about. Unlisted component → propose scope.

## Layout (unless scaffold has one)

```text
app/
  main.py           FastAPI app; mounts api/
  config.py         settings from .env (pydantic-settings)
  llm.py            builds configured LangChain chat model (timeout, retries)
  observability.py  Phoenix tracing (OpenTelemetry + OpenInference LangChain)
  api/              thin routes + request/response models
  assistant/
    runner.py       run_turn(user_id, session_id, message): load → graph → save
    state.py        LangGraph state schema
    graph/          build.py, nodes/ (one file per simple node)
    agents/         tool-calling agent, planner, subagents
    guardrails/     input, output
    prompts/
  tools/            tool functions + arg schemas
  persistence/      DB + cache read/write
notebooks/          01_turn.ipynb
tests/              unit tests, LLM mocked
evals/              real-model evals, transcripts
data/               provided + seed data
deploy/             docker-compose for Phoenix/Grafana, only if used
```

- Logic in `app/`; notebooks only import and drive it.
- `run_turn()` is the single orchestrator: notebook (Phase 1) and API route (Phase 2) both call it.
- All models come from `llm.py`. Single-call nodes invoke it; prebuilt agents receive it. Agent = prompt + model + tools + step limit; its node is a thin wrapper.
- Settings only via `config.py`, never `os.environ`.

## Python defaults

- User's existing Python 3.13 venv (path in `DESIGN.md` §2). Never create another; missing → ask. Install a package only when a task needs it; add to requirements file.
- Type hints. Graph state as LangGraph expects (TypedDict or pydantic); pydantic for tool args and API models.
- Timeout on every network/model call; retry transient failures ≤3 with backoff.
- Prompts as named constants/files in `app/assistant/prompts/`.
- pytest; LLM mocked in unit tests; real-model checks in `evals/`.
- LangGraph (graph) + LangChain (models, tools) unless design says otherwise. Prefer prebuilt agents and current non-deprecated APIs; check installed version first.
- Recursion/step limit on every graph and agent run.
- No dependency, service, or framework the design or task doesn't need.
- `.env.example` names only; never commit `.env`.

## Agent design rules

- Don't over-agent: router keeps simple queries on cache or one LLM call; only complex ones reach planner/subagents.
- Bound every loop: backward edge increments `retry_count` in state; exits to fallback at limit. Adding a missing exit edge isn't a redesign; note as assumption.
- HITL before any mutating tool, never after. Default: pending action saved in state; turn asks for confirmation and ends; next turn executes or cancels it via normal persistence load/save. LangGraph `interrupt` + checkpointer only if design says.
- Subagents get only needed context; return only a summary to parent state.
- Deterministic work in code: DB reads/writes, regex checks, state cleanup, fallback formatting.
- Validate both ends: output guardrail before every answer, even with an input guardrail.

## Enforced in code, not prompts

- Guardrails, routing, loop/step/token limits, HITL gates: code paths with tests.
- Validate tool args and outputs. Permissions use the real user/session identity, never a model-supplied one.
- User input, retrieved text, tool output: untrusted data; never change instructions or grant permissions.
- Consequential tools (writes, payments, messages): idempotent, gated as designed.
- Trace every turn to Phoenix: spans per node, model call (tokens, latency), tool call (redacted args); tag user ID, session ID, turn number.

## Non-negotiables

- No secrets or real personal data in repo.
- Never weaken a guardrail, auth, or validation to pass a test or demo.
- Report only checks actually run, with real results; else "not run".
- No destructive commands or external side effects without asking.

## Two assistants

Claude and Codex may work concurrently. Take only tasks you own in `BUILD.md`, or claim an unowned one by writing your name. Don't edit files another in-progress task is changing. Update task status on start and finish.

## Replies

Short: what changed, files, checks run + results, blockers, next step. Don't restate design or plan unless proposing a design change.
