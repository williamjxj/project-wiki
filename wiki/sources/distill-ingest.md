---
type: source-summary
raw: raw/llm/2026-05-26-claude-distill-ingest.md
source: claude
date: 2026-05-26
---

# Collect → Distill → Canonical File → Ingest

> Multi-LLM knowledge distillation and context engineering methodology. A dense guide on turning raw LLM output into assertion-dense canonical files that coding tools can consume as structured context.

## Key Claims

- Raw multi-LLM output is noise — value emerges only after distillation into assertion-dense canonical files
- 4-stage pipeline: Collect → Filter/Distill → Canonical File → Ingest; skipping any stage breaks the chain
- 5-signal test for filtering LLM outputs: Specificity, Actionability, Non-obviousness, Consensus, Contradiction — keep only blocks scoring 3+
- LLM conflicts define the **decision space**, not noise — the most valuable signal when LLMs disagree
- Distillation quality gate: zero filler sentences, every tool versioned, all tradeoffs explicit with ≥2 options and criteria, ≥3 gotchas, self-contained
- One topic → one canonical wiki file → referenced from tool configs (CLAUDE.md, AGENTS.md, .cursorrules, etc.)
- MCP integration is the highest-leverage automation for wiki access
- Distillation is a compounding skill — first takes 30 min, 20th takes 10 min

## Unique Insights

- **Meta-distillation**: using an LLM (Claude/ChatGPT) to distill LLM outputs — 5 min compute for ~80% of final canonical file
- **Anti-Pattern Hall of Fame**: 7 named anti-patterns with specific failure mechanisms and fixes (collecting from 7+ LLMs, no annotation, one giant notes.md, re-asking LLMs instead of checking wiki, etc.)
- **Decision framework**: branching logic for when to run full pipeline (~80 min) vs skip to single bullet (~2 min)
- **Canonical file selection matrix**: 7 file types mapped to consuming tools (Claude Code, Cursor, OpenCode, Copilot, MemWeaver)
- **No-code stack recommendation**: Obsidian vault (= wiki/) + Smart Connections plugin + Git sync
- **Git as version control for knowledge**: treat wiki/ like src/ with commits, diffs, and blame
- **4 tiers of automation**: no-code (Obsidian) → agent-assisted (Claude.ai Projects) → MCP servers → full ETL pipeline

## Contradictions

_(single source — no contradictions to flag)_

## Related Concepts

- [[multi-pass-distillation]] — progressive raw → canonicalized refinement
- [[context-packs]] — scoped dev-tool handoff bundles
- [[research-to-implementation-pipeline]] — broader 5-phase flow
- [[context-compression]] — tiered compression as competitive moat
- [[compounding-knowledge-layer]] — persistent wiki artifact
- [[closed-loop-harvesting]] — dev session logs back into raw/
