---
type: source-summary
raw: raw/llm/2026-05-15-gemini-llm-memory-research.md
source: gemini
date: 2026-05-15
---

# Hierarchical Memory Synthesis (Gemini)

## Key Claims

- Moves from linear memory (send everything) to synthesized memory (send essence only).
- Five-stage pipeline: interaction → synthesis → organization → retrieval → execution.
- Fast keyword scan of wiki index before public API call — no LLM needed for speed.
- Background Ollama worker: value gate (SKIP/PROCESS) then incremental wiki merge.
- Tiered Markdown folder structure with index.md map and concepts/ deep dives.
- Keep short-term buffer (last 3 raw messages) alongside long-term wiki.
- Compile prompts: Knowledge Sieve + Incremental Compiler with skill-based tone.

## Unique Insights

- Treats local machine as Knowledge Compiler, public API as Tongue.
- Phase A instant retrieval + Phase B parallel synthesis — user never waits for Ollama.

## Contradictions

ChromaDB/Neo4j mentioned vs sqlite-vec in later Claude docs — storage tech divergence in [[mem-weaver-architecture]].

**Resolved:** Summary trigger reconciled in [[dual-llm-memory-pipeline]]. ChromaDB vs sqlite-vec remains open at scale.

## Related sources

[[claude-dual-llm-memory-pipeline]], [[chatgpt-retrieval-vs-synthesis]], [[gemini-second-brain-design]]

Related concepts: [[dual-llm-memory-pipeline]] [[agent-skills-taxonomy]]
