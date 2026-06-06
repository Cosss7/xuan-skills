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
