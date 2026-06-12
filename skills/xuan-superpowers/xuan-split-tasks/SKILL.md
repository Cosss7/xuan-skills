---
name: xuan-split-tasks
description: Invoke by other skill or manually invoke only.
---

<xuan-split-tasks-skill>

# xuan-split-tasks

Break a plan into independently-grabbable coding tasks using vertical slices (tracer bullets), write to plan doc.

<process>

## Process

You MUST create a task or todo for each of these process and complete them in order for:

### 1. Gather context

Work from whatever is already in the conversation context. If a spec or design doc has written before, follow it, declare the doc path to user.

### 2. Explore the codebase (optional)

If you have not already explored the codebase, do so to understand the current state of the code. Tasks titles and descriptions should use the project's domain glossary vocabulary, and respect ADRs in the area you're touching.

### 3. Draft vertical slices

Break the plan into **tracer bullet** tasks. Each task is a thin vertical slice that cuts through ALL integration layers end-to-end, NOT a horizontal slice of one layer.

Slices may be 'HITL' or 'AFK'. HITL slices require human interaction, such as an architectural decision or a design review. AFK slices can be implemented and merged without human interaction. Prefer AFK over HITL where possible.

<vertical-slice-rules>

- Each slice delivers a narrow but COMPLETE path through every layer (schema, API, UI, tests)
- A completed slice is demoable or verifiable on its own
- Prefer many thin slices over few thick ones

</vertical-slice-rules>

### 4. Quiz the user

Present the proposed breakdown as a numbered list. For each slice, show:

- **Title**: short descriptive name
- **Type**: HITL / AFK
- **Blocked by**: which other slices (if any) must complete first
- **Description**: why-what-how

Ask the user:

- Does the granularity feel right? (too coarse / too fine)
- Are the dependency relationships correct?
- Should any slices be merged or split further?
- All unresolved decisions until HITL tasks become AFK.

Iterate until the user approves the breakdown.

### 5. Write the tasks to plan doc

**Save all approved slice to plan doc:** `docs/ai-trace/plans/YYYY-MM-DD-<feature-name>.md`
- (User preferences for plan location override this default)
- In dependency order (blockers first)
- Use plan doc template below

### 6.Self-Review

After writing the complete plan, look at the spec with fresh eyes and check the plan against it. This is a checklist you run yourself — not a subagent dispatch.

**1. Spec coverage:** Skim each section/requirement in the spec. Can you point to a task that implements it? List any gaps.

**2. Placeholder scan:** Search your plan for red flags — any of the patterns from the "No Placeholders" section above. Fix them.

**3. Type consistency:** Do the types, method signatures, and property names you used in later tasks match what you defined in earlier tasks? A function called `clearLayers()` in Task 3 but `clearFullLayers()` in Task 7 is a bug.

**4. Temeplate:** All follow the template.

**5. Task order:** In dependency order (blockers first)

If you find issues, fix them inline. No need to re-review — just fix and move on. If you find a spec requirement with no task, add the task.

</process>

## Plan doc template:

<plan-doc-template>

**Every plan MUST start with this header:**

```markdown
# [Feature Name] Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use xuan-subagent-driven-development to implement this plan task-by-task.

**Design/Spec:** [relative path reference to design doc or spec doc]

**Goal:** [One sentence describing what this builds]

**Architecture:** [2-3 sentences about approach]

**Tech Stack:** [Key technologies/libraries]

---
```

**Task Structure:**

```markdown
### Task N: [short descriptive name]

**why:**

**what:**

**how:**

```

</plan-doc-template>

## Next Step
<next-step>

Ask user confrim continue, then you invoke skill xuan-subagent-driven-development. Mark checklist done before invoke the skill.

</next-step>

</xuan-split-tasks-skill>
