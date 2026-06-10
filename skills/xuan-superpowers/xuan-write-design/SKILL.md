---
name: xuan-write-design
description: Invoke by other skill or manually invoke only.
---

<xuan-write-design-skill>

# xuan-write-design

<HARD-GATE>

You MUST create a task for each of these items and complete them in order for checklist

Do NOT invoke any implementation skill, write any code, scaffold any project, or take any implementation action until you have presented a design and the user has approved it. This applies to EVERY project regardless of perceived simplicity.

</HARD-GATE>

## Checklist

<checklist>

1. **Present design** — in sections scaled to their complexity, get user approval after each section
2. **Write design doc** — save to `docs/ai-trace/design/YYYY-MM-DD-<topic>-design.md` and commit
3. **Design self-review** — quick inline check for placeholders, contradictions, ambiguity, scope (see below)
4. **User reviews written design** — ask user to review the design file before proceeding

</checklist>

## The Process

**Presenting the design:**

- Once you believe you understand what you're building, present the design
- Scale each section to its complexity: a few sentences if straightforward, up to 200-300 words if nuanced
- Ask after each section whether it looks right so far
- Cover: architecture, components, data flow, error handling, testing
- Be ready to go back and clarify if something doesn't make sense

**Design for isolation and clarity:**

- Break the system into smaller units that each have one clear purpose, communicate through well-defined interfaces, and can be understood and tested independently
- For each unit, you should be able to answer: what does it do, how do you use it, and what does it depend on?
- Can someone understand what a unit does without reading its internals? Can you change the internals without breaking consumers? If not, the boundaries need work.
- Smaller, well-bounded units are also easier for you to work with - you reason better about code you can hold in context at once, and your edits are more reliable when files are focused. When a file grows large, that's often a signal that it's doing too much.

**Working in existing codebases:**

- Explore the current structure before proposing changes. Follow existing patterns.
- Where existing code has problems that affect the work (e.g., a file that's grown too large, unclear boundaries, tangled responsibilities), include targeted improvements as part of the design - the way a good developer improves code they're working in.
- Don't propose unrelated refactoring. Stay focused on what serves the current goal.

## After the Design

**Documentation:**

- Write the validated design (spec) to `docs/ai-trace/specs/YYYY-MM-DD-<topic>-design.md`
  - (User preferences for spec location override this default)
  - write full design, not the summary
- Commit the design document to git

**Spec Self-Review:**
After writing the spec document, look at it with fresh eyes:

- [ ] **Placeholder scan:** Any "TBD", "TODO", incomplete sections, unresolved decisions, or vague requirements? Fix them by asking user.
- [ ] **Internal consistency:** Do any sections contradict each other? Does the architecture match the feature descriptions?
- [ ] **Scope check:** Is this focused enough for a single implementation plan, or does it need decomposition?
- [ ] **Ambiguity check:** Could any requirement be interpreted two different ways? If so, pick one and make it explicit.

Fix any issues inline. No need to re-review — just fix and move on.

**User Review Gate:**
After the spec review loop passes, ask the user to review the written spec before proceeding:

> "Spec written and committed to `<path>`. Please review it and let me know if you want to make any changes before we start writing out the implementation plan."

Wait for the user's response. If they request changes, make them and re-run the spec review loop. Only proceed once the user approves.

**Next Step:**
<next-step>

Invoke skill xuan-write-plan if user approve.

</next-step>

</xuan-write-design-skill>
