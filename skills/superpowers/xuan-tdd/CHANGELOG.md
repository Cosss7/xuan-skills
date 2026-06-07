# Changelog: xuan-tdd

## Design Context

This skill fuses the iron-law discipline from superpowers' `test-driven-development` with the architectural depth from mattpocock's `tdd`. The goal: keep superpowers' strict verification gates and anti-rationalization defense, while adding matt's planning phase, tracer bullet workflow, and supporting architecture docs.

## Upstream Sources

**Source A: `test-driven-development`** (obra/superpowers)
- Commit: `030a222`
- Strength: Iron law (delete code written before test), RED/GREEN verification gates, 11-row rationalization table, 13 red flags, "Why Order Matters" essays, bug fix walkthrough
- Tone: Strict, confrontational, designed to resist AI rationalization

**Source B: `tdd`** (mattpocock/skills)
- Commit: `7afa86d`
- Supporting files: `interface-design.md`, `mocking.md`, `tests.md`, `deep-modules.md`, `refactoring.md`
- Strength: Planning phase, tracer bullet (anti-horizontal-slicing), deep module theory, mocking strategy
- Tone: Architectural, teaching-oriented

## Fusion Rules

**Rule 1: All superpowers content is preserved.** Nothing removed. Every paragraph, every rationalization table row, every red flag, every verification step stays.

**Rule 2: Matt content is additive only.** Planning Phase, Tracer Bullet, and all 5 supporting files are additions.

**Rule 3: Where both sources cover the same concept, the stricter version wins.**

## Specific Changes from Superpowers Source

### Added: Planning Phase (before RED)

```markdown
## Planning Phase (Before RED)

Before writing the first test, confirm with your human partner:
1. Interface changes — what types, functions, or config shapes change?
2. Behaviors to test — list them in priority order
3. Deep module opportunities — can the new code present a small interface
   while hiding complexity? (See deep-modules.md)
4. Testability design — accept dependencies via parameters, return results
   not side effects, keep surface area small (See interface-design.md)
5. User approval — confirm the plan before writing tests
```

Inserted after the "## When to Use" section, before the Iron Law.

### Added: Tracer Bullet Rhythm (after REFACTOR)

```markdown
### Tracer Bullet Rhythm

Build features one vertical slice at a time:
1. Write ONE test for ONE behavior (not all tests at once)
2. RED → Verify → GREEN → Verify → REFACTOR
3. Write the next test for the next behavior
4. Repeat

**Anti-pattern — Horizontal slicing:** Writing all tests first, then all
implementation. This delays feedback and encourages testing implementation
details instead of behavior.
```

### Extended: REFACTOR section

Added reference to `refactoring.md` signals and `deep-modules.md` after the original REFACTOR paragraph.

### Updated: "When Stuck" table row 3

Before: `"Must mock everything | Code too coupled. Use dependency injection."`
After: `"Must mock everything | Code too coupled. See interface-design.md for DI patterns. See mocking.md for what to mock (only system boundaries)."`

### Updated: Cross-references

- `@testing-anti-patterns.md` → `testing-anti-patterns.md` (removed `@` prefix per xuan convention)
- No `superpowers:` cross-refs were present in the source

### New Supporting Files (6 total)

From matt tdd (unchanged):
- `interface-design.md` — dependency injection, return results not side effects, small surface area
- `mocking.md` — mock only at system boundaries (external APIs, DB, time, filesystem); never mock own code
- `tests.md` — integration-style testing through public interfaces, not private methods or call order
- `deep-modules.md` — Ousterhout: small interface + large implementation = deep; large interface + little logic = shallow
- `refactoring.md` — refactoring signals: duplication, long methods, shallow modules, feature envy, primitive obsession

From superpowers (unchanged):
- `testing-anti-patterns.md` — anti-patterns reference (testing mock behavior, test-only methods, incomplete mocks)

### Content NOT Added (Rejected)

- Matt's original 4-phase workflow (Planning → Tracer Bullet → Incremental Loop → Refactor) was NOT used as the top-level structure. Instead, superpowers' RED-GREEN-REFACTOR loop is the primary structure, with Planning and Tracer Bullet inserted as subsections. This preserves superpowers' stricter cycle as the authoritative workflow.
