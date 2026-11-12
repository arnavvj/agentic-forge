# agentic-forge

A lean harness for building a Python AI application with Claude Code and Codex in a timed coding round. You design; the assistants plan, build, and test from your notes.

## Contents

```text
AGENTS.md          Rules and workflow for both assistants (Codex reads it directly)
CLAUDE.md          One line, @AGENTS.md, so Claude Code reads the same rules
docs/DESIGN.md     Your design notes: graph, state, turn lifecycle, tools, schemas, APIs, scope, evals
docs/BUILD.md      Now, questions, choices, tasks with owners, decisions, issues
```

## Setup

Copy `AGENTS.md`, `CLAUDE.md`, and `docs/` into the working repo root. If the scaffold already has an `AGENTS.md` or `CLAUDE.md`, append ours to it. Commit, then open Claude Code and Codex from the repo root.

## Workflow

| When | You | Assistants |
|---|---|---|
| Design round | Prepare your notes (problem, graph, turn lifecycle, schemas, APIs, scope, evals). | — |
| First minutes of coding | Paste the notes into `docs/DESIGN.md`. Commit. Say `PLAN`. | Read the design and scaffold; fill `BUILD.md` with questions, choices, and tasks. |
| | Answer the questions (in chat or in `BUILD.md`). Set task owners. `GO 1`. | Phase 1: one full turn running end to end in `notebooks/01_turn.ipynb`, logic in `app/`. |
| Then | Run the notebook. `CHANGE: ...` for design changes. `CHECKPOINT`. `GO 2`. | Phase 2: API, persistence, multi-turn, tests. |
| If time | `GO 3`, `GO 4`. | Multi-user and hardening; demo and README. |

## Commands

| Say | Effect |
|---|---|
| `PLAN` | Read the design and repo, fill `BUILD.md`, stop. |
| `GO <task or phase>` | Build it. |
| `CHANGE: ...` | Update the design, log the decision, adjust tasks, report impact. |
| `STATUS` | Report "Now". |
| `CHECKPOINT` | Run the tests and commit. |

## Using two assistants

- Give each a separate area in `BUILD.md`'s Owner column, for example Claude on the graph and nodes, Codex on persistence and the API.
- Both read the same `AGENTS.md`, `DESIGN.md`, and `BUILD.md`, so either can pick up from the other.
- `CHECKPOINT` between handovers so each starts from a clean commit.

## Keeping context small

- Start a fresh session (`/clear`) after each `CHECKPOINT`; the assistant resumes from "Now" in `BUILD.md`.
- Point at files and failing commands instead of pasting large output.
- Keep `DESIGN.md` to your notes; detail belongs in code.

## Observability

Tracing to a local Phoenix instance is on from the first notebook run, so every turn shows its node, model, and tool spans. In Phase 2 the traces go to your Phoenix server. A local Grafana dashboard (requests, latency, errors, linked to Phoenix by trace ID) is optional for the demo; mark it in `DESIGN.md` section 2.

## Diagrams

Draw the graph in `DESIGN.md` section 3 as Mermaid. In VS Code, install **Markdown Preview Mermaid Support** (`bierner.markdown-mermaid`) to preview it.
