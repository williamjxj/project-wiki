---
type: source-summary
raw: raw/web/s2-notebooklm.md
source: web
date: 2026-05-26
---

# S2 NotebookLM: Second Brain + Memory System

## Key Claims

1. **Three-layer architecture**: Public Reasoning Engine (Claude API/GPT-4o for complex Q&A) + Local Memory Manager (Ollama for background compilation) + Delegator/Middle Layer (FastAPI for routing and orchestration).
2. **Storage as tiered markdown folder structure**: `/wiki/index.md`, `/wiki/concepts/`, `/wiki/skills/` — human-readable, version-controllable, editable.
3. **Agent Skills Layer**: folders containing SKILL.md files package specialized knowledge into domains.
4. **Vector/Graph Index for scaling**: ChromaDB or lightweight local graph (SQLite/Neo4j) for when the wiki scales past a few hundred pages.
5. **IDE / Graph Viewer**: Obsidian for visualizing the knowledge graph in real-time.

## Unique Insights

- Proposes a **Local Memory Manager (Ollama)** running locally to handle background memory compilation asynchronously — so the user never waits for summarization.
- Suggests ChromaDB or SQLite/Neo4j as scaling layer when wiki exceeds a few hundred pages — practical threshold for when vector/graph indexing becomes necessary.
- The "Agent Skills Layer" (SKILL.md per domain) aligns with Gemini's portable agent skills concept — different framing, same mechanism.

## Contradictions

- Recommends Ollama for local LLM, while claude-04-summary notes Ollama is "too slow" — this is a practical performance tradeoff, not architectural disagreement.
- Architecture is fully compatible with the llm-wiki pattern established by earlier sources.
