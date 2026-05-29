# Wiki Index

> Catalog of all wiki pages. Updated on every ingest.

## Sources

### v1 — Research foundation
- [[claude-dual-llm-memory-pipeline]] — Claude validates dual-LLM wiki compiler architecture with implementation sketch
- [[chatgpt-retrieval-vs-synthesis]] — ChatGPT research on RAG vs Karpathy LLM-wiki hybrid memory
- [[gemini-llm-memory-research]] — Gemini hierarchical memory synthesis with value gate and index routing
- [[chatgpt-api-token-context-management]] — API vs web UI context control (enables custom memory)
- [[notebooklm-dual-llm-architecture-design]] — NotebookLM validates dual-LLM pipeline; recommends SQLite+FTS5 over ChromaDB, quantifies 80–90% token savings

### v2 — Product & architecture
- [[claude-second-brain-prd]] — Original 12-step second brain product requirements
- [[claude-second-brain-implementation]] — Full MacBook Pro implementation plan with Phase A/B
- [[claude-middleware-delegator-plan]] — FastAPI delegator with ingest/query pipelines
- [[gemini-second-brain-design]] — NotebookLM-style full-stack design with Agent Skills
- [[claude-architecture-inspiration]] — Karpathy vs Spisak comparison and mem-weaver positioning

### Implementation specs & plans
- [[claude-fastapi-skeleton-design]] — Milestone A contract-first API design
- [[claude-fastapi-skeleton-plan]] — Milestone A implementation runbook
- [[claude-milestone-b-typed-models-design]] — Pydantic v2 + settings design
- [[claude-milestone-b-typed-models-plan]] — Milestone B implementation plan
- [[claude-phase-4-hardening-plan]] — Contradictions, wikigraph, DLQ, tests
- [[claude-chat-app-frontend-design]] — Next.js SSE chat + WikiSidebar design
- [[claude-mcp-server-design]] — stdio MCP with shared memory_api
- [[claude-mcp-server-plan]] — MCP ten-task implementation plan
- [[2026-05-25-cluade-pipeline-plan]] — Shared pipeline core with Open WebUI Pipelines or custom FastAPI operator

### v3 — Roadmap & analysis
- [[chatgpt-mem-weaver-v2-roadmap]] — v2 priorities: POST /chat, taxonomy, hybrid search status
- [[claude-mem-weaver-competitive-analysis]] — 2026 AI memory market positioning
- [[claude-frontend-admin-integration]] — Obsidian + Next.js integration options
- [[claude-capability-checklist]] — Target memory capabilities (semantic/episodic/procedural, MCP, SSE)
- [[claude-mem-weaver-gaps]] — Known gaps: taxonomy, graph, temporal, MCP

### External perspectives
- [[rag-graphrag-to-llm-knowledge-runtime]] — LLM Wiki paradigm: synthesis-at-ingest, three-layer architecture, knowledge governance
- [[chatgpt-llm-based-project-workflow]] — LLM-based project workflow: context-fragmentation, semantic-deduplication, context-packs, MVP-scope
- [[claude-multi-llm-research-synthesis-workflow]] — Multi-LLM research workflow: contradictions-tracking, human-review-gate, decision-records
- [[gemini-llm-wiki-multi-agent]] — LLM-Wiki in multi-agent dev: compounding-knowledge-layer, two-stage-ingestion, closed-loop-harvesting

## Concepts

- [[dual-llm-memory-pipeline]] — Ollama compiler + public LLM reasoner with Phase A/B loop
- [[memory-synthesis-vs-rag]] — Karpathy wiki synthesis vs vector retrieval; hybrid pragmatic
- [[mem-weaver-architecture]] — FastAPI delegator, SQLite+FTS5, Markdown vault, hybrid search
- [[agent-skills-taxonomy]] — Keyword-triggered skill categories and value gate
- [[mem-weaver-known-gaps]] — Taxonomy, graph, temporal, scoping gaps
- [[mem-weaver-as-built-status]] — Contradictions across sources on what's actually built
- [[implementation-milestones]] — Milestones A/B, Phase 4, chat frontend, MCP server
- [[llm-wiki-paradigm]] — Synthesis-at-ingest, knowledge runtime, three-layer architecture
- [[knowledge-governance]] — Confidence, supersession, review queue, hallucination write-back risk

## Synthesis

- [[evolving-thesis]] — running synthesis of all ingested research
- [[project-brief]] — quick export snapshot (generated at export)
- [[project-details]] — deep export snapshot for comparison, analysis, and recommendations (generated at export)
