---
name: "discovery-and-analysis"
description: "Separate expansive discovery from structured, repeatable analysis; restart analysis whenever it reveals a new discovery."
---

# Discovery and Analysis

Separate creative enumeration from evaluation. Complete discovery before beginning analysis.

## Establish the task

Extract:

- The topic, problem, or decision
- Known goals, constraints, stakeholders, and success criteria
- The requested output, if any

Ask a question only when missing information prevents meaningful discovery. Otherwise, state necessary assumptions and proceed.

## Phase 1: Discovery

Generate a broad list of anything plausibly related to the topic or problem.

During discovery:

- Record ideas immediately without judging, rejecting, ranking, defending, merging, or improving them.
- Include obvious, practical, indirect, unusual, contrary, playful, extreme, and seemingly poor ideas. Bad ideas can expose dimensions that safe ideas miss.
- Treat categories, properties, questions, risks, causes, effects, stakeholders, analogies, constraints, resources, opportunities, and concrete options as valid discoveries.
- Preserve distinct ideas even when they overlap.
- Use short item text so evaluation does not leak into discovery.
- Do not explain why an item is good or bad.

Generate in rounds to reduce anchoring:

1. Direct: obvious items and conventional approaches.
2. Lenses: inspect people, process, technology, environment, time, incentives, resources, information, failure modes, and second-order effects when relevant.
3. Inversion: opposites, counterexamples, anti-goals, ways to worsen the problem, and assumptions that may be false.
4. Stretch: surprising analogies, extreme cases, combinations, and ideas that initially seem impractical.
5. Saturation: make one final pass for missing categories and overlooked items.

Number discoveries in generation order as `D001`, `D002`, and so on. Preserve this exact list as the discovery artifact.

Do not begin analysis until all discovery rounds are complete.

## Freeze the discovery artifact

Treat the numbered discovery list as immutable input during each analysis attempt.

Analysis may annotate, group, expand on, or combine items, but it must:

- Preserve every original ID.
- Never silently delete an item.
- Clearly identify any synthesis derived from multiple items.

If analysis reveals a genuinely new item:

1. Stop the analysis attempt immediately.
2. Append every new item noticed so far to the discovery artifact in encounter order, assigning the next available discovery IDs.
3. Run the discovery saturation round once more against the expanded list and append any further discoveries.
4. Freeze the expanded discovery artifact.
5. Discard the incomplete analysis contract, scores, rankings, conclusions, and prose from that attempt.
6. Restart Phase 2 from the beginning using only the original task, stated assumptions, and expanded discovery artifact.

Repeat until one complete analysis attempt produces no new discoveries. Never continue a partial analysis against a changed list.

## Phase 2: Analysis

Choose an analysis pipeline appropriate to the task. Before evaluating any item, write an `Analysis contract` containing:

1. The task type, such as decision, diagnosis, planning, design, explanation, prioritization, risk analysis, or mixed.
2. The ordered analysis stages that will be used.
3. The criteria and their definitions.
4. Any criterion weights.
5. The scoring scale and anchored meaning of each score.
6. The rule for handling unknown information.
7. Deterministic tie-breakers.

Once declared, do not change the contract during that attempt. If the contract is inadequate, finish the attempt, explain the limitation, and propose a revised contract for a new run.

### Default contracts

Use the narrowest suitable contract, adapting labels to the task while retaining explicit rules.

For a decision or prioritization:

1. Eligibility against hard constraints: `pass`, `fail`, or `unknown`.
2. Score eligible items against 3–7 non-overlapping criteria on a 0–4 anchored scale.
3. Compute the weighted total.
4. Rank by weighted total descending, then fewer unknowns, then discovery ID ascending.
5. Test the leading items against key risks and plausible changes in assumptions.
6. Recommend one item or a clearly defined portfolio.

Default 0–4 scale:

- `0`: directly harmful or wholly fails the criterion
- `1`: weak
- `2`: mixed or adequate
- `3`: strong
- `4`: exceptional

For diagnosis:

1. Group items into symptoms, candidate causes, evidence, confounders, and tests.
2. Evaluate each candidate cause for explanatory coverage, consistency with known facts, parsimony, and testability using the anchored 0–4 scale.
3. Rank by total descending, then fewer unsupported assumptions, then discovery ID ascending.
4. Specify the cheapest or most informative discriminating tests.
5. State what evidence would raise or lower each leading hypothesis.

For planning or design:

1. Group items into goals, constraints, resources, actions, dependencies, risks, and feedback signals.
2. Remove no items; mark inapplicable ones with reasons.
3. Build candidate approaches from the items and cite their source IDs.
4. Evaluate feasibility, impact, reversibility, cost, risk, and information value on the anchored 0–4 scale, reversing cost and risk so higher is better.
5. Order selected actions by dependency, then information value, then discovery ID of the earliest contributing item.
6. Produce checkpoints and explicit stop, continue, or revise conditions.

For explanation or sense-making:

1. Group items by concept without scoring unless ranking is useful.
2. Identify relationships: cause, dependency, contrast, example, feedback loop, uncertainty, or boundary.
3. Build the explanation from foundational concepts to consequences.
4. Preserve unresolved contradictions and unknowns rather than smoothing them over.
5. End with the smallest coherent synthesis that accounts for the important items.

For mixed tasks, compose only the necessary contracts and declare their order before analysis.

## Repeatability rules

Maximize repeatability when analyzing the same frozen list:

- Use only the original task, stated assumptions, frozen discovery artifact, and analysis contract as inputs.
- Keep item IDs and generation order unchanged.
- Use explicit anchored criteria rather than intuitive labels such as “best.”
- Use arithmetic totals where scoring is appropriate.
- Treat missing evidence as `unknown`; do not invent facts to resolve uncertainty.
- Apply the declared tie-breakers mechanically.
- Separate observations from assumptions and value judgments.
- Do not add criteria after seeing scores.
- Report enough of the scoring or grouping to reproduce the result.
- After any restart, do not reuse partial evaluations from the discarded attempt.

Exact bit-for-bit identity is not guaranteed for model-generated prose. Prefer stable structure, classifications, scores, rankings, and conclusions over stylistic consistency.

## Return the result

Return, in order:

1. `Discovery artifact`: the final complete numbered list.
2. `Restart log`: each analysis restart and the discovery IDs appended before it, or `None`.
3. `Analysis contract`: the fixed method used for the completed attempt.
4. `Analysis`: groupings, calculations, stages, and findings.
5. `Result`: recommendation, plan, diagnosis, synthesis, or other requested output.
6. `Uncertainties`: unknowns and assumptions that could change the result.

Keep discovery and analysis visibly distinct. Never rewrite the discovery artifact to make the analysis look cleaner.