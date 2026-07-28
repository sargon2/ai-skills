---
name: "discovery-and-analysis"
description: "Fully develop the leading near-tied ideas with deterministic limits."
---

# Discovery and Analysis

Separate creative enumeration from evaluation. Complete discovery before analysis, preserve the process in the result, and create durable artifacts proving the workflow ran.

## Establish the task

Extract the problem or decision, goals, hard constraints, stakeholders, success criteria, and requested output. Ask only when missing information prevents meaningful discovery; otherwise state necessary assumptions and proceed.

## Start the audit

Before discovery:

1. Obtain a system-generated UUID and current UTC start timestamp; never invent them in prose.
2. Create a distinct persistent run directory at the user-specified location or `experiments/discovery-and-analysis/<uuid>/`.
3. Create `receipt.txt` containing the task or run name, UUID, start timestamp, `status=started`, and the model identifier only when exposed reliably.
4. Keep audit metadata out of substantive reasoning.

If durable storage or a system-generated UUID is unavailable, disclose this before discovery, create the strongest inline receipt the host supports, and mark it `audit=non-durable`. Do not claim a persistent independent audit trail.

## Phase 1: Discovery

Generate broadly without evaluating, rejecting, ranking, defending, merging, or improving items. Keep item text short and include obvious, practical, indirect, unusual, contrary, extreme, and seemingly poor possibilities.

Work in five passes:

1. Direct: obvious items and conventional approaches.
2. Lenses: relevant people, process, technology, environment, time, incentives, resources, information, and failure modes.
3. Inversion: opposites, counterexamples, anti-goals, ways to worsen the problem, and possibly false assumptions.
4. Stretch: surprising analogies, extreme cases, combinations, and initially impractical ideas.
5. Saturation: missing categories and overlooked items.

Number items in generation order as `D001`, `D002`, and so on. Preserve the numbered list as the discovery artifact. Do not begin evaluation until all passes are complete.

## Preserve discovery

Keep the discovery artifact intact during analysis. Analysis may annotate, group, expand, or synthesize items, but must preserve original IDs and identify the source IDs of syntheses.

If analysis reveals a genuinely new item, append it with the next ID and evaluate or redo only the affected groupings and comparisons. Record the addition in the restart log as a late discovery; do not discard unaffected work or restart the entire analysis.

## Phase 2: Analysis

Before evaluation, declare a compact `Analysis contract`:

- task type
- hard constraints
- 3–7 decisive, non-overlapping criteria in priority order, with task-specific meaning
- comparison rule and top-N target
- treatment of unknowns

Use the narrowest suitable pipeline:

- Decision or prioritization: screen eligibility, compare candidates, and develop the leading set.
- Diagnosis: compare hypotheses by explanatory coverage and consistency, then identify discriminating tests.
- Planning or design: synthesize approaches from discovery IDs, compare them, and order selected actions by dependency and information value.
- Explanation or sense-making: organize concepts and relationships without ranking unless ranking helps.
- Mixed task: compose only the necessary stages and state their order.

Use ordinal comparison by default. Compare candidates using the highest-priority criterion with a meaningful evidence-backed difference. Mark candidates tied or incomparable when evidence does not support an order; collapse comparison cycles into one tier. Use numeric scoring only for defensible measurements or when the user explicitly requests a weighted model; define anchors and show the math.

Treat missing evidence as `unknown`. Never use discovery order as substantive evidence or invent facts to break a tie.

## Universal selection policy

Classify candidates as:

- `Selected for full analysis`
- `Not currently selected for further analysis`
- `Ineligible`
- `Unknown`

Fully develop the leading top N rather than totally ordering the tail. Default to `N=3` and a safety cap of 5. The user may choose another cap, never above 10. Tied or incomparable candidates may fill the selected set. If a tie crosses the cutoff, include the tied group up to the cap; if it exceeds the cap, analyze it collectively or report the cutoff unresolved.

Give selected candidates comparable treatment: what each is, why it was selected, a concrete path or implications, important risks and unknowns, and when it would become preferable or cease to qualify. Recommend a sole leader only when the comparison supports one; otherwise report the leading set or portfolio.

## Disconfirmation and revision

After initial selection, try to overturn every selected candidate with comparable scrutiny:

1. State its strongest plausible failure case.
2. Identify evidence that would confirm that failure and materially change selection.
3. Seek that evidence when tools and scope permit; prefer real checks to imagined objections.
4. Label the outcome accurately as `searched and not found`, `not searched`, or `evidence of absence`.
5. Preserve unavailable evidence as `unknown` and propose the cheapest discriminating test.
6. Reapply the declared comparator, demoting or promoting candidates when warranted.

Then sensitivity-test only reasonable changes to uncertain assumptions, criterion priority, or meaningful-difference thresholds that could alter the revised top-N set. Do not vary settled facts or enumerate irrelevant changes. Report the stable core, conditional selections, and whether the conclusion is robust or unstable.

## Finish the audit

After completing the substantive result:

1. Save its exact text, beginning with `Discovery artifact` and excluding audit metadata, as `result.md` in the run directory.
2. Compute its SHA-256 with a deterministic system utility.
3. Update `receipt.txt` with the UTC finish timestamp, `status=completed`, and exact result hash.
4. Return the UUID, receipt path, result path, hash, and substantive result.

If the run fails, update the receipt when possible with a finish timestamp, `status=failed`, and a short reason. Never create a completed receipt for a partial result.

## Multiple-run verification

When the user requests multiple runs, execute them sequentially with fresh conversation context unless parallel execution is explicitly requested. Do not expose prior outputs to later runs. After independently verifying all completed receipt hashes, compare the saved `result.md` files for byte identity, discovery overlap, contracts, selected sets, conclusions, and late discoveries. Different audit metadata proves distinct execution but is not substantive variation.

## Return the process

Return, in order:

1. `Discovery artifact`: the final numbered list.
2. `Restart log`: late discoveries and affected work reconsidered, or `None`.
3. `Analysis contract`: the fixed comparison policy.
4. `Analysis`: groupings, comparisons, calculations when used, disconfirmation, sensitivity, and findings.
5. `Result`: recommendation, plan, diagnosis, synthesis, or other requested output.
6. `Uncertainties`: unknowns and assumptions that could change the result.

Keep discovery and analysis visibly distinct. Never rewrite the discovery artifact to make the analysis look cleaner. Report enough reasoning to make classifications, selected sets, and conclusions reproducible.