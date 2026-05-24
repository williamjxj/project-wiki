---
type: concept
sources:
  - claude-fastapi-skeleton-design
  - claude-fastapi-skeleton-plan
  - claude-milestone-b-typed-models-design
  - claude-milestone-b-typed-models-plan
  - claude-phase-4-hardening-plan
  - claude-chat-app-frontend-design
  - claude-mcp-server-design
  - claude-mcp-server-plan
  - claude-frontend-admin-integration
last_updated: 2026-05-24
---

# Implementation Milestones

## Consensus

Incremental delivery via thin vertical slices:

| Milestone | Scope | Key deliverables | Status |
|-----------|-------|------------------|--------|
| **A — Skeleton** | Contract-first stubs | `POST /ingest` (202), `GET /query`, `GET /health` | Done |
| **B — Typed models** | Pydantic v2 + pydantic-settings | Same HTTP contracts; permissive ingest JSON | Done |
| **Phase 4 — Hardening** | Production guardrails | Contradiction check, wikilink graph, stats, DLQ, pytest ([[claude-phase-4-hardening-plan]]) | Done |
| **Chat frontend** | Second brain loop | Next.js 14 + SSE `/chat`; classifier, retriever, WikiSidebar | Backend done; frontend per [[claude-chat-app-frontend-design]] |
| **MCP server** | IDE integration | stdio FastMCP; 4 tools via shared `memory_api` ([[claude-mcp-server-design]], [[claude-mcp-server-plan]]) | Done |
| **Admin UX** | Wiki editing | Obsidian vault + optional Next admin | Design in [[claude-frontend-admin-integration]] |

## Divergence

| Priority | [[chatgpt-mem-weaver-v2-roadmap]] | [[claude-mcp-server-design]] |
|----------|-----------------------------------|------------------------------|
| Next build | P0: `POST /chat` + taxonomy | MCP as high ROI for agent ecosystem |
| Frontend | P1: Next.js chat UI | IDE is the LLM — omit `/chat` from MCP |

## Decision

Both **POST /chat** (human chat loop) and **MCP server** (IDE agent loop) are valid entry points sharing [[mem-weaver-architecture]] service layer — **both backends exist**. Next priority: Next.js chat UI ([[claude-chat-app-frontend-design]]) or polish MCP config; value gate + `_index.md` alignment remain cross-cutting.

Related: [[mem-weaver-architecture]], [[mem-weaver-as-built-status]], [[claude-frontend-admin-integration]]
