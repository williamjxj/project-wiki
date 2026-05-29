---
type: concept
sources: [claude-multi-llm-research-synthesis-workflow, gemini-llm-wiki-multi-agent]
last_updated: 2026-05-29
---

# Closed Loop Harvesting

## Consensus

The concept is confirmed by both sources. Claude implies it (file query answers back into wiki). Gemini provides the most detailed implementation specification.

**Gemini's implementation:**
- Development tools write chronological conversation logs to local project directories
- Harvester adapters scan specific paths per tool:
  - Claude Code: `~/.claude/projects/*/*.jsonl`
  - Cursor: `~/Library/.../Cursor/workspaceS...`
  - Gemini CLI: `~/.gemini/`
- Running `llmwiki sync` converts logs to markdown under `raw/sessions/`
- These logs run through the ingestion pipeline, flagging discrepancies between generated code and planned architecture
- Keeps the wiki evergreen and in sync with the actual codebase

## Divergence

| Aspect | Claude | Gemini |
|--------|-------|--------|
| Specificity | Conceptual — "don't let insights die" | Concrete — tool-specific paths, harvester adapters, sync command |
| Implementation | Manual query-filing | Automated log scanning + re-ingestion pipeline |

## Decision

Closed-loop harvesting is confirmed as a core workflow component. Gemini's tool-specific harvester paths provide the implementation blueprint for automation post-MVP.
