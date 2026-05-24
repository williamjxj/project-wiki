---
type: source-summary
raw: raw/llm/2026-04-21-gemini-second-brain-design.md
source: gemini
date: 2026-04-21
---

# NotebookLM-Style Second Brain Design

## Key Claims

- Cloud LLM reasons; local Ollama compiles — never block UX on local summarization.
- FastAPI delegator with BackgroundTasks for async synthesis.
- Tiered Markdown + SKILL.md Agent Skills packaging; optional ChromaDB/SQLite/Neo4j.
- Three phases: query/handoff → background synthesis → retrieval loop.
- Raw Q+A append-only logging; VC-style memory recommendations.
- Deterministic retrieval path needed as wiki scales.

## Unique Insights

- Agent Skills as interoperability layer, not just files.
- Explicit three-phase naming for the loop.

## Contradictions

ChromaDB emphasis vs sqlite-vec in Claude implementation docs.

**Resolved:** Storage tech divergence noted; codebase uses sqlite-vec. Index routing gap in [[agent-skills-taxonomy]].

## Related sources

[[claude-second-brain-prd]], [[claude-second-brain-implementation]], [[gemini-llm-memory-research]]

Related concepts: [[dual-llm-memory-pipeline]] [[agent-skills-taxonomy]] [[mem-weaver-architecture]]
