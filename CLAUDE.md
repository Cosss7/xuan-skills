# xuan-skills

A curated collection of AI agent skills. Published via skills.sh.

## Structure

- `skills/<category>/<skill-name>/SKILL.md` — one skill per directory
- Category: lifecycle phase (01-foundation → 06-communicate)
- Supporting files next to SKILL.md if needed

## Cross-Referencing

- **REQUIRED SUB-SKILL:** Use `<skill-name>` — when another skill must run first
- **REQUIRED BACKGROUND:** You MUST understand `<skill-name>` — prerequisite knowledge
- Never use `@` force-load syntax (burns context)

## Doc Output

- Specs: `docs/ai-trace/specs/`
- Plans: `docs/ai-trace/plans/`
- ADRs: `docs/ai-trace/adr/`
