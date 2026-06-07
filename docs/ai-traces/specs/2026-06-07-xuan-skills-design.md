# xuan-skills Design Spec

> Author: xuan (via grill-with-docs session)
> Date: 2026-06-07

## Overview

Combine two skill repositories (mattpocock/skills and obra/superpowers) into a single curated collection, published to skills.sh. Retain the best of each — superpowers' discipline and rigor, mattpocock's architectural depth and engineering workflow — under a unified `xuan-` prefix.

## Upstream Sources

Future sync should diff against these repository-level commits:

| Repository | Remote | HEAD SHA |
|---|---|---|
| mattpocock/skills | `git@github.com:mattpocock/skills.git` | `aaf2453fbdfe7a15c07f11d861224f34ab4b53cb` |
| obra/superpowers | `git@github.com:obra/superpowers.git` | `6fd4507659784c351abbd2bc264c7162cfd386dc` |

Per-skill file-level commits are tracked in the Skill Inventory below.

## Naming Convention

- All skills prefixed `xuan-`
- Origin determines name: superpowers-sourced skills keep their superpowers name; matt-sourced skills keep their matt name
- Hyphenated, lowercase, no special chars (compliant with skills.sh spec)

## Directory Structure

```
xuan-skills/
├── docs/
│   └── ai-traces/
│       └── specs/
│           └── 2026-06-07-xuan-skills-design.md
├── skills/
│   ├── 01-foundation/
│   │   ├── xuan-setup/SKILL.md              # matt -> setup-matt-pocock-skills
│   │   └── xuan-write-a-skill/SKILL.md      # matt -> write-a-skill (lightweight)
│   ├── 02-design/
│   │   ├── xuan-design/SKILL.md             # FUSION: brainstorm + grill-with-docs
│   │   ├── xuan-grill-with-docs/SKILL.md    # matt (preserved as-is)
│   │   ├── xuan-grill-me/SKILL.md           # matt
│   │   ├── xuan-writing-plans/SKILL.md      # superpowers -> writing-plans
│   │   └── xuan-prototype/SKILL.md          # matt
│   ├── 03-implement/
│   │   ├── xuan-tdd/
│   │   │   ├── SKILL.md                     # FUSION: test-driven-development + tdd
│   │   │   ├── interface-design.md          # matt
│   │   │   ├── mocking.md                   # matt
│   │   │   ├── tests.md                     # matt
│   │   │   ├── deep-modules.md              # matt
│   │   │   └── refactoring.md               # matt
│   │   ├── xuan-using-git-worktrees/SKILL.md  # superpowers
│   │   ├── xuan-subagent-driven-development/SKILL.md  # superpowers
│   │   ├── xuan-executing-plans/SKILL.md    # superpowers
│   │   └── xuan-dispatching-parallel-agents/SKILL.md  # superpowers
│   ├── 04-quality/
│   │   ├── xuan-requesting-code-review/SKILL.md   # superpowers
│   │   ├── xuan-receiving-code-review/SKILL.md    # superpowers
│   │   ├── xuan-verification-before-completion/SKILL.md  # superpowers
│   │   └── xuan-finishing-a-development-branch/SKILL.md   # superpowers
│   ├── 05-maintain/
│   │   ├── xuan-diagnose/SKILL.md            # matt (+ supporting scripts)
│   │   ├── xuan-systematic-debugging/SKILL.md # superpowers (+ supporting files)
│   │   ├── xuan-improve-codebase-architecture/SKILL.md  # matt (+ supporting files)
│   │   ├── xuan-triage/SKILL.md              # matt (+ supporting files)
│   │   ├── xuan-to-issues/SKILL.md           # matt
│   │   ├── xuan-to-prd/SKILL.md              # matt
│   │   └── xuan-zoom-out/SKILL.md            # matt
│   └── 06-communicate/
│       ├── xuan-caveman/SKILL.md             # matt
│       └── xuan-handoff/SKILL.md             # matt
├── CONTEXT.md
├── CLAUDE.md
└── .gitignore
```

No `plugin.json` — skills.sh CLI auto-discovers via `skills/<category>/<name>/SKILL.md` scanning.

## Skill Inventory

Each entry tracks: upstream source, last upstream commit touching the file, modification status, and a summary of changes made.

### Category: 01-foundation

| xuan Skill | Source Repo | Source Skill | Source File Commit | Status | Changes |
|---|---|---|---|---|---|
| `xuan-setup` | mattpocock/skills | `setup-matt-pocock-skills` | `4369256` | modified | Renamed. Matt references stripped. Seeds (issue-tracker-*, triage-labels, domain) adapted. |
| `xuan-write-a-skill` | mattpocock/skills | `write-a-skill` | `62f43a1` | as-is | Renamed only. Content unchanged. |

### Category: 02-design

| xuan Skill | Source Repo | Source Skill | Source File Commit | Status | Changes |
|---|---|---|---|---|---|
| `xuan-design` | superpowers + matt | `brainstorming` + `grill-with-docs` | `3f80f1c` / `e74f006` | **new** | New skill. Combines brainstorming's 9-step process with grill-with-docs' terminology alignment and ADR creation. 5-phase flow. See Fusion Details. |
| `xuan-grill-with-docs` | mattpocock/skills | `grill-with-docs` | `e74f006` | as-is | Content unchanged. Supporting files (ADR-FORMAT.md, CONTEXT-FORMAT.md) included. |
| `xuan-grill-me` | mattpocock/skills | `grill-me` | `62f43a1` | as-is | Content unchanged. |
| `xuan-writing-plans` | obra/superpowers | `writing-plans` | `f2cbfbe` | as-is | Content unchanged. Doc output path updated to `docs/ai-traces/plans/`. |
| `xuan-prototype` | mattpocock/skills | `prototype` | `f304057` | as-is | Content unchanged. Supporting files (LOGIC.md, UI.md) included. |

### Category: 03-implement

| xuan Skill | Source Repo | Source Skill | Source File Commit | Status | Changes |
|---|---|---|---|---|---|
| `xuan-tdd` | superpowers + matt | `test-driven-development` + `tdd` | `030a222` / `7afa86d` | **fused** | Superpowers SKILL.md content retained fully. Added: matt's 4-phase flow (Planning → Tracer Bullet → Incremental Loop → Refactor), tracer bullet philosophy. New supporting files: interface-design.md, mocking.md, tests.md, deep-modules.md, refactoring.md. |
| `xuan-using-git-worktrees` | obra/superpowers | `using-git-worktrees` | `f2cbfbe` | as-is | Content unchanged. |
| `xuan-subagent-driven-development` | obra/superpowers | `subagent-driven-development` | `f2cbfbe` | as-is | Content unchanged. |
| `xuan-executing-plans` | obra/superpowers | `executing-plans` | `f2cbfbe` | as-is | Content unchanged. |
| `xuan-dispatching-parallel-agents` | obra/superpowers | `dispatching-parallel-agents` | `9ccce3b` | as-is | Content unchanged. |

### Category: 04-quality

| xuan Skill | Source Repo | Source Skill | Source File Commit | Status | Changes |
|---|---|---|---|---|---|
| `xuan-requesting-code-review` | obra/superpowers | `requesting-code-review` | `f2cbfbe` | as-is | Content unchanged. |
| `xuan-receiving-code-review` | obra/superpowers | `receiving-code-review` | `1455ac0` | as-is | Content unchanged. |
| `xuan-verification-before-completion` | obra/superpowers | `verification-before-completion` | `48410c7` | as-is | Content unchanged. |
| `xuan-finishing-a-development-branch` | obra/superpowers | `finishing-a-development-branch` | `f2cbfbe` | as-is | Content unchanged. |

### Category: 05-maintain

| xuan Skill | Source Repo | Source Skill | Source File Commit | Status | Changes |
|---|---|---|---|---|---|
| `xuan-diagnose` | mattpocock/skills | `diagnose` | `7afa86d` | as-is | Content unchanged. HITL script included. |
| `xuan-systematic-debugging` | obra/superpowers | `systematic-debugging` | `030a222` | as-is | Content unchanged. Supporting files (root-cause-tracing.md, defense-in-depth.md, condition-based-waiting.md) included. |
| `xuan-improve-codebase-architecture` | mattpocock/skills | `improve-codebase-architecture` | `a36584e` | as-is | Content unchanged. Supporting files (LANGUAGE.md, DEEPENING.md, HTML-REPORT.md, INTERFACE-DESIGN.md) included. |
| `xuan-triage` | mattpocock/skills | `triage` | `179a14e` | as-is | Content unchanged. Supporting files (AGENT-BRIEF.md, OUT-OF-SCOPE.md) included. |
| `xuan-to-issues` | mattpocock/skills | `to-issues` | `ff3ee1d` | as-is | Content unchanged. |
| `xuan-to-prd` | mattpocock/skills | `to-prd` | `aaf2453` | as-is | Content unchanged. |
| `xuan-zoom-out` | mattpocock/skills | `zoom-out` | `7afa86d` | as-is | Content unchanged. |

### Category: 06-communicate

| xuan Skill | Source Repo | Source Skill | Source File Commit | Status | Changes |
|---|---|---|---|---|---|
| `xuan-caveman` | mattpocock/skills | `caveman` | `62f43a1` | as-is | Content unchanged. |
| `xuan-handoff` | mattpocock/skills | `handoff` | `d54c497` | as-is | Content unchanged. |

### Source Skills Not Ported

| Source Repo | Source Skill | Reason |
|---|---|---|
| obra/superpowers | `using-superpowers` | Not needed. Skill discovery described in CONTEXT.md. |
| obra/superpowers | `writing-skills` | Replaced by matt's lighter `write-a-skill`. |
| mattpocock/skills | deprecated/* | Deprecated by upstream, not ported. |
| mattpocock/skills | in-progress/* | Incomplete, not ported. |
| mattpocock/skills | misc/* | Too niche / personal, not ported. |
| mattpocock/skills | personal/* | Personal to Matt, not ported. |

## Fusion Details

### xuan-design (brainstorm + grill-with-docs)

**Process flow:**

```
Phase 1: 探索 + 需求澄清
  探索项目上下文
  检查 CONTEXT.md (已有术语)
  需求问题 (一次一个)
  [遇到模糊词 → 即时术语对齐 → 写 CONTEXT.md 更新]

Phase 2: 方案探索
  提 2-3 方案 + 推荐
  Grill 方案分支 (压力测试选择)

Phase 3: 决策固化
  [确认方案]
  [ADR — 仅当 hard-to-reverse / surprising / 真实权衡]
  [写 CONTEXT.md 更新 (非实现细节术语)]

Phase 4: 设计呈现 + 批准
  逐节呈现设计
  用户逐节确认
  写 spec
  self-review spec
  用户 review spec

Phase 5: 过渡
  transition to xuan-writing-plans
```

**Key design decisions:**
- Terminology alignment happens iteratively during Phase 1, not upfront (avoids premature glossary work before scope is known).
- Grilling happens on chosen scheme branches (Phase 2), not on all possible decisions. Termination condition: user cannot clarify further or says "enough."
- ADR written after decision confirmed (Phase 3), not mid-grilling.
- Design approval gate before spec writing (Phase 4), inherited from brainstorming's hard gate.

### xuan-tdd (test-driven-development + tdd)

**Superpowers content retained (as-is):**
- Overview + core principle
- When to Use (always, exceptions ask human)
- Iron Law: no production code without failing test first + delete code written before test
- RED: Write failing test (good/bad examples)
- Verify RED: mandatory, watch it fail
- GREEN: Minimal code (good/bad examples)
- Verify GREEN: mandatory, watch it pass
- REFACTOR: Clean up (extended with matt signals)
- Why Order Matters (5 essays)
- Common Rationalizations table (11 rows)
- Red Flags list (13 items)
- Bug fix example (complete walkthrough)
- Verification Checklist (8 items)
- When Stuck table (4 rows)
- Debugging Integration section
- Testing Anti-Patterns reference
- Final Rule
- `testing-anti-patterns.md` supporting file
- Doc output path: `docs/ai-traces/specs/` (specs), `docs/ai-traces/plans/` (plans)

**Matt content added:**
- Phase 0: Planning (confirm API changes, identify deep modules, design for testability)
- Tracer Bullet philosophy: one test → one impl, anti horizontal slicing
- `interface-design.md` — dependency injection, return results not side effects, small surface
- `mocking.md` — mock only at system boundaries (external APIs/DB/time/fs), never own code
- `tests.md` — integration-style, test public API, anti private-method testing, anti call-order assertions, one logical assertion per test
- `deep-modules.md` — Ousterhout: small interface + large implementation = deep; large interface + little logic = shallow
- `refactoring.md` — refactoring signals: duplication, long methods, shallow modules, feature envy, primitive obsession

**Removed:** None. All superpowers content preserved, only supplemented.

## Resolved Decisions (from grill session 2026-06-07)

1. `xuan-diagnose` vs `xuan-systematic-debugging` — both kept, **content untouched** from originals. Different use cases: diagnose for fast-feedback bugs, systematic-debugging for complex multi-layer investigations.

2. `xuan-write-a-skill` — **matt `write-a-skill` only**, lightweight version. No superpowers TDD-driven methodology, no CSO, no anti-Rationalization table, no skill type classification.

3. **CONTEXT.md** — created. Follows mattpocock-skills format (definition + Avoid + relationships + flagged ambiguities). Key terms: Skill, Spec, Plan, ADR, Tracer bullet, Triage, Deep module, Iron law.

4. **Release workflow** — upstream commit tracking only (`auto-track` strategy). Repo created at `github.com/Cosss7/xuan-skills`, public. Published via `npx skills add Cosss7/xuan-skills`.

5. **Doc path**: `docs/ai-traces/specs/` and `docs/ai-traces/plans/` (replaces superpowers' `docs/superpowers/`).

6. **Worktree isolation** — `xuan-using-git-worktrees` retained as optional tool skill, not required by any workflow. `xuan-subagent-driven-development` and `xuan-executing-plans` no longer list it as a required workflow skill. Users invoke manually when isolation is needed.

## Architecture Constraints

- **Platform**: skills.sh. No plugin.json. Flat `SKILL.md` in category subdirectories.
- **Compatibility**: Must work with `npx skills add <owner>/xuan-skills`.
- **Cross-references**: Skills reference each other via `**REQUIRED SUB-SKILL:** Use xuan-<name>` or `**REQUIRED BACKGROUND:**` markers (not `@` force-load syntax).
- **Supporting files**: Heavy references and reusable scripts go in separate files next to SKILL.md. Code examples < 50 lines stay inline.
