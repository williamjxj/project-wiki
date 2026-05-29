---
type: source-summary
raw: raw/llm/2026-05-24-claude-multi-llm-research-synthesis-workflow.md
source: claude
date: 2026-05-24
---

# Claude — Multi-LLM Research Synthesis Workflow

## Key Claims

- The 6-step workflow **maps almost perfectly onto Karpathy's llm-wiki pattern** — multi-LLM collection → wiki distillation → dev context package is a meaningful upgrade over "paste chat into Cursor".
- **Critical reframe:** LLM outputs ≠ raw sources. They are *synthetic knowledge* — useful signal but drifted, hallucinated-at-edges, biased. Treat as **first-pass synthesis**, not ground truth. This makes the wiki layer *more* important.
- Four-phase architecture: Multi-LLM Collection → Wiki Distillation → Dev Context Package → Dev Tools.
- Wiki structure should include: `index.md`, `log.md`, `synthesis.md`, `decisions.md`, **`contradictions.md`**, `concepts/`.
- **[[contradictions-tracking]]** is where multi-LLM input earns its keep — explicit UNRESOLVED status for disagreements before dev starts.
- Operational rhythm: ingest one file at a time; **lint every 3–5 ingests**; query → file insights back into wiki.
- **[[human-review-gate]]** between Phase 2 (wiki) and Phase 3 (dev context) is **non-negotiable** — never feed unreviewed synthesis to a code agent.
- Phase 3 compiles targeted [[context-packs]] per task/feature — constraints → architecture decisions → acceptance criteria → task list. **Don't dump the full wiki.**
- **[[decision-records]]** must include source attribution, confidence levels, and runner-up alternatives — makes dev context defensible.
- Recommended tools: Obsidian (wiki IDE), Claude Code/OpenCode (wiki maintainer), qmd (BM25+vector search + MCP), obsidian-llm-wiki plugin, LLM-Wiki-Agent-Workflow-Demo (4 agent roles).
- Watch-outs: multi-LLM outputs can amplify hallucinations if contradictions aren't caught; wiki maintenance overhead grows; Phase 3 compile is currently manual (needs prompt template/script eventually).

## Unique Insights

- Identical prompts across models with controlled variables (source, date, prompt_hash tags).
- Prompt set recommendation: "What are the main approaches?", "What are the trade-offs?", "What would you warn against?"
- `contradictions.md` format with per-model positions and UNRESOLVED status — concrete example for auth strategy.
- Explicit Phase 3 output files: `CLAUDE.md`/`AGENTS.md`, `spec.md`, `architecture.md`, `tasks.md`.
- Weekly lint pass commitment to manage wiki maintenance overhead.

## Contradictions

- **Supports LLM-Wiki framing** — directly contradicts ChatGPT's [[wiki-vs-context-engine]] "don't build a wiki" advice. Aligns with Gemini's [[compounding-knowledge-layer]].
- **Human-in-the-loop emphasis** — stronger than ChatGPT's automated pipeline vision. ChatGPT optimizes for automated distillation; Claude insists on human review gate and manual Phase 3 compile (for now).
- **Dedup approach** — Claude relies on explicit contradiction tracking and lint passes rather than ChatGPT's embedding-based [[semantic-deduplication]] cluster pipeline.
