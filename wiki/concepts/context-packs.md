---
type: concept
sources: [chatgpt-llm-based-project-workflow, gemini-llm-wiki-multi-agent, distill-ingest]
last_updated: 2026-05-29
---

# Context Packs

## Consensus

ChatGPT identifies context packs as per-module bundles for coding agents. Gemini extends this with specific machine-readable export formats:

- **`llms.txt`**: standard index of all available topics and pages (per llms.txt spec)
- **`llms-full.txt`**: entire compiled database as single ≤5MB flat file for pasting into any model window
- **`graph.jsonld`**: JSON-LD knowledge graph with typed entities and semantic relationships for programmatic graph-traversal

**Portable agent skills**: thematic subdirectories of the wiki can be compressed into Anthropic `SKILL.md` packages, placed in `~/.claude/skills/`, making them immediately discoverable by Claude Code. This avoids consuming token budgets reading raw markdown files on every session.

**Tool-specific ingest formats** (distill-ingest): each dev tool needs its own integration file:
- **Claude Code**: `CLAUDE.md` at project root (auto-loaded every session)
- **Cursor**: `.cursorrules` with instructions to check wiki before implementing
- **OpenCode/Codex CLI**: `AGENTS.md` with wiki article Read-before-Write rules
- **VSCode Copilot**: `.github/copilot-instructions.md` pointing to wiki/ for answers

## Divergence

| Aspect | ChatGPT | Gemini |
|--------|---------|--------|
| Format | Conceptual "bundle per feature" | Specific: llms.txt, llms-full.txt, JSON-LD, SKILL.md |
| Audience | Coding agents (Cursor, OpenCode, etc.) | Coding agents + Claude Code skills system |
| Packaging | Ad-hoc generation per module | Automated export + skill compilation |

## Decision

Context packs span both per-module bundles (ChatGPT's vision) and standardized exports (Gemini's specification). The `llms.txt`, `llms-full.txt`, and `graph.jsonld` formats provide the implementation spec for automated export.
