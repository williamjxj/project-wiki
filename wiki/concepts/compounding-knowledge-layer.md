---
type: concept
sources: [chatgpt-llm-based-project-workflow, claude-multi-llm-research-synthesis-workflow, gemini-llm-wiki-multi-agent, s2-notebooklm]
last_updated: 2026-05-29
---

# Compounding Knowledge Layer

## Consensus

The core architectural shift is from transient LLM chat sessions to a persistent, structured knowledge base that compounds over time. All three sources agree.

Gemini adds the most detailed knowledge lifecycle management:
- **Decay-weighted confidence scoring**: every claim carries confirmation sources, creation date, and exponential decay confidence (Ebbinghaus forgetting curve). Claims reinforced across sessions gain strength; unreferenced assertions decay.
- **Systematic supersession**: contradictions don't just get flagged — old claims are marked stale with timestamped links to newer assertions, archived for auditability.
- **Graph-layered entity extraction**: typed entities (Project, Library, API_Contract, Developer_Decision) with typed relationships (depends_on, supersedes) enable programmatic graph traversal by coding agents.

## Divergence

| Aspect | ChatGPT | Claude | Gemini |
|--------|---------|--------|--------|
| Emphasis | Context compression as moat | Persistent artifact | Knowledge lifecycle + graph typing |
| Knowledge model | Tiered compression pipeline | Cross-ref + contradiction flags | Decay-weighted confidence + supersession |
| Entity layer | Flat concepts | Wiki pages with wikilinks | Typed entities with semantic relationships |

**Scaling threshold** (s2-notebooklm): vector/graph indexing (ChromaDB/SQLite/Neo4j) becomes necessary when the wiki exceeds a few hundred pages. Below that, markdown + git + Obsidian suffices. This provides a concrete scaling milestone for the MVP-to-production transition.

**Local Memory Manager** (s2-notebooklm): a local Ollama instance can handle background memory compilation (summarization, dedup, linking) asynchronously — keeping cloud API costs low for routine processing while reserving cloud LLMs for complex reasoning.

## Decision

The compounding knowledge layer is the central architectural pattern — wiki persists and compounds. Gemini's knowledge lifecycle management (decay, supersession, typed entities) is the most complete model and should guide implementation.
