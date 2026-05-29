---
type: concept
sources: [chatgpt-llm-based-project-workflow, gemini-llm-wiki-multi-agent, claude-multi-llm-research-synthesis-workflow]
last_updated: 2026-05-24
---

# Research-to-Implementation Pipeline

## Consensus

All sources describe multi-LLM research → compiled knowledge → dev-tool handoff. **Never feed raw chat dumps directly to coding agents.**

Unified view merging all three sources:

```
PHASE 1: MULTI-LLM COLLECTION
  Same prompts → Claude / GPT / Gemini → raw/ (immutable, tagged)
        ↓
PHASE 2: WIKI DISTILLATION
  [[two-stage-ingestion]] or [[semantic-deduplication]]
  → concepts/, sources/, synthesis, [[contradictions-tracking]]
  → lint every 3–5 ingests
        ↓
PHASE 3: DEV CONTEXT PACKAGE  ([[human-review-gate]] required)
  Compile [[context-packs]] per task: spec, architecture, tasks, AGENTS.md
        ↓
PHASE 4: DEV TOOLS
  Cursor / Claude Code / VSCode + MCP / Skills / llms.txt
        ↓
PHASE 5: CLOSED LOOP  ([[closed-loop-harvesting]])
  Dev session logs → raw/sessions/ → re-ingest → wiki stays evergreen
```

## Divergence

| Source | Emphasis |
|--------|----------|
| ChatGPT | Automated dedup/cluster pipeline; context compression as moat |
| Gemini | 7 explicit phases; Obsidian MCP; machine-readable exports |
| Claude | Human review gate; contradictions.md; manual Phase 3 compile for now |

Differences are emphasis, not architecture — all describe the same loop.

## Decision

**Lean: adopt Claude's 4-phase model with Gemini's closed-loop Phase 5 and ChatGPT's compression goals.** This project's wiki submodule already implements Phases 1–2 manually.
