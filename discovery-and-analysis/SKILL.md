---
name: "discovery-and-analysis"
description: "Fully develop the leading near-tied ideas with deterministic limits."
---

# Discovery and Analysis

Separate creative enumeration from evaluation. Complete discovery before beginning analysis.

## Establish the task

Extract:

- The topic, problem, or decision
- Known goals, constraints, stakeholders, and success criteria
- The requested output, if any

Ask a question only when missing information prevents meaningful discovery. Otherwise, state necessary assumptions and proceed.

## Start the audit

Audit every run before discovery begins.

1. Obtain a random UUID from the operating system and record the current UTC start timestamp. Do not invent either value in model prose.
2. Create a distinct persistent run directory. Use a user-specified location, or default to `experiments/discovery-and-analysis/<uuid>/` under the available workspace.
3. Create `receipt.txt` with:
   - task or run name
   - UUID
   - UTC start timestamp
   - `status=started`
   - model identifier only when the runtime exposes it reliably
4. Treat audit metadata as outside the substantive task. Do not use the UUID, timestamps, paths, or receipts as discovery or analysis inputs.

If persistent storage or system-generated UUIDs are unavailable, disclose that limitation before discovery. Create the strongest inline receipt the host supports, mark it `audit=non-durable`, and do not claim a persistent independent audit trail.

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
5. Discard the incomplete analysis contract, comparisons, rankings, conclusions, and prose from that attempt.
6. Restart Phase 2 from the beginning using only the original task, stated assumptions, and expanded discovery artifact.

Repeat until one complete analysis attempt produces no new discoveries. Never continue a partial analysis against a changed list.

## Phase 2: Analysis

Choose an analysis pipeline appropriate to the task. Before evaluating any item, write an `Analysis contract` containing:

1. The task type, such as decision, diagnosis, planning, design, explanation, prioritization, risk analysis, or mixed.
2. The ordered analysis stages that will be used.
3. The criteria and their definitions.
4. The comparison method: ordinal by default, or numeric only when justified.
5. For ordinal comparison: criterion priority, what counts as a meaningful difference, tie and incomparability rules, top-N target, and safety cap.
6. For numeric comparison: criterion weights, anchored measurement scale, aggregation rule, and tie-breakers.
7. The disconfirmation method and the evidence that could change selection.
8. The sensitivity bounds: which uncertain assumptions, criterion priorities, or meaningful-difference thresholds may reasonably vary.
9. The rule for handling unknown information.
10. Deterministic tie-breakers used only where the evidence supports breaking a tie.

Once declared, do not change the contract during that attempt. If the contract is inadequate, finish the attempt, explain the limitation, and propose a revised contract for a new run.

### Default contracts

Use the narrowest suitable contract, adapting labels to the task while retaining explicit rules.

For a decision or prioritization:

1. Classify eligibility against hard constraints as `eligible`, `ineligible`, or `unknown`.
2. Define 3–7 non-overlapping decisive criteria in priority order. Give each criterion task-specific observable anchors for weak, mixed, and strong evidence.
3. Place clearly dominated or noncompetitive eligible candidates in `not currently selected for further analysis`. Keep uncertain or plausibly competitive candidates in the comparison pool.
4. Compare candidates pairwise using the highest-priority criterion on which the evidence shows a meaningful difference. If neither clearly beats the other, mark them tied or incomparable; do not force an order.
5. Collapse comparison cycles into the same tier. A cycle is evidence that the declared comparator cannot consistently distinguish those candidates, not permission to invent a winner.
6. Continue comparison only until the top N candidates are separated from the rest, or the unresolved leading tier fills the available selection. Default `N=3`.
7. Select the top N for full analysis. Tied or incomparable candidates may occupy the selected set. If a tie crosses the cutoff, include all tied candidates up to a default safety cap of 5. The user may set a different cap, never above 10. If the tie exceeds the cap, analyze the tied group collectively first or report the cutoff unresolved.
8. Run the disconfirmation pass against every selected candidate using comparable scrutiny.
9. Recompare the selected set after disconfirmation. Demote candidates when contrary evidence warrants it and promote eligible candidates from `not currently selected for further analysis` when they now cross the cutoff.
10. Sensitivity-test only reasonable changes to uncertain assumptions, criterion priority, and meaningful-difference thresholds that could alter the revised top-N set. Do not vary settled facts or enumerate changes that cannot affect selection. Report the stable core, conditional selections, and whether the conclusion is robust or unstable.
11. Recommend one candidate, a tied or incomparable leading set, or a clearly defined portfolio. Do not manufacture a single winner when the evidence does not support one.

Use numeric scoring only when criteria have defensible measurements or the user explicitly requests a weighted tradeoff model. Define task-specific anchors and show the math. Do not convert qualitative impressions into numbers merely to force a total order.

For diagnosis:

1. Group items into symptoms, candidate causes, evidence, confounders, and tests.
2. Compare candidate causes by explanatory coverage, consistency with known facts, parsimony, and testability in declared priority order.
3. Preserve ties and incomparability when available evidence cannot distinguish causes.
4. Select the leading causes for full development using the same top-N and safety-cap rules.
5. Specify the cheapest or most informative discriminating tests.
6. State what evidence would raise or lower each leading hypothesis.

For planning or design:

1. Group items into goals, constraints, resources, actions, dependencies, risks, and feedback signals.
2. Remove no items; mark inapplicable ones with reasons.
3. Build candidate approaches from the items and cite their source IDs.
4. Compare approaches by feasibility, impact, reversibility, cost, risk, and information value in a declared task-specific priority order.
5. Select approaches using the same top-N, tie, incomparability, and safety-cap rules.
6. Order selected actions by dependency, then information value, then the earliest contributing discovery ID only when still tied.
7. Produce checkpoints and explicit stop, continue, or revise conditions.

For explanation or sense-making:

1. Group items by concept without ranking unless ranking is useful.
2. Identify relationships: cause, dependency, contrast, example, feedback loop, uncertainty, or boundary.
3. Build the explanation from foundational concepts to consequences.
4. Preserve unresolved contradictions and unknowns rather than smoothing them over.
5. End with the smallest coherent synthesis that accounts for the important items.

For mixed tasks, compose only the necessary contracts and declare their order before analysis.

## Disconfirmation pass

After initial top-N selection and before the final recommendation, try to overturn the selection.

1. For every selected candidate, hypothesis, or approach, state the strongest plausible reason it should not remain selected.
2. Identify evidence that would confirm that failure case and could materially change selection.
3. Seek that evidence when tools and scope permit. Prefer real checks over ceremonial devil's-advocate prose.
4. Apply comparable scrutiny to every selected candidate, not only the apparent leader.
5. Distinguish:
   - `searched and not found`: the specified search did not locate the evidence;
   - `not searched`: the check was outside available tools, time, or scope;
   - `evidence of absence`: reliable evidence indicates the condition is absent.
6. Reapply the declared comparator after the pass. Disconfirming evidence may reorder tiers, create ties or incomparability, demote a selected candidate, or promote one previously not selected.
7. When evidence is unavailable, preserve the concern as an `unknown` and propose the cheapest discriminating test.
8. Report what was checked, what was found, and whether the selected set changed.

If the task does not permit external research, use known evidence and explicit tests without pretending that an imagined objection was verified.

## Develop leading alternatives

When analysis selects candidate ideas, fully develop the selected top N rather than forcing a total ordering of every eligible candidate.

1. Default to the top 3 eligible, relevant candidates when that many exist.
2. Tied or incomparable candidates may appear anywhere in the selected set, including the leading tier.
3. If a tie crosses the N cutoff, include all tied candidates up to the active safety cap. If the tied group exceeds the cap, analyze the group collectively first or report that the cutoff remains unresolved.
4. Default to at most 5 fully developed candidates. The user may request a different limit, but never fully develop more than 10.
5. Give each selected candidate comparable treatment: what it is, why it was selected, a concrete execution path or implications, important risks and unknowns, and the conditions under which it would become preferable or cease to qualify.
6. Identify a sole leader only when the declared comparison supports one. Otherwise report the leading tier, ties, or incomparability explicitly.
7. Classify all candidates in the final result as:
   - `Selected for full analysis`: the top N, including tied or incomparable candidates.
   - `Not currently selected for further analysis`: eligible candidates below the cutoff, with a brief reason or category but no fabricated exact rank.
   - `Ineligible`: candidates that violate a hard constraint.
   - `Unknown`: candidates lacking enough information even for screening.

## Repeatability rules

Maximize repeatability when analyzing the same frozen list:

- Use only the original task, stated assumptions, frozen discovery artifact, and analysis contract as inputs.
- Keep item IDs and generation order unchanged.
- Use explicit task-specific criteria and observable anchors rather than intuitive labels such as `best`.
- Apply the declared comparator consistently.
- Treat missing evidence as `unknown`; do not invent facts to resolve uncertainty.
- Preserve the distinction between `searched and not found`, `not searched`, and `evidence of absence`.
- Do not use discovery ID to break a substantive tie unless the contract explicitly defines it as a final presentation-only rule.
- Separate observations from assumptions and value judgments.
- Do not add criteria or change their priority after comparing candidates.
- Report enough pairwise reasoning, tiers, classifications, or numeric calculations to reproduce the result.
- After any restart, do not reuse partial evaluations from the discarded attempt.

Exact bit-for-bit identity is not guaranteed for model-generated prose. Prefer stable structure, classifications, selected sets, comparisons, and conclusions over stylistic consistency.

## Finish the audit

After completing the substantive result:

1. Save its exact text, beginning with `Discovery artifact` and excluding audit metadata, as `result.md` in the run directory.
2. Compute the SHA-256 of the saved `result.md` with a deterministic system utility.
3. Update `receipt.txt` with the UTC finish timestamp, `status=completed`, and exact result SHA-256.
4. Return the UUID, receipt path, result path, hash, and substantive result.

If the run fails, update the durable receipt when possible with UTC finish timestamp, `status=failed`, and a short failure reason. Do not create a completed receipt for a partial result.

## Compare multiple runs

Run multiple executions sequentially unless the user explicitly requests parallel execution. Start each with fresh conversation context and do not provide prior outputs, conclusions, or artifacts.

Do not read another run's directory before the current run is complete. Compare runs only after all receipts show `status=completed` and their hashes have been independently verified against the saved files.

When comparing runs:

- Compare saved `result.md` files, not wrapper messages.
- Report whether they are byte-identical.
- Compare discovery counts and overlap, analysis contracts, tiers or numeric results, selected sets, conclusions, and restart logs.
- Treat different audit metadata as evidence of distinct execution, not substantive variation.
- State that run-specific audit requirements make the complete prompts non-identical even though the substantive task remains the same.

## Return the result

Return, in order:

1. `Discovery artifact`: the final complete numbered list.
2. `Restart log`: each analysis restart and the discovery IDs appended before it, or `None`.
3. `Analysis contract`: the fixed method used for the completed attempt.
4. `Analysis`: groupings, comparisons, calculations when used, stages, and findings.
5. `Result`: recommendation, plan, diagnosis, synthesis, or other requested output.
6. `Uncertainties`: unknowns and assumptions that could change the result.

Keep discovery and analysis visibly distinct. Never rewrite the discovery artifact to make the analysis look cleaner.
