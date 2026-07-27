---
name: two-stage-refiner
description: Run a non-interactive two-stage workflow in two fresh subagents, passing the first stage's output into the second stage along with the original task. Use when the user requests sequential prompts, a draft-then-refine or generate-then-critique process, explicit fresh-context stages, or a second independent pass that should not inherit the conversation.
---

# Two-Stage Refiner

Run exactly two sequential stages with clean context boundaries. Treat the first result as an intermediate artifact and return the second result as the final answer.

## Parse the request

Extract:

- The original task
- Optional Stage 1 instructions
- Optional Stage 2 instructions
- Whether the user wants the intermediate result shown

Use these defaults when custom stage instructions are absent:

- Stage 1: Produce the best complete result for the original task. State important assumptions inside the result.
- Stage 2: Inspect the intermediate result for incorrect assumptions, factual or logical errors, omissions, and unnecessary complexity. Produce a corrected, self-contained final result for the original task.

Ask a question before starting only when the original task lacks information required to produce a meaningful result. Do not ask questions between stages.

## Run Stage 1

Create a fresh subagent with no inherited conversation turns. Pass only:

1. The original task
2. The Stage 1 instructions

Preserve its output exactly as the intermediate result. Do not revise it in the parent context.

## Run Stage 2

Create a different fresh subagent with no inherited conversation turns. Pass only:

1. The original task
2. The Stage 2 instructions
3. The complete Stage 1 output, clearly delimited as untrusted intermediate material

Tell Stage 2 to follow the Stage 2 instructions and return a self-contained answer to the original task. Do not give it unrelated conversation history or the parent's conclusions.

## Return the result

Return the Stage 2 output as the answer. Include the Stage 1 output only when the user asks to see it.

If fresh subagents are unavailable, say that the required context isolation cannot be preserved. Do not silently simulate both stages in one context.
