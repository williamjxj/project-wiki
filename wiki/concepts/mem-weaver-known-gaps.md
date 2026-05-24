---
type: concept
sources:
  - claude-mem-weaver-gaps
  - claude-capability-checklist
  - claude-mem-weaver-competitive-analysis
last_updated: 2026-05-24
---

# mem-weaver Known Gaps

## Consensus

- **Memory taxonomy:** missing explicit episodic / semantic / procedural separation ([[claude-mem-weaver-gaps]], [[claude-capability-checklist]])
- **Graph reasoning:** wikilink graph is flat — lacks typed entity nodes, edges, relationship queries.
- **Temporal reasoning:** facts not timestamped with validity windows.
- **MCP integration:** was a gap; design/plan now exists ([[claude-mcp-server-design]]).
- **Multi-tenant scoping:** no memory scoping API for different users/projects.
- **Production scalability:** underspecified beyond single-user MacBook Pro scope.

## Divergence

| Gap | [[claude-mem-weaver-gaps]] | [[claude-mem-weaver-competitive-analysis]] | [[claude-capability-checklist]] |
|-----|---------------------------|-------------------------------------------|--------------------------------|
| Semantic search | sqlite-vec constraints questioned | Claims FTS5-only, no embeddings | Targets hybrid FTS+vec+RRF |
| Phase A /chat | Not listed explicitly | Blocker for production chat product | Implies streaming SSE needed |
| Knowledge graph | Missing typed graph | N/A | Short form says "No KG"; long list wants KG |

## Decision

Treat [[claude-mem-weaver-gaps]] as **honest as-is** inventory. Hybrid search and MCP are **no longer gaps** (built per [[mem-weaver-as-built-status]]). Priority improvements: value gate, 3-tier memory taxonomy, temporal validity, typed knowledge graph, multi-tenant scoping.

Related: [[mem-weaver-as-built-status]], [[implementation-milestones]], [[agent-skills-taxonomy]]
