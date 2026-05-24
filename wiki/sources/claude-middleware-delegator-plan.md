---
type: source-summary
raw: raw/llm/2026-04-22-claude-middleware-delegator-plan.md
source: claude
date: 2026-04-22
---

# Middleware Delegator Implementation Plan

## Key Claims

- Stateless FastAPI daemon: POST /ingest (202 async), GET /query (FTS5 BM25), between any LLM client and wiki store.
- Ingest: validate → Ollama summarize → raw JSON → wiki page → SQLite → index.md/log.md.
- Query: tokenize → FTS5 → load snippets → ranked JSON; optional ?summarize=true.
- Stack: Python 3.12, Ollama glm-4.7-flash, SQLite FTS5, Obsidian-compatible Markdown.
- Dual persistence: structured SQLite + human-readable vault.
- Background asyncio queue — caller unblocked at validation.

## Unique Insights

- No LLM in default query path — fast, deterministic, token-free retrieval.
- Detailed API contract with Pydantic schema for generic Q+A JSON.

## Contradictions

Wiki folder layout differs from Karpathy sources/concepts split — see [[mem-weaver-architecture]].

## Related sources

[[claude-second-brain-implementation]], [[claude-architecture-inspiration]], [[mem-weaver-architecture]]

Related concepts: [[mem-weaver-architecture]] [[implementation-milestones]]
