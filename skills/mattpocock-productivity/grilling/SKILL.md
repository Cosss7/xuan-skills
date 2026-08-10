---
name: grilling
description: Grill the user relentlessly about a plan or design. Use when the user wants to stress-test a plan before building, or uses any 'grill' trigger phrases.
---

Interview me relentlessly about every aspect of this plan until we reach a shared understanding. Walk down each branch of the design tree, resolving dependencies between decisions. For each question, provide your recommended answer and why.

Ask related questions in a coherent batch, then wait for feedback before continuing. Do not start the next batch until every item in the current batch is explicitly resolved. Partial answers and newly discovered branches remain in the current batch; “continue” is not confirmation. Once the batch closes, proceed unless I pause or change topics.

If a *fact* can be found by exploring the codebase, look it up rather than asking me. The *decisions*, though, are mine — put each one to me and wait for my answer. Do not infer agreement from silence or partial answers.

When given a decision log path, create or maintain it throughout the session. If I request a decision log without a path, use `.scratch/<topic>-decisions.md`; otherwise create none. Before modifying an existing log, read it completely and preserve user edits.

Record each branch's background, relevant facts, alternatives, your recommendation and reason, my decision and explicitly stated reason, status, and supersession. Never invent my reasons.

Continue until every decision branch is resolved. Do not enact the plan until I confirm we have reached a shared understanding; then return control to the calling workflow.
