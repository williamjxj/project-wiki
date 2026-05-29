---
type: concept
sources: [chatgpt-llm-based-project-workflow, distill-ingest]
last_updated: 2026-05-29
---

# Multi-Pass Distillation

## Consensus

ChatGPT defines the general pipeline (raw → clustered → summarized → canonicalized → implementation-oriented). The distill-ingest guide operationalizes this into four discrete stages with concrete methodology:

1. **Collect** (20 min): Ask same 3–5 seed questions across all LLMs. Save raw immediately — never paste from memory.
2. **Filter** (10 min): Apply **5-signal test** — score each paragraph on Specificity, Actionability, Non-obviousness, Consensus, Contradiction. Keep only paragraphs scoring ≥3.
3. **Distill** (30 min): Synthesize surviving content into structured form. LLM disagreements become explicit tradeoffs (Conflict → Decision Space).
4. **Canonical** (15 min): Write dense markdown with frontmatter, Facts (bullets), Implementation (code), Tradeoffs (table), Gotchas (≥3).

**Quality gate**: zero filler, every tool named with version, every tradeoff explicit.

## Divergence

| Aspect | ChatGPT | Distill-Ingest |
|--------|---------|---------------|
| Stages | raw → clustered → summarized → canonicalized | Collect → Filter → Distill → Canonical |
| Filter method | Embedding-based dedup | 5-signal manual scoring |
| Time budget | None specified | ~80 min per topic |
| Quality criteria | Implementation readiness | Zero filler, versioned tools, explicit tradeoffs, gotchas |

## Decision

Combine both. ChatGPT's embedding dedup handles the automated dedup layer; distill-ingest's 5-signal test provides the manual review methodology for human-in-the-loop quality.
