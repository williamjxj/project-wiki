---
type: source-summary
raw: raw/llm/2026-05-11-claude-second-brain-prd.md
source: claude
date: 2026-05-11
---

# Second Brain PRD

## Key Claims

- 12-step loop: chat → extract Q+A → delegator ingest → Ollama wiki summary → indexed storage → query on next turn → inject summary → public LLM → repeat.
- raw layer = Q+A pairs; wiki layer = indexed Agent-Skills incremental graphified KB.
- References Karpathy LLM-wiki, Agent Skills, memoryLLM/M+, LangChain, LlamaIndex, Ollama.
- Goal: app grows smarter without context window limit via compiled knowledge feedback.

## Unique Insights

- Original product requirements document anchoring all subsequent architecture work.
- Explicitly combines LLM-wiki ingest with Agent-Skills categorization.

## Contradictions

None — foundational PRD.

## Related sources

[[claude-second-brain-implementation]], [[gemini-second-brain-design]], [[claude-middleware-delegator-plan]]

Related concepts: [[dual-llm-memory-pipeline]] [[agent-skills-taxonomy]] [[mem-weaver-architecture]]
