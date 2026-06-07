# Changelog: xuan-using-git-worktrees

## Upstream Source

**Source:** `obra/superpowers/skills/using-git-worktrees` — commit `f2cbfbe`

## Changes from Upstream

### Updated: Config paths

- `~/.config/superpowers/worktrees/` → `~/.config/xuan/worktrees/`

### Updated: Frontmatter name

- `name: using-git-worktrees` → `name: xuan-using-git-worktrees`

### Not Changed

- All detection logic (Step 0: existing isolation check, submodule guard)
- Creation order (native tools → git fallback)
- Directory priority logic
- Safety verification (git check-ignore)
- Baseline test verification
- All red flags and common mistakes
