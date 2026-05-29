---
type: concept
sources: [chatgpt-llm-based-project-workflow, gemini-llm-wiki-multi-agent, claude-multi-llm-research-synthesis-workflow]
last_updated: 2026-05-24
---

# Context Packs

## Consensus

Dev tools need scoped, compressed context bundles — **not raw research dumps, not the full wiki** ([[claude-multi-llm-research-synthesis-workflow]]). Part of [[context-compression]] and [[implementation-readiness]].

Structure per Claude: constraints → architecture decisions → acceptance criteria → task list.

## Divergence

| Source | Handoff format |
|--------|---------------|
| ChatGPT | CLI `generate-context <domain>` → per-tool tuning |
| Gemini | `llms.txt`, `llms-full.txt`, `graph.jsonld`, Anthropic Skills, Obsidian MCP |
| Claude | Phase 3 files: `AGENTS.md`, `spec.md`, `architecture.md`, `tasks.md` — targeted per task/feature |

## Decision

**Lean: both targeted packs AND standard exports.** Export-brief workflow produces Phase 3 files; later add Gemini-style `llms.txt` and Skills packaging.
