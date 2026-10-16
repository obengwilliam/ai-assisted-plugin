---
name: deepen-task
description: Use when a user asks to make a task or prompt deeper, more expert, or more rigorous without making it bigger; identify the right ambition, raw source material, methods and tools, and independent proof, then rewrite the prompt.
---

# Deepen a Task

Improve the rigor of the requested task while preserving its scope. Rewrite the prompt; do not execute it unless asked separately.

## Choose the ambition

Use the ambition the user asks for:

- **Speed:** same work in less time.
- **Altitude:** focus on the outcome above the individual task.
- **Depth:** work from underlying evidence and use the methods a leading practitioner would.
- **Range:** bring in useful knowledge and methods from other fields.

When the user asks for “deeper, not bigger,” choose **Depth**. Do not add altitude or range unless requested.

## Deepen the task

Before rewriting, identify:

1. **Expert step:** one concrete thing a top professional would do at this task’s scope that the prompt does not ask for. Do not invent a larger deliverable.
2. **Raw material:** the most direct source material available, such as original data, records, source documents, code, or logs. Name it specifically and distinguish it from summaries. If unavailable, say what input is needed or mark the assumption.
3. **Methods and tools:** specific, appropriate methods and tools, tied to the material they will use. Avoid generic research plans and tool lists.
4. **Independent proof:** observable evidence or a reproducible check that lets someone other than the assistant or user judge the result. Do not claim certainty where the domain cannot provide it.

Preserve the original goal, constraints, audience, and output. Add only the smallest expert step that materially improves the result. Use available files or sources to make the raw material and methods concrete; do not pretend to have inputs that are missing. Ask only when missing information would materially change the rewrite.

## Output

Return these parts in order:

- **Ambition:** Speed, Altitude, Depth, or Range.
- **Expert step:** the bounded improvement.
- **Start from:** the raw material or missing input.
- **Methods and tools:** specific approaches tied to the material.
- **Proof:** independent, observable evidence of correctness.
- **Rewritten prompt:** a concise prompt that asks for exactly this work and keeps the original scope.

Use this wording when it fits:

> I want a deeper version of this task, not a bigger one. Before rewriting it: (1) say what a top professional in this field would do here that I'm not asking for; (2) name the rawest material they would start from instead of what has already been digested for me; (3) name the specific methods and tools they would use; (4) say what, other than you or me, would show the result is right. Then rewrite my prompt to ask for exactly that.
