---
type: source-summary
raw: raw/llm/2026-05-13-claude-mem-weaver-gaps.md
source: claude
date: 2026-05-13
---

# mem-weaver Gaps & Improvements

## Key Claims

- Missing episodic/semantic/procedural taxonomy separation.
- Graph reasoning shallow — wikilinks vs typed entities/edges.
- No temporal reasoning / validity windows on facts.
- No MCP server (gap at time of writing; since designed).
- sqlite-vec constraints raised as open concern.
- Recommend: graph layer, temporal validity, MCP, 3-tier taxonomy, multi-tenant scoping, A-Mem linking, automate embeddings.

## Unique Insights

- Ties gaps to industry-standard memory taxonomy, not just retrieval quality.

## Contradictions

Questions sqlite-vec while [[chatgpt-mem-weaver-v2-roadmap]] marks hybrid done — risk register vs shipped.

**Updated (2026-05-24):** Hybrid search and MCP no longer gaps. Value gate, taxonomy, graph, temporal still open. See [[mem-weaver-known-gaps]].

Related concepts: [[mem-weaver-known-gaps]] [[mem-weaver-as-built-status]]
