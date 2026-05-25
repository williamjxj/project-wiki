---
type: concept
sources: [2026-05-25-cluade-pipeline-plan]
last_updated: 2026-05-25
---

# Pipeline Operator

## Consensus

A shared **pipeline core** should own ingest/lint/export/sync; UIs and MCP are thin adapters — validated by both Claude's plan and the implemented Distill-Wiki-Pipeline operator.

## Divergence

| Topic | Claude plan (this source) | Implemented (Distill-Wiki-Pipeline) |
|-------|---------------------------|--------------------------------|
| Web UI | Open WebUI Pipelines plugin | Dedicated FastAPI + React operator at `pipeline/ui/` |
| MCP | FastMCP with run_pipeline tools | Read-heavy MCP sidecar over `wiki_core` |
| LLM runtime | anthropic SDK in core | Ollama default (`qwen2.5:7b-instruct`) with approval gates |

## Decision

Adopted **Hybrid C** from brainstorming: markdown/git source of truth, Ollama-backed workflows, human approval gates, MCP as optional sidecar — not Open WebUI Pipelines.
