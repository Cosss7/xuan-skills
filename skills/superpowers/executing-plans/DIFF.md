# Changelog: executing-plans

## Upstream Source

**Source:** `obra/superpowers/skills/executing-plans` — commit `f2cbfbe`

## Changes from Upstream

### Removed: `using-git-worktrees` from required workflow skills

**Context:** Same decision as `subagent-driven-development`. Worktree isolation is optional, not automatic.

**Change:** Removed `- **superpowers:using-git-worktrees** - Ensures isolated workspace (creates one or verifies existing)` from the Integration section.

### Updated: Cross-references

- `superpowers:subagent-driven-development` → `subagent-driven-development`
- `superpowers:writing-plans` → `writing-plans`
- `superpowers:finishing-a-development-branch` → `finishing-a-development-branch`

### Updated: Frontmatter name

- `name: executing-plans` → `name: executing-plans`

### Not Changed

- All process flow, verification steps, and stopping criteria
