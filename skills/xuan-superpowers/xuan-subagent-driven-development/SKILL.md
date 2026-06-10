---
name: xuan-subagent-driven-development
description: Invoke by other skill or manually invoke only.
---

<xuan-subagent-driven-development-skill>

# xuan-subagent-driven-development

Execute plan by dispatching fresh subagent per task, with two-stage review after each: spec compliance review first, then code quality review.

**Why subagents:** You delegate tasks to specialized agents with isolated context. By precisely crafting their instructions and context, you ensure they stay focused and succeed at their task. They should never inherit your session's context or history — you construct exactly what they need. This also preserves your own context for coordination work.

**Core principle:** Fresh subagent per task + two-stage review (spec then quality) = high quality, fast iteration

**Continuous execution:** Do not pause to check in with your human partner between tasks. Execute all tasks from the plan without stopping. The only reasons to stop are: BLOCKED status you cannot resolve, ambiguity that genuinely prevents progress, or all tasks complete. "Should I continue?" prompts and progress summaries waste their time — they asked you to execute the plan, so execute it.

**Context:** Work from whatever is already in the conversation context. If a plan doc has written before, follow it, declare the doc path to user.

<HARD-GATE>

**HARD-GATE:** 
- You MUST tell subagent invoke skill `xuan-tdd`
- You MUST create checklist tracking the tasks in the plan doc

</HARD-GATE>

## Process



</xuan-subagent-driven-development-skill>
