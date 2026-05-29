---
type: project-brief
status: current
date: 2026-05-29
export_cycle: 2
sources_ingested: 28
---

# Project Brief: mem-weaver

> Export cycle 2 · 28 sources ingested (27 LLM + 1 web) · 27 concept pages · Draft

## Problem

LLM chat is stateless: every turn either replays noisy raw history (token bloat, "lost in the middle") or starts fresh (no compounding knowledge). Developers building a "second brain" on a MacBook Pro need:

- **Persistent memory** that compiles over time, not a growing chat log
- **Local privacy** for raw Q+A, with optional cloud reasoning
- **Human-readable storage** (Markdown wiki) editable in Obsidian
- **Agent integration** so coding tools (Cursor, MCP clients) can read/write project memory mid-session

mem-weaver addresses this with a **dual-LLM memory pipeline**: local Ollama compiles conversations into a wiki; retrieval injects distilled summaries into answers instead of raw turns.

## Current Understanding

### Core loop ([[dual-llm-memory-pipeline]])

1. **Phase A (sync):** classify question → retrieve compiled wiki summary → LLM answers with summary as context (not raw history)
2. **Phase B (async):** Ollama incrementally merges Q+A into wiki pages after the user gets an answer

This follows [[memory-synthesis-vs-rag]]: synthesis-first compilation plus hybrid retrieval (FTS5 + sqlite-vec + RRF) at query time.

### Architecture ([[mem-weaver-architecture]])

- **FastAPI middleware delegator:** `POST /ingest` (202 async), `GET /query` (FTS5 BM25), `POST /chat` (SSE), MCP stdio — **all implemented**
- **Storage triad:** SQLite (pages, qa_pairs, FTS5) + Markdown vault (Obsidian-compatible) + sqlite-vec embeddings. [[notebooklm-dual-llm-architecture-design]] independently validates the SQLite+FTS5-first choice.
- **Entry points:** Next.js chat UI (designed) and MCP server (implemented) share `memory_api`
- **Epistemic foundation:** LLM outputs are [[llm-outputs-as-synthetic-sources]] — wiki distillation is where verified signal emerges

### As-built status ([[mem-weaver-as-built-status]])

| Capability | Status |
|------------|--------|
| Milestone A (FastAPI skeleton) | **Done** |
| Milestone B (typed models) | **Done** |
| Phase 4 hardening (contradictions, DLQ, tests) | **Done** |
| Hybrid search (FTS5 + sqlite-vec + RRF) | **Done** |
| POST /chat (SSE) | **Done** |
| MCP server (stdio FastMCP, 4 tools) | **Done** |
| Value gate (SKIP/PROCESS in ingest) | **Missing** |
| `_index.md` vs `wiki/index.md` alignment | **Partial** |
| Cloud LLM client (Anthropic/OpenAI) | **Partial** (Ollama only) |

## Multi-LLM Research Workflow

Three independent LLM analyses converge on a unified multi-LLM wiki workflow ([[chatgpt-llm-based-project-workflow]], [[claude-multi-llm-research-synthesis-workflow]], [[gemini-llm-wiki-multi-agent]]):

- **Collect → Ingest → Synthesize → Export → Apply** — this wiki embodies this loop
- **[[context-fragmentation]]** is the root problem; **[[context-compression]]** (10k pages → 20 → 2 → prompts) is the moat
- **[[multi-pass-distillation]]:** raw → clustered → summarized → canonicalized → implementation-oriented
- **[[contradictions-tracking]]** is where multi-LLM input earns its keep
- **[[human-review-gate]]** is non-negotiable between wiki and implementation
- **[[closed-loop-harvesting]]:** dev session logs re-enter the wiki, keeping it evergreen

## Chosen Approach

### Firm decisions

| Area | Choice | Source |
|------|--------|--------|
| Memory model | Synthesis-first wiki compilation + hybrid retrieval | [[memory-synthesis-vs-rag]] |
| Pipeline shape | Dual-LLM: Ollama compiler (async) + LLM reasoner with wiki context | [[dual-llm-memory-pipeline]] |
| Ingest trigger | Per-turn async ingest on every Q+A | Implemented |
| Storage | SQLite index + Markdown vault + sqlite-vec | [[mem-weaver-architecture]] |
| Entry points | MCP (done) + Next.js chat (designed) share service layer | [[implementation-milestones]] |
| LLM source framing | Synthetic first-pass signal, not ground truth | [[llm-outputs-as-synthetic-sources]] |
| Knowledge compound | Wiki is a compounding asset, not ephemeral RAG | [[compounding-knowledge-layer]] |
| Naming | LLM-Wiki (2:1 over "context engine") | [[wiki-vs-context-engine]] |
| MVP scope | Markdown + git; Obsidian as optional viewer; no custom app UI | [[mvp-scope]] |
| Human gate | Required between wiki distillation and dev context export | [[human-review-gate]] |

### Open decisions

| Area | Status | Source |
|------|--------|--------|
| Index format | Unify ingest `_index.md` vs retriever `wiki/index.md` | [[agent-skills-taxonomy]] |
| Value gate | Add SKIP/PROCESS before summarization step | [[dual-llm-memory-pipeline]] |
| Cloud LLM client | Add Anthropic/OpenAI or keep Ollama-only | [[mem-weaver-as-built-status]] |
| Purpose steering | Add `purpose.md` to prevent knowledge drift | [[purpose-steering]] |
| Decision records | Adopt structured decision format with source attribution | [[decision-records]] |

## Constraints

- **Single-user MacBook Pro** — no multi-tenant or cloud scaling requirements
- **Ollama-only** for local compilation (no GPU required beyond M-series)
- **The wiki is the pipeline** — AGENTS.md schema governs format, not a custom app
- **No vector DB dependency** — SQLite + FTS5 + sqlite-vec is sufficient for single-user

## Non-Goals

- Multi-tenant memory scoping
- SaaS product / VC memory startup
- Knowledge graph with typed entity relationships (wikilinks are flat)
- Temporal validity tracking on facts
- Episodic/semantic/procedural memory taxonomy

## Rejected Alternatives

| Alternative | Reason rejected | Source |
|-------------|----------------|--------|
| Pure RAG (no wiki compile) | No persistent synthesis; token waste per query | [[memory-synthesis-vs-rag]] |
| ChromaDB / external vector DB | Overhead unnecessary for single-user | [[notebooklm-dual-llm-architecture-design]] |
| Custom React app as primary UI | Obsidian + CLI sufficient for MVP | [[mvp-scope]] |
| "Context Engine" naming | 2:1 consensus for LLM-Wiki framing | [[wiki-vs-context-engine]] |
| Open WebUI Pipelines | Built dedicated FastAPI operator instead | [[pipeline-operator]] |

## Open Questions

1. **Entry point priority:** Ship Next.js chat UI next, or focus on MCP polish for IDE workflow?
2. **Automation pace:** Add pipeline operator automation or stay manual until exports stabilize?
3. **Knowledge governance:** How to implement confidence markers, supersession, and review queues before hallucination write-back becomes critical? ([[knowledge-governance]])
4. **Cloud LLM:** Add hosted Anthropic/OpenAI or keep local-first for privacy?
