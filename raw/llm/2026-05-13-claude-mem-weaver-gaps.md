---
type: llm-chat
source: claude
topic: mem-weaver gaps and improvement recommendations
date: 2026-05-13
question: What gaps exist in mem-weaver (taxonomy, graph, MCP, temporal reasoning) and what should be improved?
status: ingested
---

## Miss

- memory taxonomy: missing explicit episodic / semantic / procedural separation; the industry has standardized on this for good reason.
- graph reasoning: wikilink graph is flat; lacks entity nodes, typed edges, and relationship queries.
- production scalability 
- Ecosystem / Framework fit: No MCP server
- No temporal reasoning — facts aren't timestamped with validity windows
- sqlite-vec constraints ?


## Improvement Recommendation

- Add a knowledge graph layer (entity + relations)
- Add temporal validity to stored facts
- Expose as an MCP server
- Implement the 3-tier memory taxonomy (episodic, sementic-'distilled wiki facts', procedural)
- Add multi-tenant memory scoping
- Evolve(改进) wiki pages with A-Mem style linking
- Automate embedding generation (remove backfill script)
- Add explicit memory compression/summarization layer