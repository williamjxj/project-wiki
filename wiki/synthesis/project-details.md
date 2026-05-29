---
type: project-details
status: current
date: 2026-05-29
export_cycle: 2
sources_ingested: 28
paired_brief: project-brief
---

# Project Details: mem-weaver

> Deep analysis for export cycle 2. Companion to [[project-brief]].

## Source Map

28 sources across 6 providers, organized by role in the research:

| Provider | Sources | Role |
|----------|---------|------|
| **Claude** (all versions) | 16 | Primary architecture, implementation plans, as-built audit, capability analysis |
| **ChatGPT** | 5 | Market positioning, API-level context control, v2 roadmap, workflow analysis |
| **Gemini** | 3 | Hierarchical memory, value gate, two-stage ingestion, closed-loop harvesting |
| **NotebookLM** | 1 | Independent architecture validation (SQLite+FTS5, cost quantification) |
| **YouTube video (TGLTommy)** | 1 (web) | LLM Wiki paradigm — three-layer architecture, knowledge governance |
| **Claude pipeline plan** | 1 | Pipeline operator, Open WebUI alternative |

### Research chronology

1. **Foundation (Apr 21):** Dual-LLM pipeline explored across Claude, ChatGPT, Gemini, and NotebookLM — converging on the same architecture independently.
2. **Product & planning (May 11–13):** PRD, implementation plan, architecture inspiration, gaps, competitive analysis.
3. **Implementation specs (Apr 21 – May 23):** Milestones A/B, Phase 4 hardening, chat frontend, MCP server.
4. **Workflow synthesis (May 24):** Three LLMs independently analyze the multi-LLM wiki workflow — converging on Collect → Ingest → Synthesize → Export → Apply.
5. **Paradigm enrichment (May 25):** LLM Wiki video introduces knowledge governance, hallucination write-back risk, three-layer architecture.

## Combined Understanding

### The mem-weaver architecture (implemented)

```
┌─────────────────────────────────────────────────────┐
│                   USER / CLIENT                       │
│  Next.js Chat UI  │  MCP Client  │  curl / API       │
└─────────┬──────────┴──────┬───────┴───┬──────────────┘
          │                 │           │
          ▼                 ▼           ▼
┌─────────────────────────────────────────────────────┐
│              FastAPI MIDDLEWARE DELEGATOR             │
│  POST /ingest (202)  │  GET /query   │  POST /chat   │
│  MCP stdio server    │  GET /health  │  GET /stats    │
└─────────┬──────────────────────┬─────────────────────┘
          │                      │
          ▼                      ▼
┌──────────────────┐  ┌──────────────────────────────┐
│   OLLAMA COMPILER │  │    HYBRID RETRIEVER          │
│  (Phase B async)  │  │  FTS5 + sqlite-vec + RRF     │
│  → wiki pages     │  │  → ranked snippets            │
└─────────┬─────────┘  └──────────────┬───────────────┘
          │                            │
          ▼                            ▼
┌─────────────────────────────────────────────────────┐
│                STORAGE TRIAD                          │
│  SQLite (pages, qa_pairs, FTS5, wiki_links)          │
│  Markdown vault (Obsidian-compatible wiki/)          │
│  sqlite-vec (embeddings, optional)                   │
└─────────────────────────────────────────────────────┘
```

### The research workflow (operational)

```
PHASE 1: COLLECT          LLM chats → raw/llm/, web clips → raw/web/
          ↓
PHASE 2: INGEST           One source at a time; two-stage (analyze → write)
          ↓
PHASE 3: SYNTHESIZE       [[contradictions-tracking]], lint, evolving-thesis
          ↓
PHASE 4: EXPORT           [[context-packs]], project-brief, project-details
          ↓
PHASE 5: APPLY            Parent project docs/ sync; coding agents use synthesized context
          ↓
PHASE 6: CLOSED LOOP      Dev session logs → re-ingest → wiki stays evergreen
```

This workflow is implemented as the **AGENTS.md skills** in this wiki submodule. The project-brief and project-details are the Phase 4 export vehicle.

## Comparison Matrix

### LLM Provider Perspectives on Core Topics

| Topic | Claude | ChatGPT | Gemini | NotebookLM | Video (TGLTommy) |
|-------|--------|---------|--------|------------|-------------------|
| **Pipeline** | Dual-LLM with explicit Phase A/B | Dual-LLM; focuses on retrieval economy | Value gate + incremental merge | 3-phase roadmap (pipe → retrieve → harden) | Three-layer architecture (raw → wiki → schema) |
| **Storage** | SQLite + Karpathy folders | Vector search or tags | Hierarchical folders + index | SQLite+FTS5 > ChromaDB for single-user | Raw Sources → Wiki → Schema |
| **Taxonomy** | `_index.md` + SKILL_TAXONOMY | Semantic search | Keyword scan + Ollama fallback | Agent Skills layer | Frontmatter governance |
| **Ingest trigger** | Batch 3–5 turns (plan) → per-turn (as-built) | Per-turn ok but costly | Value gate (SKIP/PROCESS) | Per-turn async | Synthesis-at-ingest |
| **Human role** | Non-negotiable review gate | Automated pipeline; less explicit gate | Obsidian synthesis & verification | N/A | Review queue for high-uncertainty claims |
| **Unique contribution** | Implementation plans, as-built audit, MCP design | Market positioning, context management API, workflow framing | Two-stage ingestion, closed-loop harvesting, purpose steering | SQLite validation, cost quantification, Lost-in-the-Middle mitigation | Knowledge governance, hallucination write-back risk |

### Concept Maturity

| Concept | Sources | Status |
|---------|---------|--------|
| [[dual-llm-memory-pipeline]] | 9 | **Stable** — all sources agree; implemented |
| [[memory-synthesis-vs-rag]] | 4 | **Stable** — hybrid approach adopted |
| [[mem-weaver-architecture]] | 5 | **Stable** — largely implemented |
| [[agent-skills-taxonomy]] | 6 | **Stable** — code exists; index format gap |
| [[contradictions-tracking]] | 3 | **Stable** — divergence table format + lint |
| [[human-review-gate]] | 3 | **Stable** — non-negotiable |
| [[context-compression]] | 3 | **Stable** — design principle adopted |
| [[context-packs]] | 3 | **Stable** — export vehicle |
| [[compounding-knowledge-layer]] | 3 | **Stable** — architectural center |
| [[research-to-implementation-pipeline]] | 3 | **Stable** — unified model |
| [[multi-pass-distillation]] | 3 | **Stable** — conceptual frame |
| [[semantic-deduplication]] | 3 | **Stable** — combined approach |
| [[two-stage-ingestion]] | 3 | **Stable** — operational ingest |
| [[closed-loop-harvesting]] | 3 | **Stable** — post-MVP |
| [[decision-records]] | 2 | **Stable** — lean adopted |
| [[purpose-steering]] | 3 | **Stable** — lean adopted |
| [[wiki-vs-context-engine]] | 3 | **Stable** — resolved 2:1 |
| [[llm-outputs-as-synthetic-sources]] | 3 | **Stable** — epistemic foundation |
| [[llm-wiki-paradigm]] | 1 | **Needs more sources** — single source; divergence + decision pending |
| [[knowledge-governance]] | 1 | **Needs more sources** — single source; divergence + decision pending |
| [[mem-weaver-as-built-status]] | 4 | **Stable** — reconciled via codebase audit |
| [[mem-weaver-known-gaps]] | 3 | **Stable** — honest inventory |
| [[implementation-milestones]] | 9 | **Stable** — comprehensive |
| [[implementation-readiness]] | 3 | **Stable** — north-star metric |
| [[mvp-scope]] | 2 | **Stable** — lean defined |
| [[pipeline-operator]] | 1 | **Single source** — Claude plan only; divergence table vs as-built |
| [[context-fragmentation]] | 3 | **Stable** — core problem confirmed |

## Deep Analysis

### 1. The paradigm shift: synthesis-at-ingest

The most important insight from this research is the **LLM Wiki paradigm** ([[llm-wiki-paradigm]]): moving knowledge synthesis from query time (RAG) to ingestion time. Each ingest permanently improves the knowledge asset rather than starting from scratch per query.

This isn't just a technical optimization — it's a **trust model shift**. In RAG:
- Raw chunks are authoritative but context-diluted
- Each query re-discovers the same information
- No analytical progress is retained between queries

In LLM Wiki:
- Wiki pages are synthesized but may contain LLM errors
- The asset compounds over time — contradictions flagged, cross-refs built
- The critical risk is **hallucination write-back**: an LLM writes incorrect info during ingestion, later retrieves its own incorrect output, and creates a self-reinforcing error loop

The three-layer architecture (Raw → Wiki → Schema) is the structural answer: raw sources are immutable, the wiki is curated but fallible, and schema (frontmatter with governance metadata) provides the audit trail.

### 2. Multi-LLM convergence validates the approach

Three independent LLMs (Claude, ChatGPT, Gemini) plus NotebookLM and a YouTube analysis all converge on the same architectural pattern. The divergences are about emphasis and mechanism — not fundamental disagreement:

- **Claude** focuses on implementation structure, human gates, and production readiness
- **ChatGPT** focuses on market positioning, context compression economics, and automated distillation
- **Gemini** provides the richest operational detail: two-stage ingestion, closed-loop harvesting, purpose steering, decay-weighted confidence
- **NotebookLM** independently validates the SQLite+FTS5 storage choice and quantifies token savings at 80–90%
- **The YouTube video** identifies knowledge governance as the long-term risk and the three-layer architecture as the structural pattern

The 2:1 resolution on LLM-Wiki vs "context engine" ([[wiki-vs-context-engine]]) confirms the Karpathy pattern is the right architectural center.

### 3. What's built vs what's design

The [[mem-weaver-as-built-status]] codebase audit (2026-05-24) reveals:

**Substantially built:**
- FastAPI middleware delegator with all API endpoints
- Ingest pipeline with Ollama summarization
- SQLite+FTS5 + sqlite-vec + RRF hybrid search
- Contradiction guardrails and wikilink graph
- Dead letter queue and stats
- POST /chat with SSE streaming
- MCP stdio server with 4 tools over shared `memory_api`

**Remaining design gaps:**
- Value gate (SKIP/PROCESS) in ingest — currently summarizes every Q+A
- `_index.md` pipe-table vs `wiki/index.md` catalog mismatch blocks chat retrieval
- Optional cloud LLM client for hosted Anthropic/OpenAI
- Knowledge governance (confidence markers, supersession, review queue)
- Typed entity-relationship graph (flat wikilinks only)
- Temporal validity tracking on facts

### 4. The epistemological foundation

A recurring theme across sources is that **LLM outputs are not ground truth** — they are synthetic first-pass knowledge ([[llm-outputs-as-synthetic-sources]]). This has operational implications:

- Raw LLM exports go to `raw/llm/` and are immutable after first ingest
- Wiki distillation is where verified signal emerges via contradiction tracking and human review
- Multi-model collection is essential — each model has different biases, blind spots, and confidence calibration
- Identical prompts across models with controlled variables (source, date, prompt_hash) enables systematic comparison

The decision to treat LLM outputs as synthetic sources is more than a label — it drives the entire wiki architecture: immutable raw, curated wiki, governance schema.

### 5. Human-in-the-loop is non-negotiable

Despite enthusiasm for automation, all workflow sources agree: a [[human-review-gate]] is required between wiki distillation and implementation. This is not a temporary constraint — it's an architectural property of a system that writes its own knowledge base.

The current AGENTS.md workflow implements this: ingest requires user confirmation, lint warnings require approval, export-brief requires review. Automation can accelerate ingest mechanics (Gemini's [[two-stage-ingestion]]) but not the review gate itself.

## Recommendations

### Short-term (next cycle)

1. **Fix the `_index.md` alignment** — This is the blocker for chat retrieval working correctly. Either teach the ingest workflow to write `_index.md` rows alongside `wiki/index.md`, or point the chat retriever at `wiki/index.md` catalog + hybrid search fallback (already exists).

2. **Add the value gate** — A SKIP/PROCESS classification before the Ollama summarization step. Many Q+A exchanges contain no reusable technical insight. This is the highest-ROI single change to reduce noise in the wiki.

3. **Document decision records** — Convert concept page Decisions into structured YAML decision records per [[decision-records]] format. Start with the "Firm decisions" table in the project brief — these are decisions the project has made but not formally recorded.

### Medium-term

4. **Design knowledge governance** — This is the most critical unaddressed risk ([[knowledge-governance]]). Define confidence markers, supersession metadata, and a review queue pattern before the wiki grows past ~50 auto-synthesized pages. The hallucination write-back risk compounds over cycles.

5. **Add `purpose.md`** — Per [[purpose-steering]], a root purpose file prevents the compounding knowledge layer from drifting off-topic. The project brief can evolve into this role.

6. **Evaluate pipeline operator** — If the manual ingest/lint/export workflow becomes burdensome at scale, the [[pipeline-operator]] pattern (shared Python core with CLI/MCP/UI adapters) is the automation path. Start with CLI automation before UI.

### Longer-term

7. **Implement closed-loop harvesting** — Re-ingest dev session logs from Cursor/Claude Code to keep the wiki evergreen and flag architecture drift ([[closed-loop-harvesting]]). Post-MVP after the core pipeline is stable.

8. **Typed knowledge graph** — Evolve flat wikilinks to typed entity relationships (`depends_on`, `supersedes`, `conflicts_with`). This enables contradiction detection and cross-reference quality that flat links cannot.

## Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|------------|
| **Hallucination write-back** (LLM writes errors → wiki → future LLM retrieves and reinforces) | Medium | Critical | Knowledge governance design before wiki scales; human review gate on all exports |
| **Wiki maintenance overhead** grows faster than value | Medium | High | Lint every 3–5 ingests; automation only after manual workflow is proven |
| **Multi-LLM contradictions amplify errors** rather than catch them | Low | High | Explicit UNRESOLVED status; human review resolves before export |
| **Single-user architecture limits future options** | Low | Medium | Accept constraint; design for single-user, don't pre-optimize for multi-tenant |
| **Next.js chat frontend becomes a distraction** | Medium | Low | Keep as optional entry point; MCP + Obsidian cover primary use cases |

## Open Questions for Further Research

1. **How to detect hallucination write-back in practice?** The video ([[knowledge-governance]]) identifies the risk but offers no detection mechanism. Is cross-model verification (ask another LLM to audit wiki pages) sufficient?

2. **What's the right confidence scoring system?** Gemini's decay-weighted confidence is the most detailed proposal, but no implementation exists. Should confidence be model-attributed, human-verified, or both?

3. **When does the pipeline operator become worth building?** At what wiki scale (sources, concepts, exports per cycle) does the manual workflow break down?

4. **What's the relationship between this project-wiki and the parent project's architecture?** The [[purpose-steering]] concept suggests `purpose.md` as the steering guide — but should the wiki own the purpose, or should the parent project brief own it and the wiki reflect it?

5. **How to handle supersession when the same claim appears in multiple sources?** The first source says X, the second says Y, the third says Z — does the wiki track all three, or does the Decision section represent the true current state?
