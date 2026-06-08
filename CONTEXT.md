# xuan-skills

A curated collection of agent skills combining discipline from obra/superpowers and engineering workflow from mattpocock/skills. All skills are prefixed with `xuan-` and organized into lifecycle categories under `skills/`.

Published via skills.sh. Installed with `npx skills add <owner>/xuan-skills`.

## Language

**Skill**:
A directory containing `SKILL.md` with YAML frontmatter (`name`, `description`) and optional supporting files. Skills provide procedural knowledge — techniques, patterns, workflows, and references — that agents load at runtime.
_Avoid_: plugin, addon, extension

**Spec**:
A design document written during `xuan-design` (Phase 4). Captures all decisions reached during the design process. Saved to `docs/ai-trace/specs/`.
_Avoid_: design doc, requirement doc

**Plan**:
An implementation plan produced by `xuan-writing-plans`, containing bite-sized tasks with exact file paths, code blocks, and commands. Each task is independently executable by an agent. Saved to `docs/ai-trace/plans/`.
_Avoid_: todo list, ticket breakdown

**ADR**:
Architecture Decision Record — a lightweight document capturing a hard-to-reverse, surprising, or trade-off-heavy decision. Created during `xuan-design` (Phase 3) or `xuan-grill-with-docs`. Saved to `docs/ai-trace/adr/`.
_Avoid_: design doc, decision log (prefer ADR explicitly)

**Tracer bullet**:
A vertical slice pattern where one test is written first, then the minimal implementation to pass it, then repeated for the next behavior. Prevents horizontal slicing (writing all tests first, then all implementation).
_Avoid_: vertical slice (term is valid but "tracer bullet" emphasizes the iterative discovery nature)

**Triage**:
The process of moving an issue through a state machine of categories (`bug`, `enhancement`) and states (`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`). Applied by the `xuan-triage` skill.
_Avoid_: issue sorting, ticket review

**Deep module**:
From Ousterhout's *A Philosophy of Software Design*. A module with a small interface and large implementation (good) — contrast with **shallow module** (large interface, little implementation).
_Avoid_: abstraction (too vague), layer

**Iron law**:
A non-negotiable rule enforced by a skill. Violating the letter is violating the spirit. Example: "No production code without a failing test first" in `xuan-tdd`.
_Avoid_: hard rule, strict policy

## Relationships

- A **Spec** is produced by `xuan-design` and consumed by `xuan-writing-plans`
- A **Plan** is produced by `xuan-writing-plans` and executed by `xuan-subagent-driven-development` or `xuan-executing-plans`
- An **ADR** is produced by `xuan-design` or `xuan-grill-with-docs` when a decision meets all three criteria: hard to reverse, surprising without context, real trade-off
- **TDD** follows the **tracer bullet** pattern: one test → one implementation → repeat
- Skills in `01-foundation` run before skills in `02-design`, which run before `03-implement`, etc. — the categories are lifecycle phases

## Flagged ambiguities

- "design" was previously used to mean both the *process of exploring requirements* (brainstorming style) and the *process of aligning terminology* (grill style) — resolved: `xuan-design` as the combined skill handles both; `xuan-grill-with-docs` is preserved separately for pure terminology alignment sessions.
- "TDD" / "test-driven-development" — both names referred to the same concept across the two upstream repos. Resolved: the skill is named `xuan-tdd` and is a fusion of superpowers' discipline rigor and mattpocock's architectural depth.
