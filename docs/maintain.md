# project-wiki Branch Strategy

Shared wiki repo used as a submodule across different apps.

## Branch → App Mapping

```
main                  →  skeleton/template (pristine, minimal)
distill-wiki-pipeline →  github.com/williamjxj/distill-wiki-pipeline
wiki-memweaver        →  github.com/williamjxj/MemWeaver
```

## Core Rules

- **Never merge `distill-wiki-pipeline` or `wiki-memweaver` back into `main`**
- `main` is the clean skeleton only — one-way flow: `main → branches`
- Each app stays pinned to its own branch, no cross-contamination
- Keep `raw/` empty and `wiki/` minimal on `main`; generated export docs (`project-brief.md`, `project-details.md`) belong on app branches after research exists

---

## Setup — Pin MemWeaver to `wiki-memweaver`

```bash
# Inside MemWeaver repo
git submodule add -b wiki-memweaver https://github.com/williamjxj/project-wiki wiki
git submodule update --remote --merge
```

## Setup — Pin distill-wiki-pipeline to its branch

```bash
# Inside distill-wiki-pipeline repo
git submodule add -b distill-wiki-pipeline https://github.com/williamjxj/project-wiki wiki
git submodule update --remote --merge
```

---

## Daily Workflow — Updating Wiki Content for MemWeaver

```bash
cd wiki                      # enter submodule
git checkout wiki-memweaver  # confirm correct branch
# edit files
git add . && git commit -m "update wiki for MemWeaver"
git push origin wiki-memweaver
cd ..                        # back to MemWeaver root
git add wiki && git commit -m "bump wiki submodule"
git push
```

## Daily Workflow — Updating Wiki Content for distill-wiki-pipeline

```bash
cd wiki
git checkout distill-wiki-pipeline
# edit files
git add . && git commit -m "update wiki for distill-wiki-pipeline"
git push origin distill-wiki-pipeline
cd ..
git add wiki && git commit -m "bump wiki submodule"
git push
```

---

## Sync Skeleton Updates from main → branches

When `main` gets a useful skeleton update, propagate one-way:

```bash
git checkout wiki-memweaver
git merge main
git push origin wiki-memweaver

git checkout distill-wiki-pipeline
git merge main
git push origin distill-wiki-pipeline
```

**Never merge branches back into main.**

---

## Quick Reference

| Action | Command |
|---|---|
| Update wiki-memweaver content | `cd wiki && git checkout wiki-memweaver → edit → push` |
| Update distill-wiki-pipeline content | `cd wiki && git checkout distill-wiki-pipeline → edit → push` |
| Sync skeleton to wiki-memweaver | `git checkout wiki-memweaver && git merge main` |
| Pull latest branch in app | `git submodule update --remote` |
| Check submodule branch | `cd wiki && git branch` |
