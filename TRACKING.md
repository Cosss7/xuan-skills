# xuan-skills Upstream Tracking

Track every skill's source, upstream commit, and modification summary for future sync.

## Upstream Repositories

| Repository | Remote | HEAD SHA (at fork time) |
|---|---|---|
| mattpocock/skills | `git@github.com:mattpocock/skills.git` | `aaf2453fbdfe7a15c07f11d861224f34ab4b53cb` |
| obra/superpowers | `git@github.com:obra/superpowers.git` | `6fd4507659784c351abbd2bc264c7162cfd386dc` |

---

## superpowers/ (12 skills)

| Skill | Source | File Commit | Status | Changes Summary |
|---|---|---|---|---|
| xuan-writing-plans | `writing-plans` | `f2cbfbe` | modified | Doc path: `docs/superpowers/` → `docs/ai-traces/`. Cross-refs updated to `xuan-` prefix. |
| xuan-using-git-worktrees | `using-git-worktrees` | `f2cbfbe` | modified | Paths: `~/.config/superpowers/` → `~/.config/xuan/`. Cross-refs updated. |
| xuan-subagent-driven-development | `subagent-driven-development` | `f2cbfbe` | modified | Removed `using-git-worktrees` from required workflow skills. Cross-refs and paths updated. |
| xuan-executing-plans | `executing-plans` | `f2cbfbe` | modified | Removed `using-git-worktrees` from required workflow skills. Cross-refs updated. |
| xuan-dispatching-parallel-agents | `dispatching-parallel-agents` | `9ccce3b` | as-is | Renamed only. Content unchanged. |
| xuan-requesting-code-review | `requesting-code-review` | `f2cbfbe` | as-is | Renamed only. Content unchanged. |
| xuan-receiving-code-review | `receiving-code-review` | `1455ac0` | as-is | Renamed only. Content unchanged. |
| xuan-verification-before-completion | `verification-before-completion` | `48410c7` | as-is | Renamed only. Content unchanged. |
| xuan-finishing-a-development-branch | `finishing-a-development-branch` | `f2cbfbe` | modified | Paths: `~/.config/superpowers/` → `~/.config/xuan/`. |
| xuan-systematic-debugging | `systematic-debugging` | `030a222` | modified | Cross-refs updated: `superpowers:test-driven-development` → `xuan-tdd`, `superpowers:verification-before-completion` → `xuan-verification-before-completion`. |
| xuan-design | `brainstorming` + `grill-with-docs` | `3f80f1c` / `e74f006` | **new** | Fused skill. Combines brainstorming's 5-phase process with grill-with-docs' terminology alignment and ADR creation. New content. |
| xuan-tdd (6 supporting files) | `test-driven-development` + `tdd` | `030a222` / `7afa86d` | **fused** | Superpowers TDD content fully retained. Added: Planning Phase, Tracer Bullet Rhythm, extended REFACTOR with deep-modules.md/refactoring.md refs. Supporting files from matt: interface-design.md, mocking.md, tests.md, deep-modules.md, refactoring.md. testing-anti-patterns.md from superpowers. |

---

## mattpocock-engineering/ (7 skills)

| Skill | Source | File Commit | Status | Changes Summary |
|---|---|---|---|---|
| xuan-setup | `setup-matt-pocock-skills` | `4369256` | modified | Renamed. Matt references stripped. Repo references updated to `Cosss7/xuan-skills`. Seeds (issue-tracker-*, triage-labels, domain) unchanged. |
| xuan-grill-with-docs | `grill-with-docs` | `e74f006` | as-is | Renamed only. Supporting files (ADR-FORMAT.md, CONTEXT-FORMAT.md) unchanged. |
| xuan-prototype | `prototype` | `f304057` | as-is | Renamed only. Supporting files (LOGIC.md, UI.md) unchanged. |
| xuan-diagnose | `diagnose` | `7afa86d` | as-is | Renamed only. HITL script unchanged. |
| xuan-improve-codebase-architecture | `improve-codebase-architecture` | `a36584e` | as-is | Renamed only. Supporting files (LANGUAGE.md, DEEPENING.md, HTML-REPORT.md, INTERFACE-DESIGN.md) unchanged. |
| xuan-to-prd | `to-prd` | `aaf2453` | as-is | Renamed only. Content unchanged. |
| xuan-zoom-out | `zoom-out` | `7afa86d` | as-is | Renamed only. Content unchanged. |

---

## mattpocock-productivity/ (4 skills)

| Skill | Source | File Commit | Status | Changes Summary |
|---|---|---|---|---|
| xuan-write-a-skill | `write-a-skill` | `62f43a1` | as-is | Renamed only. Content unchanged. |
| xuan-grill-me | `grill-me` | `62f43a1` | as-is | Renamed only. Content unchanged. |
| xuan-caveman | `caveman` | `62f43a1` | as-is | Renamed only. Content unchanged. |
| xuan-handoff | `handoff` | `d54c497` | as-is | Renamed only. Content unchanged. |

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
1. Update `name:` field in frontmatter to `xuan-` prefix
2. Update any cross-references to use `xuan-` prefix
3. Update doc paths (`docs/superpowers/` → `docs/ai-traces/`)
4. Update config paths (`~/.config/superpowers/` → `~/.config/xuan/`)
