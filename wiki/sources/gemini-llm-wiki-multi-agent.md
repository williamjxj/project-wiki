---
type: source-summary
raw: raw/llm/2026-05-24-gemini-llm-wiki-multi-agent.md
source: gemini
date: 2026-05-24
---

# Gemini — LLM-Wiki Pattern in Multi-Agent Dev

## Key Claims

- The proposed six-step workflow is **highly practical** and aligns with agent-guided software engineering — separating research from implementation via a compiled **LLM-Wiki** intermediate layer ([[compounding-knowledge-layer]]).
- Standard RAG is ephemeral and wasteful: models re-segment and re-discover the same documents every query, causing token overhead and context dilution. A compiling wiki avoids feeding raw contradictory transcripts to coding agents.
- Full pipeline has **seven phases**: exploratory gathering → immutable logging → automated ingestion/distillation → synthesis/verification → context export → IDE execution → [[closed-loop-harvesting]].
- Ingestion must use a **[[two-stage-ingestion]]** pipeline: Stage 1 structural analysis (no file writes) → Stage 2 generation and linkage. Single-pass prompts fail on large transcripts.
- **[[purpose-steering]]** via `purpose.md` is essential alongside `schema.md` — schema tells the agent *how* to build; purpose tells *why* and prevents knowledge graph drift.
- Knowledge lifecycle requires: decay-weighted confidence scoring, systematic supersession of stale claims, and graph-layered entity extraction with typed relationships (`depends_on`, `supersedes`).
- Long documents (>20 pages) should use **tree indexing** (PageIndex) instead of flat chunking — hierarchical section nodes, not vector search.
- Dev-tool integration via machine-readable exports: `llms.txt`, `llms-full.txt` (5MB cap), `graph.jsonld`, portable Anthropic Skills (OpenKB), and Obsidian MCP servers for bi-directional vault access.
- **[[closed-loop-harvesting]]**: harvest dev session logs from Cursor/Claude Code/Gemini CLI → `raw/sessions/` → re-ingest to keep wiki evergreen and flag code/architecture drift.
- Recommended directory layout matches Karpathy pattern: `raw/` (read-only), `wiki/` (concepts, entities, sources, index, log), root `CLAUDE.md`/`schema.md` + `purpose.md`.
- Tool options: OpenKB (CLI, MarkItDown, PageIndex, Skills export), Nashsu llm_wiki (desktop, Louvain clustering), Pratiyush llm-wiki (session sync adapters, llms.txt export).

## Unique Insights

- Explicit ASCII architecture diagram with three macro-phases: Exploration & Harvesting → Knowledge Compilation → Active Development.
- Typed semantic relationships beyond wikilinks: entities like `Project`, `Library`, `API_Contract`, `Developer_Decision` with `depends_on` / `supersedes` edges.
- Ebbinghaus-inspired decay-weighted confidence — claims reinforced across sessions gain strength; unreferenced claims decay.
- MCP tools named specifically: `obsidian_get_note`, `obsidian_patch_note`, `obsidian_search_notes` for surgical vault access.
- Harvester adapter table mapping Claude Code JSONL, Cursor workspace paths, Gemini CLI directories.

## Contradictions

- **Directly contradicts** ChatGPT's [[wiki-vs-context-engine]] recommendation — Gemini fully embraces "LLM-Wiki" and Obsidian vault as the compiled knowledge layer, not a reframed "context engine."
- Ingestion approach differs from ChatGPT's [[semantic-deduplication]] via embeddings — Gemini emphasizes two-stage LLM analysis + tree indexing over embedding clustering as primary mechanism.
- MVP tooling differs: Gemini recommends Obsidian vault + OpenKB/Nashsu/Pratiyush tools; ChatGPT recommends CLI-first with no UI and custom FastAPI/LangChain pipeline.
