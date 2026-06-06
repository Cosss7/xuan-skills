# xuan-skills Design Spec

> Author: xuan (via grill-with-docs session)
> Date: 2026-06-07

## Overview

Combine two skill repositories (mattpocock/skills and obra/superpowers) into a single curated collection, published to skills.sh. Retain the best of each — superpowers' discipline and rigor, mattpocock's architectural depth and engineering workflow — under a unified `xuan-` prefix.

## Upstream Sources

Future sync should diff against these commits:

| Repository | Remote | Commit SHA |
|---|---|---|
| mattpocock/skills | `git@github.com:mattpocock/skills.git` | `aaf2453fbdfe7a15c07f11d861224f34ab4b53cb` |
| obra/superpowers | `git@github.com:obra/superpowers.git` | `6fd4507659784c351abbd2bc264c7162cfd386dc` |

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

### Category: 01-foundation

| Skill | Origin | Notes |
|---|---|---|
| `xuan-setup` | matt `setup-matt-pocock-skills` | Renamed. Seeds for issue-tracker, triage-labels, domain config. |
| `xuan-write-a-skill` | matt `write-a-skill` | Lightweight structure. Not TDD-driven. |

### Category: 02-design

| Skill | Origin | Notes |
|---|---|---|
| `xuan-design` | **FUSION**: brainstorm + grill-with-docs | New design. See flow below. |
| `xuan-grill-with-docs` | matt `grill-with-docs` | Preserved as-is. For pure terminology alignment. |
| `xuan-grill-me` | matt `grill-me` | Preserved as-is. Non-code variant. |
| `xuan-writing-plans` | superpowers `writing-plans` | Preserved as-is. |
| `xuan-prototype` | matt `prototype` | Preserved as-is. |

### Category: 03-implement

| Skill | Origin | Notes |
|---|---|---|
| `xuan-tdd` | **FUSION**: superpowers `test-driven-development` + matt `tdd` | Superpowers iron law + rationalization table + verification gates. Matt interface-design/mocking/tests/deep-modules/refactoring as supporting files. Tracer bullet 4-phase flow. |
| `xuan-using-git-worktrees` | superpowers `using-git-worktrees` | As-is. |
| `xuan-subagent-driven-development` | superpowers `subagent-driven-development` | As-is. |
| `xuan-executing-plans` | superpowers `executing-plans` | As-is. |
| `xuan-dispatching-parallel-agents` | superpowers `dispatching-parallel-agents` | As-is. |

### Category: 04-quality

| Skill | Origin | Notes |
|---|---|---|
| `xuan-requesting-code-review` | superpowers `requesting-code-review` | As-is. |
| `xuan-receiving-code-review` | superpowers `receiving-code-review` | As-is. |
| `xuan-verification-before-completion` | superpowers `verification-before-completion` | As-is. |
| `xuan-finishing-a-development-branch` | superpowers `finishing-a-development-branch` | As-is. |

### Category: 05-maintain

| Skill | Origin | Notes |
|---|---|---|
| `xuan-diagnose` | matt `diagnose` | As-is. 6-phase loop, HITL script. For fast feedback bugs. |
| `xuan-systematic-debugging` | superpowers `systematic-debugging` | As-is. 4-phase + multi-layer tracing. For complex bugs. |
| `xuan-improve-codebase-architecture` | matt `improve-codebase-architecture` | As-is. HTML report, deepening candidates. |
| `xuan-triage` | matt `triage` | As-is. Issue state machine. |
| `xuan-to-issues` | matt `to-issues` | As-is. Vertical-slice issue breakdown. |
| `xuan-to-prd` | matt `to-prd` | As-is. |
| `xuan-zoom-out` | matt `zoom-out` | As-is. One-paragraph skill. |

### Category: 06-communicate

| Skill | Origin | Notes |
|---|---|---|
| `xuan-caveman` | matt `caveman` | As-is. |
| `xuan-handoff` | matt `handoff` | As-is. |

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

## Remaining Decisions (not yet discussed)

These were identified during grilling but deferred:

1. `xuan-diagnose` vs `xuan-systematic-debugging` — both kept, but exact boundary/overlap resolution deferred
2. `xuan-write-a-skill` — exact contents and whether to adopt any of writing-skills' TDD methodology
3. CONTEXT.md for this repo — what domain terms need definition
4. Release workflow — versioning, CHANGELOG, sync process from upstream

## Architecture Constraints

- **Platform**: skills.sh. No plugin.json. Flat `SKILL.md` in category subdirectories.
- **Compatibility**: Must work with `npx skills add <owner>/xuan-skills`.
- **Cross-references**: Skills reference each other via `**REQUIRED SUB-SKILL:** Use xuan-<name>` or `**REQUIRED BACKGROUND:**` markers (not `@` force-load syntax).
- **Supporting files**: Heavy references and reusable scripts go in separate files next to SKILL.md. Code examples < 50 lines stay inline.
