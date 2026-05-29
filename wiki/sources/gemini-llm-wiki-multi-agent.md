---
type: source-summary
raw: raw/llm/2026-05-24-gemini-llm-wiki-multi-agent.md
source: gemini
date: 2026-05-24
---

# Gemini: LLM-Wiki Pattern in Multi-Agent Development

## Key Claims

1. **Two-stage ingestion is essential** — Stage 1 (Structural Analysis): read-only analysis of raw sources + wiki index, detect conflicts, map entities, output blueprint. Stage 2 (Generation & Linkage): execute blueprint, write pages, update links, log changes. Separation prevents corrupted formatting.
2. **purpose.md for intent steering** — Beyond structural schema (`CLAUDE.md`/`schema.md`), a `purpose.md` file defines *why* the wiki exists: project thesis, engineering goals, core constraints, research boundary. Prevents knowledge graph drift.
3. **Decay-weighted confidence scoring** — Every claim carries metadata: confirmation sources, creation date, and exponential decay confidence (Ebbinghaus curve). Claims reinforced across sessions gain strength; unreferenced assertions decay.
4. **Systematic supersession** — When new info contradicts existing, mark old claim as stale, timestamped link to newer assertion, archive for auditability. Enables clean contradiction resolution.
5. **Graph-layered entity extraction** — Typed entities (Project, Library, API_Contract, Developer_Decision) with typed semantic relationships (depends_on, supersedes). Enables graph-traversal queries by coding agents.
6. **Hierarchical tree indexing** (PageIndex) — For documents >20 pages, build multi-level tree index rather than flat chunking. Keeps context windows clean, avoids vector DB overhead.
7. **Machine-readable exports** — `llms.txt` (topic index), `llms-full.txt` (≤5MB flattened dump), `graph.jsonld` (JSON-LD knowledge graph for programmatic traversal).
8. **Portable agent skills** — Thematic subdirectories compressed into Anthropic `SKILL.md` packages, loadable into `~/.claude/skills/`.
9. **Obsidian MCP integration** — Mount wiki to IDE via Obsidian MCP server: `obsidian_get_note`, `obsidian_patch_note`, `obsidian_search_notes`.
10. **Closed-loop dev-log harvesting** — Specific log paths for Claude Code, Cursor, Gemini CLI; harvester adapters convert logs to `raw/sessions/` for re-ingestion.

## Unique Insights

- **7-phase architecture** expands Claude's 4 phases: Exploratory Gathering → Immutable Logging → Automated Ingestion & Distillation → Synthesis & Verification → Context Export → IDE Execution → Closed-Loop Harvesting
- **Tool comparison matrix**: OpenKB (best for CLI/infrastructure), Nashsu/llm_wiki (best for visual analysis with Sigma.js graphs), Pratiyush/llm-wiki (best for automated session sync)
- Recommended implementation: OpenKB + Obsidian + MCP server as the practical stack
- Emphasizes Ebbinghaus forgetting curve for knowledge decay — most detailed treatment of knowledge lifecycle management
- Suggests JSON-LD schema graphs for agentic tool interoperability — a unique export format not mentioned by other sources

## Contradictions

- None with ChatGPT or Claude on core architecture. Gemini formalizes and extends concepts that Claude mentioned in passing (two-stage ingestion, purpose steering, closed-loop harvesting) into concrete implementation specifications.
- Gemini's 7-phase architecture is compatible with Claude's 4-phase model — it simply subdivides phases 2 and 4 into finer granularity.
