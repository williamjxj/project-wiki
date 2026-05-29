---
type: source-summary
raw: raw/llm/2026-05-24-claude-multi-llm-research-synthesis-workflow.md
source: claude
date: 2026-05-24
---

# Claude: Multi-LLM Research Synthesis Workflow

## Key Claims

1. **LLM outputs ≠ raw sources** — they are synthetic knowledge, first-pass synthesis with inherent drift, hallucinated edges, and model bias. This makes the wiki distillation layer more important, not less.
2. **Same prompt across models** — control the variable. Force diverse angles by asking each model: "What are the main approaches?", "What are the trade-offs?", "What would you warn against?"
3. **Wiki as persistent compounding artifact** — contradictions already flagged, cross-references built, synthesis already reflecting everything ingested. Contrast with RAG which re-discovers on every query.
4. **Decision records need source attribution and confidence** — for engineering decisions, you need to know *why* a choice was made, which LLM suggested it, what the runner-up was, and confidence level.
5. **Human review gate is non-negotiable** — never feed unreviewed wiki synthesis to a code agent.
6. **Lint every 3–5 ingests** — find contradictions, orphan concepts, stale claims.

## Unique Insights

- Explicit **contradictions tracking** dedicated page with UNRESOLVED flags is Claude's key addition — "this is where multi-LLM input earns its keep"
- Recommends specific tools: Obsidian (wiki IDE), [qmd](https://github.com/tobi/qmd) (BM25+vector search), obsidian-llm-wiki plugin, multi-agent variant (WayneChou-bot/LLM-Wiki-Agent-Workflow-Demo)
- Identifies risks: multi-LLM outputs can amplify hallucinations if contradictions aren't caught; wiki maintenance grows and requires weekly commitment; the Phase 3 compile step is currently manual
- Dev context package structure: constraints → architecture decisions → acceptance criteria → task list (note: dump the full wiki, compile targeted package per task)
- **4-phase architecture**: (1) Multi-LLM Collection, (2) Wiki Distillation, (3) Dev Context Package, (4) Dev Tools

## Contradictions

- None with ChatGPT on core approach. Both validate the pipeline. Claude adds more operational structure (contradictions tracking, lint rhythm, human review gate) while ChatGPT focuses more on architectural vision (context compression as moat, context packs as killer feature).
