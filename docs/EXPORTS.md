# Export Documents

The wiki has one live synthesis file and two generated export files.

## `wiki/synthesis/evolving-thesis.md`

Live working synthesis. Updated after every ingest. It captures the current state of understanding while research is still moving.

Keep this file on `main` as an empty starter. On project branches, it evolves continuously.

## `wiki/synthesis/project-brief.md`

Generated quick view. Use it for fast project orientation, brainstorming, planning, and implementation handoff.

It should be concise and include:

- Problem
- Current understanding
- Chosen approach
- Constraints
- Non-goals
- Rejected alternatives
- Open questions

Do not keep a generated `project-brief.md` on `main`.

## `wiki/synthesis/project-details.md`

Generated deep view. Use it when an agent or developer needs to combine sources, compare alternatives, analyze tradeoffs, and make suggestions.

It should preserve nuance and include:

- Source map
- Combined understanding
- Comparison matrix
- Deep analysis
- Recommendations
- Implementation notes
- Risks and mitigations
- Open questions for further research

Do not keep a generated `project-details.md` on `main`.

## Export Command

Prefer:

```text
export synthesis
```

Compatibility triggers also work:

```text
export brief
export details
```
