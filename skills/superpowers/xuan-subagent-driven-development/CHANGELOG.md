# Changelog: xuan-subagent-driven-development

## Upstream Source

**Source:** `obra/superpowers/skills/subagent-driven-development` — commit `f2cbfbe`

## Changes from Upstream

### Removed: `using-git-worktrees` from required workflow skills

**Context:** The original skill listed `superpowers:using-git-worktrees` as a required workflow skill, meaning a worktree was automatically created before execution. After discussion, the team decided worktree isolation should be optional — users invoke `xuan-using-git-worktrees` manually when they need it.

**Change:** Removed the line `- **superpowers:using-git-worktrees** - Ensures isolated workspace (creates one or verifies existing)` from the Integration section.

### Updated: Cross-references

- `superpowers:writing-plans` → `xuan-writing-plans`
- `superpowers:executing-plans` → `xuan-executing-plans`
- `superpowers:test-driven-development` → `xuan-tdd`
- `superpowers:requesting-code-review` → `xuan-requesting-code-review`
- `superpowers:finishing-a-development-branch` → `xuan-finishing-a-development-branch`
- `superpowers:verification-before-completion` → `xuan-verification-before-completion`

### Updated: Paths

- `docs/superpowers/plans/` → `docs/ai-traces/plans/`
- `~/.config/superpowers` → `~/.config/xuan`

### Updated: Frontmatter name

- `name: subagent-driven-development` → `name: xuan-subagent-driven-development`

### Not Changed

- Implementer prompt templates (`implementer-prompt.md`, `spec-reviewer-prompt.md`, `code-quality-reviewer-prompt.md`) — no cross-refs to update
- All process flow, diagrams, and workflow logic
- Model selection guidance
- Red flags and quality gates
