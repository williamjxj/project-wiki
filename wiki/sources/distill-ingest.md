---
type: source-summary
raw: raw/llm/2026-05-26-claude-distill-ingest.md
source: claude
date: 2026-05-26
---

# Claude: Distill-Ingest Methodology Guide

## Key Claims

1. **Pipeline must have 4 discrete stages**: Collect → Filter → Distill → Canonical File → Ingest. Skipping any one breaks the chain.
2. **5-signal filter**: Score every paragraph on Specificity, Actionability, Non-obviousness, Consensus, Contradiction — keep only paragraphs scoring 3+.
3. **Time budget per topic**: Collect 20 min · Filter 10 min · Distill 30 min · Canonical 15 min · Ingest 5 min = ~80 min for a durable artifact.
4. **Distillation quality gate**: zero filler, every tool named with version, every tradeoff explicit, at least 3 gotchas per article.
5. **Conflict → Decision Space framing**: LLM disagreements define the design space, not bugs to eliminate. State as tradeoffs with explicit choices.
6. **Canonical file structure**: Frontmatter (title, slug, tags, sources, updated) + Facts (bullets) + Implementation (code) + Tradeoffs (table) + Gotchas (≥3).
7. **Tiered automation ladder**: No-code (Obsidian) → Agent-assisted (Claude Projects) → MCP Servers → ETL Pipeline. Don't overbuild — use the simplest tier that fits scale.
8. **Tool-specific ingest**: Each coding tool needs its own integration — CLAUDE.md for Claude Code, .cursorrules for Cursor, AGENTS.md for OpenCode, copilot-instructions.md for VS Code Copilot.

## Unique Insights

- Detailed **chunking strategy guide** (fixed-size vs semantic vs recursive vs small-to-big) with gotchas per approach
- **Same seed questions across all LLMs** — specific template: "core concepts, failure modes, best tools, non-obvious tradeoffs, recommended approach"
- **ETL pipeline prototype** — 80-line Python script using Claude API to distill raw → canonical
- **Tool-specific MCP integration**: filesystem server, memory server, mcp-obsidian, mcp-sqlite, and MemWeaver-as-MCP
- Recommends **NotebookLM** as a no-code alternative for quick synthesis
- Most practical, step-by-step guide of all sources — directly actionable without further interpretation

## Contradictions

- None with earlier sources. This is a methodology companion that operationalizes concepts from sources 1–3 into concrete procedures.
- The "Conflict → Decision Space" reframing extends Claude's original contradiction-tracking (source 2) beyond UNRESOLVED flags into design space exploration.
