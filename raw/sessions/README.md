# Dev Session Logs

Place harvested dev-session logs here for closed-loop re-ingestion.

## Source paths

| Tool | Log Location |
|------|-------------|
| Claude Code | `~/.claude/projects/<project-hash>/*.jsonl` |
| Cursor | `~/Library/Application Support/Cursor/User/workspaceStorage/<id>/` |
| OpenCode | session transcripts (export via `/handoff` or `session_read`) |

## Format

Harvested logs should be named `<YYYY-MM-DD>-<tool>-<topic>.md` with frontmatter:

```yaml
---
type: session-log
source: claude-code | cursor | opencode
topic: "what happened in this session"
date: YYYY-MM-DD
status: pending
---
```

After ingest, `status` changes to `ingested` and the raw file is never modified.
