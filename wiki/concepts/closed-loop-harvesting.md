---
type: concept
sources: [chatgpt-llm-based-project-workflow, gemini-llm-wiki-multi-agent, claude-multi-llm-research-synthesis-workflow]
last_updated: 2026-05-24
---

# Closed-Loop Harvesting

## Consensus

Dev session transcripts flow back into `raw/sessions/` and re-enter ingestion, keeping the wiki evergreen ([[gemini-llm-wiki-multi-agent]]).

| Dev tool | Log location | Harvester |
|----------|-------------|-----------|
| Claude Code | `~/.claude/projects/*/*.jsonl` | `llmwiki.adapters.claude_code` |
| Cursor | `~/Library/.../Cursor/workspaceS...` | `llmwiki.adapters.cursor` |
| Gemini CLI | `~/.gemini/` | `llmwiki.adapters.gemini_cli` |

Re-ingestion flags where generated code deviates from planned architecture. Extends [[research-to-implementation-pipeline]] Phase 5.

ChatGPT mentions "Continuous Feedback + Memory" at high level. Claude doesn't detail harvest mechanics.

## Divergence

| Source | View |
|--------|------|
| Gemini | Automated harvester adapters; cron/git hook; `llmwiki sync` |
| ChatGPT | Continuous feedback loop in long-term vision |
| Claude | Not detailed |

## Decision

**Post-MVP.** Evaluate Pratiyush llm-wiki session sync adapters when core ingest/export pipeline is stable. Aligns with [[mvp-scope]].
