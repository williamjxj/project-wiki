---
type: concept
sources: [claude-multi-llm-research-synthesis-workflow, gemini-llm-wiki-multi-agent]
last_updated: 2026-05-29
---

# Two-Stage Ingestion

## Consensus

Both Claude and Gemini define a two-stage ingestion process. Gemini formalizes it most explicitly:

- **Stage 1 (Structural Analysis):** The model analyzes raw sources alongside the wiki index, maps entities, identifies overlaps, detects contradictions. No files are modified — the model outputs a structured blueprint of required changes.
- **Stage 2 (Generation & Linkage):** The model executes the blueprint — updates existing pages, creates new concept pages, establishes bidirectional links, logs operations.

This separation prevents formatting and structural organization competing for model attention, which can cause corrupted formatting and broken directories.

## Divergence

| Aspect | Claude | Gemini |
|--------|-------|--------|
| Formalization | Implicit in Phase 2 workflow | Explicit two-stage pipeline with blueprint |
| Tools | Generic "LLM writes, you browse" | OpenKB or Nashsu desktop app, file watcher |
| Input guidance | General schema | purpose.md for steering + CLAUDE.md for structure |

## Decision

The two-stage ingestion pipeline (analysis before generation) is confirmed — it is the canonical ingestion method. Stage 1 is read-only analysis outputting a blueprint; Stage 2 executes the blueprint.
