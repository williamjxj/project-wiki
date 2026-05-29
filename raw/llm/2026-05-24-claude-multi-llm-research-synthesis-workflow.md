---
type: llm-chat
source: claude
topic: "Multi-LLM research synthesis workflow"
date: 2026-05-24
status: ingested
question: "Implement Karpathy llm-wiki for multi-LLM research → distillation → dev-tool handoff — good approach?"
url: "https://claude.ai/share/bd4b35f0-5d50-4860-b7f6-cdec24a85209"
---
**You**

/brainstorming I want to implement a basic version of andrej karpathy's llm-wiki, refer to [https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f), also refer to [https://x.com/karpathy/status/2039805659525644595](https://x.com/karpathy/status/2039805659525644595), or open mind to summery tools/apps. the thought and target: 1. when I start a project, I chat with various llms to collect information from scratch for different views, e.g I ask same questions in claude, chatgpt, gemini to get their research, analysis information 2. these info might be some duplicated, some unique, some useful some not. so need to filter, distill. 3. I want to use llm-wiki mode to ingest these info to refine and category the whole ideas for canonical and feasible solution 4. or some tools to summerize them to generate a feasible solution 5. then I feed this refined canonical feasible solution to dev-tools such as cursor, vscode, opencode etc, by combing their llm + input info, to deliver enough information 6. the dev-tools will use brainstorms, skills, mcp etc to spec, plan, tasks, implement etc. do you think this is a good way? or some suggestion?

---

**Claude**

Good read. Here's my assessment + suggested refinements.

---

### Your Workflow Is Sound — With One Key Reframe

Your 6-step flow maps almost perfectly onto Karpathy's pattern, but there's a conceptual gap worth naming:

**LLM outputs ≠ raw sources.** They're synthetic knowledge — useful signal, but inherently drifted, hallucinated-at-edges, and biased by each model's training. Treat them as *first-pass synthesis*, not ground truth. This actually makes the wiki layer *more* important, not less.

---

### Recommended Architecture

```
┌─────────────────────────────────────────────────────────────┐
│  PHASE 1: MULTI-LLM COLLECTION                              │
│  Same prompt set → Claude / GPT / Gemini                    │
│  Save as: raw/claude-{topic}.md, raw/gpt-{topic}.md         │
│  Tag: source, date, prompt_hash                             │
└───────────────────────┬─────────────────────────────────────┘
                        │ ingest (one-by-one, stay involved)
┌───────────────────────▼─────────────────────────────────────┐
│  PHASE 2: WIKI DISTILLATION  (Karpathy's pattern)           │
│  wiki/                                                      │
│  ├── index.md           (catalog of all pages)              │
│  ├── log.md             (append-only ingest history)        │
│  ├── synthesis.md       (evolving canonical view)           │
│  ├── decisions.md       (options + trade-offs)              │
│  ├── contradictions.md  (where LLMs disagreed)              │
│  └── concepts/          (entity/concept pages)              │
│                                                             │
│  LLM writes, you browse. Flag contradictions explicitly.    │
└───────────────────────┬─────────────────────────────────────┘
                        │ compile output (human review gate)
┌───────────────────────▼─────────────────────────────────────┐
│  PHASE 3: DEV CONTEXT PACKAGE                               │
│  CLAUDE.md / AGENTS.md  ← wiki schema + constraints        │
│  spec.md                ← what to build, what not to build  │
│  architecture.md        ← decisions + rationale             │
│  tasks.md               ← ordered implementation plan       │
└───────────────────────┬─────────────────────────────────────┘
                        │ feed into
┌───────────────────────▼─────────────────────────────────────┐
│  PHASE 4: DEV TOOLS                                         │
│  Cursor / VSCode / OpenCode / Claude Code                   │
│  + their LLM + your context package                         │
│  → spec → plan → implement                                  │
└─────────────────────────────────────────────────────────────┘
```

---

### Key Design Decisions

**Phase 1 — Collection**

- Use identical prompts across models (control the variable). Slight paraphrasing is fine; question intent must be identical.
- Ask each model: "What are the main approaches?", "What are the trade-offs?", "What would you warn against?" — forces diverse angles.
- Don't filter yet. Dump everything raw.

**Phase 2 — Wiki (this is where the value compounds)**

The core insight: instead of rediscovering knowledge on every query (RAG), the wiki is a **persistent, compounding artifact** — contradictions already flagged, cross-references already built, synthesis already reflecting everything ingested.

Practical operations:

- **Ingest** one file at a time. Let LLM update 10–15 wiki pages per source.
- **Lint** after every 3–5 ingests: find contradictions, orphan concepts, stale claims.
- **Query** → file good answers back into the wiki. Don't let insights die in chat.

**Critical addition for your use case — `contradictions.md`:**

```markdown
## [Topic]: Auth Strategy
- Claude: Use JWT + refresh tokens
- GPT: Use opaque tokens for security
- Gemini: Both, with JWT for internal, opaque for public
- Status: UNRESOLVED — research OAuth2 RFC before deciding
```

This is where multi-LLM input earns its keep.

**Phase 3 — Dev Context Package**

- CLAUDE.md / AGENTS.md is the schema — what the dev LLM needs to know about project conventions, what's decided, what's off-limits.
- Don't dump the full wiki. Compile a **targeted context package** per task/feature.
- Structure: constraints → architecture decisions → acceptance criteria → task list.

---

### Tools That Fit This Stack

| Purpose | Tool | Notes |
| --- | --- | --- |
| Obsidian | Wiki IDE | Graph view, Dataview, Marp, Web Clipper |
| Claude Code / OpenCode | Wiki maintainer | Reads/writes files, follows schema |
| [qmd](https://github.com/tobi/qmd) | Wiki search at scale | BM25+vector, CLI + MCP server |
| [obsidian-llm-wiki](https://github.com/kytmanov/obsidian-llm-wiki-local) | Obsidian plugin | 600+ stars, local-first implementation |
| [LLM-Wiki-Agent-Workflow-Demo](https://github.com/WayneChou-bot/LLM-Wiki-Agent-Workflow-Demo) | Multi-agent variant | 4 agent roles per source (PM, Dev, Design, Knowledge) — close to your use case |

---

### Honest Trade-offs

**Pros:**

- Wiki synthesis is reusable across sessions/projects — knowledge compounds
- Contradiction tracking forces explicit decisions before dev starts
- Dev tools get structured, curated context vs. raw chat dumps
- Works with any toolchain (it's just markdown + git)

**Cons / Watch-outs:**

- Multi-LLM outputs as sources can amplify hallucinations if contradictions aren't caught. **Never skip the lint step.**
- Wiki maintenance overhead grows — commit to a weekly lint pass
- The Phase 3 compile step (wiki → dev context) is currently manual. You'll want a prompt template or script for this eventually.
- Human review gate between Phase 2 and Phase 3 is non-negotiable. Don't feed unreviewed wiki synthesis to a code agent.

---

### Verdict

**Yes, this is the right direction.** The addition of multi-LLM collection → wiki distillation → dev context package is a meaningful upgrade over "paste chat into Cursor." The Karpathy pattern solves exactly the compounding/maintenance problem you'd hit otherwise.

The one thing I'd add that's not in Karpathy's spec: **explicit decision records** with source attribution and confidence levels. For engineering decisions specifically, you want to know *why* you chose something, which LLM suggested it, and what the runner-up was — that's what makes the dev context package defensible.