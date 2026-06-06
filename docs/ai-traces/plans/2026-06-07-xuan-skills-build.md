# xuan-skills Build Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build and publish the xuan-skills repository — 25 curated skills from mattpocock/skills and obra/superpowers.

**Plan note:** xuan skills don't exist yet, so execution uses current `superpowers:subagent-driven-development` or `superpowers:executing-plans`. Cross-refs point to `xuan-` names; update paths as needed during execution.

**Architecture:** Flat SKILL.md-based skills organized into 6 lifecycle categories under `skills/`. Published via skills.sh. No plugin.json.

**Tech Stack:** SKILL.md files with YAML frontmatter. Some TypeScript/Shell examples inline. Git + GitHub for distribution.

**Upstream repos:**
- `../mattpocock-skills` at `aaf2453`
- `../superpowers` at `6fd4507`

---

## Phase 1: Scaffolding

### Task 1: Create directory structure

**Files:**
- Create: `skills/01-foundation/.gitkeep`
- Create: `skills/02-design/.gitkeep`
- Create: `skills/03-implement/.gitkeep`
- Create: `skills/04-quality/.gitkeep`
- Create: `skills/05-maintain/.gitkeep`
- Create: `skills/06-communicate/.gitkeep`

- [ ] **Step 1: Create category directories**

```bash
mkdir -p skills/0{1,2,3,4,5,6}-{foundation,design,implement,quality,maintain,communicate}
touch skills/01-foundation/.gitkeep
touch skills/02-design/.gitkeep
touch skills/03-implement/.gitkeep
touch skills/04-quality/.gitkeep
touch skills/05-maintain/.gitkeep
touch skills/06-communicate/.gitkeep
```

- [ ] **Step 2: Create .gitignore**

```gitignore
# OS
.DS_Store
Thumbs.db

# Editor
*.swp
*.swo
*~

# Temp
tmp/
```

- [ ] **Step 3: Commit**

```bash
git add skills/ .gitignore
git commit -m "chore: scaffold category directories"
```

---

### Task 2: Create CLAUDE.md

**Files:**
- Create: `CLAUDE.md`

- [ ] **Step 1: Write CLAUDE.md**

```markdown
# xuan-skills

A curated collection of AI agent skills. Published via skills.sh.

## Structure

- `skills/<category>/<skill-name>/SKILL.md` — one skill per directory
- Category: lifecycle phase (01-foundation → 06-communicate)
- Supporting files next to SKILL.md if needed

## Cross-Referencing

- **REQUIRED SUB-SKILL:** Use `xuan-<name>` — when another skill must run first
- **REQUIRED BACKGROUND:** You MUST understand `xuan-<name>` — prerequisite knowledge
- Never use `@` force-load syntax (burns context)

## Doc Output

- Specs: `docs/ai-traces/specs/`
- Plans: `docs/ai-traces/plans/`
- ADRs: `docs/ai-traces/adr/`
```

- [ ] **Step 2: Commit**

```bash
git add CLAUDE.md
git commit -m "chore: add CLAUDE.md with conventions"
```

---

## Phase 2: Foundation Skills

### Task 3: Create xuan-write-a-skill

**Source:** `../mattpocock-skills/skills/productivity/write-a-skill/SKILL.md` at `62f43a1`

**Files:**
- Create: `skills/01-foundation/xuan-write-a-skill/SKILL.md`

- [ ] **Step 1: Copy source SKILL.md**

```bash
cp ../mattpocock-skills/skills/productivity/write-a-skill/SKILL.md skills/01-foundation/xuan-write-a-skill/SKILL.md
```

- [ ] **Step 2: Update frontmatter name**

Replace `name: write-a-skill` with `name: xuan-write-a-skill`.

- [ ] **Step 3: Commit**

```bash
git add skills/01-foundation/xuan-write-a-skill/
git commit -m "feat: add xuan-write-a-skill from mattpocock"
```

---

### Task 4: Create xuan-setup (modified)

**Source:** `../mattpocock-skills/skills/engineering/setup-matt-pocock-skills/SKILL.md` at `4369256`

**Supporting files from source:**
- `issue-tracker-github.md`
- `issue-tracker-gitlab.md`
- `issue-tracker-local.md`
- `triage-labels.md`
- `domain.md`

**Files:**
- Create: `skills/01-foundation/xuan-setup/SKILL.md`
- Create: `skills/01-foundation/xuan-setup/issue-tracker-github.md`
- Create: `skills/01-foundation/xuan-setup/issue-tracker-gitlab.md`
- Create: `skills/01-foundation/xuan-setup/issue-tracker-local.md`
- Create: `skills/01-foundation/xuan-setup/triage-labels.md`
- Create: `skills/01-foundation/xuan-setup/domain.md`

- [ ] **Step 1: Copy supporting files (unchanged)**

```bash
SKILL_DIR=skills/01-foundation/xuan-setup
mkdir -p "$SKILL_DIR"
for f in issue-tracker-github.md issue-tracker-gitlab.md issue-tracker-local.md triage-labels.md domain.md; do
  cp "../mattpocock-skills/skills/engineering/setup-matt-pocock-skills/$f" "$SKILL_DIR/$f"
done
```

- [ ] **Step 2: Copy and edit SKILL.md**

```
cp ../mattpocock-skills/skills/engineering/setup-matt-pocock-skills/SKILL.md skills/01-foundation/xuan-setup/SKILL.md
```

Changes to make in SKILL.md:
- `name:` field → `xuan-setup`
- Remove all references to "Matt Pocock" / "mattpocock"
- Update repo references from `mattpocock/skills` to `Cosss7/xuan-skills`
- Update skill names from `/setup-matt-pocock-skills` to `/xuan-setup`
- Update doc paths from `docs/agents/` to `docs/ai-traces/` (or keep agents/? tbd)
- Output config files still go to `docs/agents/` (project-level, not repo-level)

- [ ] **Step 3: Commit**

```bash
git add skills/01-foundation/xuan-setup/
git commit -m "feat: add xuan-setup from mattpocock/setup-matt-pocock-skills"
```

---

## Phase 3: Design Skills

### Task 5: Create xuan-grill-with-docs

**Source:** `../mattpocock-skills/skills/engineering/grill-with-docs/SKILL.md` at `e74f006`

**Supporting files:**
- `ADR-FORMAT.md`
- `CONTEXT-FORMAT.md`

- [ ] **Step 1: Copy all files**

```bash
SKILL_DIR=skills/02-design/xuan-grill-with-docs
mkdir -p "$SKILL_DIR"
cp ../mattpocock-skills/skills/engineering/grill-with-docs/*.md "$SKILL_DIR/"
```

- [ ] **Step 2: Update frontmatter name**

Replace `name: grill-with-docs` with `name: xuan-grill-with-docs`.

- [ ] **Step 3: Commit**

```bash
git add skills/02-design/xuan-grill-with-docs/
git commit -m "feat: add xuan-grill-with-docs"
```

---

### Task 6: Create xuan-grill-me

**Source:** `../mattpocock-skills/skills/productivity/grill-me/SKILL.md` at `62f43a1`

- [ ] **Step 1: Copy and update**

```bash
SKILL_DIR=skills/02-design/xuan-grill-me
mkdir -p "$SKILL_DIR"
cp ../mattpocock-skills/skills/productivity/grill-me/SKILL.md "$SKILL_DIR/"
```

Replace `name: grill-me` with `name: xuan-grill-me`.

- [ ] **Step 2: Commit**

```bash
git add skills/02-design/xuan-grill-me/
git commit -m "feat: add xuan-grill-me"
```

---

### Task 7: Create xuan-prototype

**Source:** `../mattpocock-skills/skills/engineering/prototype/` at `f304057`

**Supporting files:** `LOGIC.md`, `UI.md`

- [ ] **Step 1: Copy all files**

```bash
SKILL_DIR=skills/02-design/xuan-prototype
mkdir -p "$SKILL_DIR"
cp ../mattpocock-skills/skills/engineering/prototype/*.md "$SKILL_DIR/"
```

Update SKILL.md name to `xuan-prototype`.

- [ ] **Step 2: Commit**

```bash
git add skills/02-design/xuan-prototype/
git commit -m "feat: add xuan-prototype"
```

---

### Task 8: Create xuan-writing-plans

**Source:** `../superpowers/skills/writing-plans/SKILL.md` at `f2cbfbe`

- [ ] **Step 1: Copy and update**

```bash
SKILL_DIR=skills/02-design/xuan-writing-plans
mkdir -p "$SKILL_DIR"
cp ../superpowers/skills/writing-plans/SKILL.md "$SKILL_DIR/"
```

Changes:
- `name:` → `xuan-writing-plans`
- Doc output path: `docs/superpowers/plans/` → `docs/ai-traces/plans/`
- `superpowers:using-git-worktrees` refs → `xuan-using-git-worktrees`
- `superpowers:writing-plans` refs → `xuan-writing-plans`
- `superpowers:subagent-driven-development` → `xuan-subagent-driven-development`
- `superpowers:executing-plans` → `xuan-executing-plans`
- `superpowers:finishing-a-development-branch` → `xuan-finishing-a-development-branch`
- `superpowers:test-driven-development` → `xuan-tdd`
- `superpowers:requesting-code-review` → `xuan-requesting-code-review`

- [ ] **Step 2: Commit**

```bash
git add skills/02-design/xuan-writing-plans/
git commit -m "feat: add xuan-writing-plans from superpowers"
```

---

### Task 9: Create xuan-design (NEW — fused skill)

**Source:** brainstorm (`3f80f1c`) + grill-with-docs (`e74f006`) design from spec

- [ ] **Step 1: Write SKILL.md**

```markdown
---
name: xuan-design
description: Use before any creative work — exploring user intent, aligning terminology, grilling decision branches, and producing a spec before implementation. Combines brainstorming's design flow with grill-with-docs' terminology alignment and ADR creation.
---

# xuan-design — Design Through Shared Understanding

## Overview

Turn fuzzy ideas into fully-formed specs through a disciplined 5-phase process. Align terminology, grill decision branches, capture architecture decisions, and produce a written spec before any implementation.

**Core principle:** Design is an iterative dialogue, not a document. Write decisions down only after shared understanding is reached.

**Hard gate:** Do NOT invoke any implementation skill, write any code, scaffold any project, or take any implementation action until the design is approved in Phase 4 and a spec is written.

## When to Use

**Always before:**
- New features or components
- Architecture changes
- Workflow changes
- Any implementation task

**Exceptions (ask your human partner):**
- Throwaway prototypes (use xuan-prototype instead)
- Bug fixes with clear reproduction

## Phase 1: Explore + Clarify Requirements

1. **Explore project context** — read files, docs, recent commits, existing CONTEXT.md
2. **Ask clarifying questions** — one at a time, understand purpose, constraints, success criteria
   - Prefer multiple choice when possible
   - If scope is too large for one spec, flag it: break into sub-projects
3. **Terminology alignment (iterative)** — when the user uses a fuzzy or loaded term:
   - Propose a precise canonical term
   - Check against existing CONTEXT.md glossary
   - If resolved, update CONTEXT.md immediately
4. **Visual companion** — if upcoming questions benefit from visual treatment (mockups, diagrams, layouts), offer a browser companion. One message, nothing else. Wait for consent.

## Phase 2: Explore Approaches

1. Propose 2-3 different approaches with trade-offs
2. Lead with your recommended option and reasoning
3. **Grill the chosen branch(es):**
   - Stress-test with concrete scenarios
   - Probe edge cases that force precision about boundaries
   - Cross-reference stated intent against actual code
   - Stop when user cannot clarify further or says "enough"

## Phase 3: Solidify Decisions

1. User confirms the chosen approach
2. **ADR (only when all three are true):**
   - Hard to reverse
   - Surprising without context
   - Result of a real trade-off with genuine alternatives
   - Use: `docs/ai-traces/adr/YYYY-MM-DD-title.md`
3. Update CONTEXT.md with any new resolved terms (not implementation details)

## Phase 4: Present Design + Approve

1. Present design section by section. Scale each section to its complexity.
   - Cover: architecture, components, data flow, error handling, testing
2. Ask after each section: "Does this look right?"
3. After all sections are approved: write the spec to `docs/ai-traces/specs/YYYY-MM-DD-topic-design.md`
4. **Spec self-review:**
   - Placeholder scan: any TBD, TODO, incomplete sections?
   - Internal consistency: do sections contradict each other?
   - Scope check: focused enough for one implementation plan?
   - Ambiguity check: could any requirement be read two ways?
5. Ask user to review the written spec. Wait for approval.

## Phase 5: Transition to Implementation

1. Invoke `xuan-writing-plans` to create a detailed implementation plan
2. Do NOT invoke any implementation skill directly

## Key Principles

- **One question at a time** — don't overwhelm
- **Terminology first** — shared language prevents wasted design
- **YAGNI ruthlessly** — strip unnecessary features
- **Alternatives before commitment** — 2-3 approaches, not one
- **Grill don't guess** — stress-test decisions with concrete scenarios
- **ADR sparingly** — only when hard to reverse, surprising, or a real trade-off
- **Design gate** — no code before approved design

## Visual Companion

When visual questions are ahead (mockups, layouts, diagrams, comparisons), offer the browser companion:

> "Some of what we're working on might be easier to explain if I can show it to you in a web browser. I can put together mockups, diagrams, comparisons, and other visuals as we go. Want to try it? (Requires opening a local URL)"

This offer MUST be its own message. Wait for response. If declined, proceed text-only.

## Red Flags — STOP

- Writing code before design approval
- Skipping terminology alignment ("we all know what X means")
- Proposing only one approach
- Skipping ADR for a hard-to-reverse decision
- Writing spec while still unclear about requirements
- Moving to implementation without user approving the written spec

**These all mean: Go back to Phase 1 or Phase 2. Don't proceed.**
```

- [ ] **Step 2: Commit**

```bash
git add skills/02-design/xuan-design/
git commit -m "feat: add xuan-design (brainstorm + grill-with-docs fusion)"
```

---

## Phase 4: Implement Skills

### Task 10: Create xuan-tdd (FUSED — with supporting files)

**Primary source:** `../superpowers/skills/test-driven-development/SKILL.md` at `030a222`
**Matt supporting files:** `../mattpocock-skills/skills/engineering/tdd/` at `7afa86d`

**Files to create:**
- `skills/03-implement/xuan-tdd/SKILL.md` (fused content)
- `skills/03-implement/xuan-tdd/testing-anti-patterns.md` (from superpowers)
- `skills/03-implement/xuan-tdd/interface-design.md` (from matt)
- `skills/03-implement/xuan-tdd/mocking.md` (from matt)
- `skills/03-implement/xuan-tdd/tests.md` (from matt)
- `skills/03-implement/xuan-tdd/deep-modules.md` (from matt)
- `skills/03-implement/xuan-tdd/refactoring.md` (from matt)

- [ ] **Step 1: Copy supporting files (unchanged)**

```bash
SKILL_DIR=skills/03-implement/xuan-tdd
mkdir -p "$SKILL_DIR"

# Superpowers anti-patterns
cp ../superpowers/skills/test-driven-development/testing-anti-patterns.md "$SKILL_DIR/"

# Matt supporting files
for f in interface-design.md mocking.md tests.md deep-modules.md refactoring.md; do
  cp "../mattpocock-skills/skills/engineering/tdd/$f" "$SKILL_DIR/$f"
done
```

- [ ] **Step 2: Write fused SKILL.md**

Start from `../superpowers/skills/test-driven-development/SKILL.md` content. Retain ALL superpowers content. Add the following changes:

**Frontmatter:**
```yaml
---
name: xuan-tdd
description: Use when implementing any feature or bugfix, before writing implementation code
---
```

**After "## When to Use" section, insert Phase 0: Planning:**

```markdown
## Planning Phase (Before RED)

Before writing the first test, confirm with your human partner:

1. **Interface changes** — what types, functions, or config shapes change?
2. **Behaviors to test** — list them in priority order
3. **Deep module opportunities** — can the new code present a small interface
   while hiding complexity? (See deep-modules.md)
4. **Testability design** — accept dependencies via parameters, return results
   not side effects, keep surface area small (See interface-design.md)
5. **User approval** — confirm the plan before writing tests
```

**Replace the "Red-Green-Refactor" section heading and diagram to include tracer bullet philosophy:**

After the existing Red-Green-Refactor cycle diagram and sections, add:

```markdown
### Tracer Bullet Rhythm

Build features one vertical slice at a time:

1. Write ONE test for ONE behavior (not all tests at once)
2. RED → Verify → GREEN → Verify → REFACTOR
3. Write the next test for the next behavior
4. Repeat

**Anti-pattern — Horizontal slicing:** Writing all tests first, then all
implementation. This delays feedback and encourages testing implementation
details instead of behavior. One test → one implementation → repeat.
```

**Update REFACTOR section to reference deep-modules.md and refactoring.md:**

After the existing REFACTOR paragraph, add:

```markdown
After GREEN, check for refactoring signals (see refactoring.md):
- Duplication, long methods, shallow modules
- Feature envy, primitive obsession

Prefer deep modules: small interface + rich implementation.
See deep-modules.md for the full concept.
```

**Update "When Stuck" table row 3:**

```
Before: "Must mock everything | Code too coupled. Use dependency injection."
After:  "Must mock everything | Code too coupled. See interface-design.md for dependency injection patterns. See mocking.md for what to mock (only system boundaries)."
```

**Update cross-references:**
- `@testing-anti-patterns.md` → keep (same directory)
- Remove `superpowers:` prefix from any refs

- [ ] **Step 3: Commit**

```bash
git add skills/03-implement/xuan-tdd/
git commit -m "feat: add xuan-tdd (superpowers + matt fusion)"
```

---

### Task 11: Create xuan-using-git-worktrees

**Source:** `../superpowers/skills/using-git-worktrees/SKILL.md` at `f2cbfbe`

- [ ] **Step 1: Copy and update**

```bash
SKILL_DIR=skills/03-implement/xuan-using-git-worktrees
mkdir -p "$SKILL_DIR"
cp ../superpowers/skills/using-git-worktrees/SKILL.md "$SKILL_DIR/"
```

Changes:
- `name:` → `xuan-using-git-worktrees`
- `~/.config/superpowers/worktrees/` → `~/.config/xuan/worktrees/`
- `superpowers:test-driven-development` → `xuan-tdd`
- Remove `xuan:using-superpowers` ref if present

- [ ] **Step 2: Commit**

```bash
git add skills/03-implement/xuan-using-git-worktrees/
git commit -m "feat: add xuan-using-git-worktrees"
```

---

### Task 12: Create xuan-subagent-driven-development (modified)

**Source:** `../superpowers/skills/subagent-driven-development/SKILL.md` at `f2cbfbe`

**Supporting files:** `implementer-prompt.md`, `spec-reviewer-prompt.md`, `code-quality-reviewer-prompt.md`

- [ ] **Step 1: Copy all files**

```bash
SKILL_DIR=skills/03-implement/xuan-subagent-driven-development
mkdir -p "$SKILL_DIR"
cp ../superpowers/skills/subagent-driven-development/*.md "$SKILL_DIR/"
```

- [ ] **Step 2: Update SKILL.md**

Changes:
- `name:` → `xuan-subagent-driven-development`
- Remove `superpowers:using-git-worktrees` from Required workflow skills (worktree is optional, not required)
- Update cross-refs: `superpowers:writing-plans` → `xuan-writing-plans`, `superpowers:test-driven-development` → `xuan-tdd`, `superpowers:requesting-code-review` → `xuan-requesting-code-review`, `superpowers:finishing-a-development-branch` → `xuan-finishing-a-development-branch`
- Update `docs/superpowers/plans/` → `docs/ai-traces/plans/`

- [ ] **Step 3: Commit**

```bash
git add skills/03-implement/xuan-subagent-driven-development/
git commit -m "feat: add xuan-subagent-driven-development, remove required worktree dep"
```

---

### Task 13: Create xuan-executing-plans (modified)

**Source:** `../superpowers/skills/executing-plans/SKILL.md` at `f2cbfbe`

- [ ] **Step 1: Copy and update**

```bash
SKILL_DIR=skills/03-implement/xuan-executing-plans
mkdir -p "$SKILL_DIR"
cp ../superpowers/skills/executing-plans/SKILL.md "$SKILL_DIR/"
```

Changes:
- `name:` → `xuan-executing-plans`
- Remove `superpowers:using-git-worktrees` from required workflow skills
- Update cross-refs: `superpowers:subagent-driven-development` → `xuan-subagent-driven-development`, `superpowers:finishing-a-development-branch` → `xuan-finishing-a-development-branch`, `superpowers:writing-plans` → `xuan-writing-plans`

- [ ] **Step 2: Commit**

```bash
git add skills/03-implement/xuan-executing-plans/
git commit -m "feat: add xuan-executing-plans, remove required worktree dep"
```

---

### Task 14: Create xuan-dispatching-parallel-agents

**Source:** `../superpowers/skills/dispatching-parallel-agents/SKILL.md` at `9ccce3b`

- [ ] **Step 1: Copy and update**

```bash
SKILL_DIR=skills/03-implement/xuan-dispatching-parallel-agents
mkdir -p "$SKILL_DIR"
cp ../superpowers/skills/dispatching-parallel-agents/SKILL.md "$SKILL_DIR/"
```

Change `name:` to `xuan-dispatching-parallel-agents`.

- [ ] **Step 2: Commit**

```bash
git add skills/03-implement/xuan-dispatching-parallel-agents/
git commit -m "feat: add xuan-dispatching-parallel-agents"
```

---

## Phase 5: Quality Skills

### Task 15: Create xuan-requesting-code-review

**Source:** `../superpowers/skills/requesting-code-review/SKILL.md` at `f2cbfbe`

- [ ] **Step 1: Copy and update**

```bash
SKILL_DIR=skills/04-quality/xuan-requesting-code-review
mkdir -p "$SKILL_DIR"
cp ../superpowers/skills/requesting-code-review/SKILL.md "$SKILL_DIR/"
```

Update name and cross-refs (`superpowers:test-driven-development` → `xuan-tdd`).

- [ ] **Step 2: Commit**

```bash
git add skills/04-quality/xuan-requesting-code-review/
git commit -m "feat: add xuan-requesting-code-review"
```

---

### Task 16: Create xuan-receiving-code-review

**Source:** `../superpowers/skills/receiving-code-review/SKILL.md` at `1455ac0`

- [ ] **Step 1: Copy and update**

```bash
SKILL_DIR=skills/04-quality/xuan-receiving-code-review
mkdir -p "$SKILL_DIR"
cp ../superpowers/skills/receiving-code-review/SKILL.md "$SKILL_DIR/"
```

Update name only.

- [ ] **Step 2: Commit**

```bash
git add skills/04-quality/xuan-receiving-code-review/
git commit -m "feat: add xuan-receiving-code-review"
```

---

### Task 17: Create xuan-verification-before-completion

**Source:** `../superpowers/skills/verification-before-completion/SKILL.md` at `48410c7`

- [ ] **Step 1: Copy and update**

```bash
SKILL_DIR=skills/04-quality/xuan-verification-before-completion
mkdir -p "$SKILL_DIR"
cp ../superpowers/skills/verification-before-completion/SKILL.md "$SKILL_DIR/"
```

Update name and cross-refs (`superpowers:test-driven-development` → `xuan-tdd`).

- [ ] **Step 2: Commit**

```bash
git add skills/04-quality/xuan-verification-before-completion/
git commit -m "feat: add xuan-verification-before-completion"
```

---

### Task 18: Create xuan-finishing-a-development-branch

**Source:** `../superpowers/skills/finishing-a-development-branch/SKILL.md` at `f2cbfbe`

- [ ] **Step 1: Copy and update**

```bash
SKILL_DIR=skills/04-quality/xuan-finishing-a-development-branch
mkdir -p "$SKILL_DIR"
cp ../superpowers/skills/finishing-a-development-branch/SKILL.md "$SKILL_DIR/"
```

Changes:
- `name:` → `xuan-finishing-a-development-branch`
- `~/.config/superpowers/worktrees/` → `~/.config/xuan/worktrees/`
- Update any `superpowers:` cross-refs

- [ ] **Step 2: Commit**

```bash
git add skills/04-quality/xuan-finishing-a-development-branch/
git commit -m "feat: add xuan-finishing-a-development-branch"
```

---

## Phase 6: Maintain Skills

### Task 19: Create xuan-diagnose

**Source:** `../mattpocock-skills/skills/engineering/diagnose/` at `7afa86d`

**Supporting files:** `scripts/hitl-loop.template.sh`

- [ ] **Step 1: Copy all files**

```bash
SKILL_DIR=skills/05-maintain/xuan-diagnose
mkdir -p "$SKILL_DIR"
cp -r ../mattpocock-skills/skills/engineering/diagnose/* "$SKILL_DIR/"
```

Update `name:` to `xuan-diagnose`.

- [ ] **Step 2: Commit**

```bash
git add skills/05-maintain/xuan-diagnose/
git commit -m "feat: add xuan-diagnose"
```

---

### Task 20: Create xuan-systematic-debugging

**Source:** `../superpowers/skills/systematic-debugging/` at `030a222`

**Supporting files:** `root-cause-tracing.md`, `defense-in-depth.md`, `condition-based-waiting.md`, `condition-based-waiting-example.ts`, `find-polluter.sh`

- [ ] **Step 1: Copy files**

```bash
SKILL_DIR=skills/05-maintain/xuan-systematic-debugging
mkdir -p "$SKILL_DIR"
cp ../superpowers/skills/systematic-debugging/*.md "$SKILL_DIR/"
cp ../superpowers/skills/systematic-debugging/*.ts "$SKILL_DIR/" 2>/dev/null || true
cp ../superpowers/skills/systematic-debugging/*.sh "$SKILL_DIR/" 2>/dev/null || true
```

Update `name:` to `xuan-systematic-debugging` and cross-refs (`superpowers:test-driven-development` → `xuan-tdd`, `superpowers:verification-before-completion` → `xuan-verification-before-completion`).

- [ ] **Step 2: Commit**

```bash
git add skills/05-maintain/xuan-systematic-debugging/
git commit -m "feat: add xuan-systematic-debugging"
```

---

### Task 21: Create xuan-improve-codebase-architecture

**Source:** `../mattpocock-skills/skills/engineering/improve-codebase-architecture/` at `a36584e`

**Supporting files:** `LANGUAGE.md`, `DEEPENING.md`, `HTML-REPORT.md`, `INTERFACE-DESIGN.md`

- [ ] **Step 1: Copy all files**

```bash
SKILL_DIR=skills/05-maintain/xuan-improve-codebase-architecture
mkdir -p "$SKILL_DIR"
cp ../mattpocock-skills/skills/engineering/improve-codebase-architecture/*.md "$SKILL_DIR/"
```

Update `name:` to `xuan-improve-codebase-architecture`.

- [ ] **Step 2: Commit**

```bash
git add skills/05-maintain/xuan-improve-codebase-architecture/
git commit -m "feat: add xuan-improve-codebase-architecture"
```

---

### Task 22: Create xuan-triage

**Source:** `../mattpocock-skills/skills/engineering/triage/` at `179a14e`

**Supporting files:** `AGENT-BRIEF.md`, `OUT-OF-SCOPE.md`

- [ ] **Step 1: Copy all files**

```bash
SKILL_DIR=skills/05-maintain/xuan-triage
mkdir -p "$SKILL_DIR"
cp ../mattpocock-skills/skills/engineering/triage/*.md "$SKILL_DIR/"
```

Update `name:` to `xuan-triage`.

- [ ] **Step 2: Commit**

```bash
git add skills/05-maintain/xuan-triage/
git commit -m "feat: add xuan-triage"
```

---

### Task 23: Create xuan-to-issues

**Source:** `../mattpocock-skills/skills/engineering/to-issues/SKILL.md` at `ff3ee1d`

- [ ] **Step 1: Copy and update**

```bash
SKILL_DIR=skills/05-maintain/xuan-to-issues
mkdir -p "$SKILL_DIR"
cp ../mattpocock-skills/skills/engineering/to-issues/SKILL.md "$SKILL_DIR/"
```

Update `name:` to `xuan-to-issues`.

- [ ] **Step 2: Commit**

```bash
git add skills/05-maintain/xuan-to-issues/
git commit -m "feat: add xuan-to-issues"
```

---

### Task 24: Create xuan-to-prd

**Source:** `../mattpocock-skills/skills/engineering/to-prd/SKILL.md` at `aaf2453`

- [ ] **Step 1: Copy and update**

```bash
SKILL_DIR=skills/05-maintain/xuan-to-prd
mkdir -p "$SKILL_DIR"
cp ../mattpocock-skills/skills/engineering/to-prd/SKILL.md "$SKILL_DIR/"
```

Update `name:` to `xuan-to-prd`.

- [ ] **Step 2: Commit**

```bash
git add skills/05-maintain/xuan-to-prd/
git commit -m "feat: add xuan-to-prd"
```

---

### Task 25: Create xuan-zoom-out

**Source:** `../mattpocock-skills/skills/engineering/zoom-out/SKILL.md` at `7afa86d`

- [ ] **Step 1: Copy and update**

```bash
SKILL_DIR=skills/05-maintain/xuan-zoom-out
mkdir -p "$SKILL_DIR"
cp ../mattpocock-skills/skills/engineering/zoom-out/SKILL.md "$SKILL_DIR/"
```

Update `name:` to `xuan-zoom-out`.

- [ ] **Step 2: Commit**

```bash
git add skills/05-maintain/xuan-zoom-out/
git commit -m "feat: add xuan-zoom-out"
```

---

## Phase 7: Communicate Skills

### Task 26: Create xuan-caveman

**Source:** `../mattpocock-skills/skills/productivity/caveman/SKILL.md` at `62f43a1`

- [ ] **Step 1: Copy and update**

```bash
SKILL_DIR=skills/06-communicate/xuan-caveman
mkdir -p "$SKILL_DIR"
cp ../mattpocock-skills/skills/productivity/caveman/SKILL.md "$SKILL_DIR/"
```

Update `name:` to `xuan-caveman`.

- [ ] **Step 2: Commit**

```bash
git add skills/06-communicate/xuan-caveman/
git commit -m "feat: add xuan-caveman"
```

---

### Task 27: Create xuan-handoff

**Source:** `../mattpocock-skills/skills/productivity/handoff/SKILL.md` at `d54c497`

- [ ] **Step 1: Copy and update**

```bash
SKILL_DIR=skills/06-communicate/xuan-handoff
mkdir -p "$SKILL_DIR"
cp ../mattpocock-skills/skills/productivity/handoff/SKILL.md "$SKILL_DIR/"
```

Update `name:` to `xuan-handoff`.

- [ ] **Step 2: Commit**

```bash
git add skills/06-communicate/xuan-handoff/
git commit -m "feat: add xuan-handoff"
```

---

## Phase 8: Verify and Publish

### Task 28: Verify skills.sh discovery

- [ ] **Step 1: Count all SKILL.md files**

```bash
find skills -name "SKILL.md" | wc -l
# Expected: 25
```

- [ ] **Step 2: Validate all frontmatter**

```bash
# Check each SKILL.md has name and description
for f in $(find skills -name "SKILL.md"); do
  name=$(head -20 "$f" | grep "^name:" | head -1)
  desc=$(head -20 "$f" | grep "^description:" | head -1)
  if [ -z "$name" ] || [ -z "$desc" ]; then
    echo "MISSING: $f"
  fi
done
echo "Check complete"
```

- [ ] **Step 3: Check for stale superpowers: cross-references**

```bash
grep -r "superpowers:" skills/ --include="*.md" || echo "No stale superpowers refs"
```

- [ ] **Step 4: Push and verify install**

```bash
git push origin main
npx skills add Cosss7/xuan-skills --dry-run
```

- [ ] **Step 5: Fix any issues found in verification**

- [ ] **Step 6: Final commit if fixes needed**

```bash
git push origin main
```
