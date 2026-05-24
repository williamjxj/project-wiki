---
name: wiki-query
description: Answer a question using the project wiki with citations. Use when the user asks about project research, decisions, or synthesized knowledge.
---

# Wiki Query

Answer questions from the wiki, not from raw sources or general knowledge.

## Steps

1. **Read** `wiki/index.md` to locate relevant pages
2. **Read** the identified wiki pages (prefer wiki/ over raw/)
3. **Synthesize** an answer with `[[wikilink]]` citations to specific concept and source pages
4. **Assess** whether the answer adds new knowledge not already in the wiki
5. If valuable and new → **offer** to file as a new `wiki/concepts/<slug>.md` page, update index and log

## Guardrails

- Read index.md FIRST — do not grep raw/ directory
- Cite wikilinks, not vague references
- Do not answer from general knowledge when wiki pages exist on the topic
- Good answers compound — offer to file insights that would be lost in chat history
