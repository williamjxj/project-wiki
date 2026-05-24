---
type: concept
sources: [chatgpt-llm-based-project-workflow, gemini-llm-wiki-multi-agent, claude-multi-llm-research-synthesis-workflow]
last_updated: 2026-05-24
---

# LLM Outputs as Synthetic Sources

## Consensus

LLM chat exports are **not ground truth** — they are first-pass synthetic knowledge ([[claude-multi-llm-research-synthesis-workflow]]).

| Property | Implication |
|----------|-------------|
| Drifted / hallucinated-at-edges | Cannot skip distillation and [[contradictions-tracking]] |
| Model-biased by training | Multi-model collection needed for diverse angles |
| Useful signal, not raw facts | [[compounding-knowledge-layer]] becomes *more* important, not less |

Collection rules (Claude + ChatGPT):
- Identical prompts across models; tag with `source`, `date`, `prompt_hash`
- Don't filter at collection — dump everything raw to `raw/llm/`
- Prompt set: approaches, trade-offs, warnings

Raw files now use AGENTS.md frontmatter (`type: llm-chat`, `source`, `topic`, `question`).

## Divergence

| Source | View |
|--------|------|
| Claude | Explicit epistemological reframe — synthetic first-pass synthesis |
| ChatGPT | Treats as research inputs to dedup/cluster; no epistemic flag |
| Gemini | Compilation mechanics focus; implies distillation needed |

## Decision

**Adopt synthetic-source framing.** All LLM exports in `raw/llm/` with proper frontmatter. Wiki distillation is where verified signal emerges.
