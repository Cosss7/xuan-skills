# xuan-skills Upstream Tracking

Track every skill's source, upstream commit, and modification summary for future sync.

## Upstream Repositories

| Repository | Remote | HEAD SHA (at fork time) |
|---|---|---|
| mattpocock/skills | `git@github.com:mattpocock/skills.git` | `6eeb81b5fcfeeb5bd531dd47ab2f9f2bbea27461` |

---

## mattpocock-engineering/ (7 skills)

| Skill | Source | File Commit | Status | Changes Summary |
|---|---|---|---|---|
| setup | `setup-matt-pocock-skills` | `4369256` | modified | Renamed. Matt references stripped. Repo references updated to `Cosss7/xuan-skills` (repo name unchanged). Seeds (issue-tracker-*, triage-labels, domain) unchanged. |
| grill-with-docs | `grill-with-docs` | `e74f006` | modified | Added `<HARD-GATE>` block to prevent implementation before design approval. |
| prototype | `prototype` | `f304057` | as-is | Supporting files (LOGIC.md, UI.md) unchanged. |
| diagnose | `diagnose` | `7afa86d` | as-is | HITL script unchanged. |
| improve-codebase-architecture | `improve-codebase-architecture` | `a36584e` | as-is | Supporting files (LANGUAGE.md, DEEPENING.md, HTML-REPORT.md, INTERFACE-DESIGN.md) unchanged. |
| to-prd | `to-prd` | `aaf2453` | as-is | Content unchanged. |
| zoom-out | `zoom-out` | `7afa86d` | as-is | Content unchanged. |

---

## mattpocock-productivity/ (4 skills)

| Skill | Source | File Commit | Status | Changes Summary |
|---|---|---|---|---|
| writing-great-skills | `writing-great-skills` | `6eeb81b` | as-is | Renamed only. Content unchanged. |
| grill-me | `grill-me` | `62f43a1` | as-is | Renamed only. Content unchanged. |
| caveman | `caveman` | `62f43a1` | as-is | Renamed only. Content unchanged. |
| handoff | `handoff` | `d54c497` | as-is | Renamed only. Content unchanged. |

---

## Sync Guide

When syncing from upstream:

```
Status: as-is     → can safely overwrite with upstream version (+ rename)
Status: modified  → review upstream diff, manually merge changes
Status: fused     → review both upstream sources, rebuild fused content
Status: new       → no upstream sync needed
```

Key changes to apply after overwriting an as-is skill:
1. Update `name:` field in frontmatter (no prefix)
2. Update any cross-references (no `xuan-` prefix)
3. Update doc paths as needed
4. Update config paths as needed
