---
name: "business-idea-research"
description: "Generate, validate, compare, and stress-test business ideas with sourced market research."
---

# Business idea research

Use when asked to find, assess, compare, or validate ways to make money, products, services, micro-SaaS ideas, or business opportunities.

## Scope first

Extract constraints from the request: available capabilities, capital, time, geography, customer type, acceptable sales model, forbidden dependencies, and desired scale. State consequential assumptions. Ask only when an unknown would materially change the search.

## Choose research depth

- `scan`: Generate and lightly screen ideas. Fast; competition checks are directional.
- `standard`: Shortlist ideas and verify the leading candidates with sourced market research.
- `deep`: Use a durable TaskFlow job. Investigate finalists across multiple stages and retain intermediate state across turns or restarts.

Default to `standard`. Use `deep` when the user requests thoroughness, the decision carries meaningful cost, or several finalists need real validation. Give progress updates during long runs.

## Workflow

1. Define prioritized comparison criteria from the user's actual constraints. Include customer pain, willingness to pay, reachability, competition, differentiation, build/operating burden, risk, and fit. Give decisive criteria observable anchors.
2. Generate a diverse candidate set. Discovery-and-analysis may be used for divergent ideation, but do not treat its initial ordering as market evidence.
3. Eliminate ideas that violate hard constraints or depend on vague access, contacts, data, distribution, or user resources the prompt excludes.
4. Use ordinal top-N selection to shortlist 3–5 candidates before spending heavily on research. Preserve ties and incomparability. Label other eligible ideas `not currently selected for further analysis`, not rejected.
5. For each finalist, research:
   - direct competitors and close substitutes;
   - current pricing, packaging, target customer, and positioning;
   - evidence of demand: purchases, reviews, job posts, active communities, search behavior, public revenue/customer claims, or repeated complaints;
   - customer-acquisition paths and whether a new entrant can realistically reach buyers;
   - differentiation, switching costs, defensibility, and likely incumbent response;
   - implementation, support, compliance, platform, abuse, and unit-economics risks.
6. Distinguish verified facts, vendor claims, estimates, and inference. Link sources and record access dates for volatile facts. Do not use the absence of found competitors as proof of an open market.
7. Search specifically for failure evidence: abandoned products, weak reviews, saturated listings, free substitutes, acquisition bottlenecks, and reasons buyers tolerate the current problem.
8. Revise the product concept in response to evidence. Preserve the original description. A competitor can validate demand while invalidating an undifferentiated implementation.
9. Recompare finalists only after research using the declared criterion priority. Explain major changes in selection, ordering, ties, or candidate definitions from the initial screen. Use numeric scoring only when inputs have defensible measurements or the user explicitly requests it.
10. Return a clear verdict for each researched finalist: `pursue`, `modify`, `hold`, or `reject`. Do not force a sole winner when evidence supports a tied or incomparable leading set.

## Minimum evidence standard

For every recommended idea:

- Identify at least 3 relevant competitors or substitutes when they exist.
- Inspect primary product/pricing pages, not only search snippets or listicles.
- Include at least 2 independent demand signals when obtainable.
- Name the likely first acquisition channel and why it is credible.
- State the proposed wedge in one sentence and compare it directly with incumbents.
- Name the most likely reason the business fails.
- Propose the cheapest useful validation experiment with a falsifiable success threshold.

If evidence is thin, label confidence low and recommend research or a test—not confidence disguised as a rank or score.

## Output

Lead with the verdict and the best-supported opportunity or leading set. Then provide:

- constraints and assumptions;
- selected finalists, including ties or incomparability;
- ideas not currently selected for further analysis;
- competitor/pricing evidence;
- demand and acquisition evidence;
- revised wedge;
- risks and failure case;
- cheapest validation experiment;
- sources.

Prefer a small comparison table when several finalists use the same fields. Keep unselected ideas brief unless the user asks for the full funnel.

## Long-running work

For `deep` runs, use TaskFlow to persist the goal, current stage, shortlisted candidates, evidence gathered, unresolved questions, and child research tasks. Stages should be resumable and independently checkable. Notify the owner at meaningful milestones, when blocked, and on completion. Do not silently broaden the user's authorized external actions; market research is read-only unless the user separately authorizes outreach, purchases, publication, or account creation.
