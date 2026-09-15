---
name: "plan-and-execute"
description: "Plan complex work deliberately, verify the plan, obtain approval by default, execute against a live Markdown plan, replan when needed, and verify the final result."
---

# Plan and execute

Use this skill when the user explicitly asks to use `plan-and-execute`, or when they ask for this specific planning-and-execution workflow for a longer or deeper task.

The purpose is not merely to "think carefully." Separate understanding, plan formation, plan verification, execution, replanning, and final verification into explicit stages, with the plan serving as the canonical working state for the task.

## Operating modes

There are two modes.

### Manual approval mode — default

Unless the user explicitly requests automated/autonomous execution:

1. Understand the task.
2. Do only the research needed to create a sound plan.
3. Create and verify the plan.
4. Present the verified plan and stop for user approval.
5. After approval, execute the plan.
6. Minor plan changes may proceed without approval but must be stated explicitly.
7. Material plan changes require a revised, re-verified plan and user approval before continuing.

Do not treat the user's request to use this skill as approval of the eventual plan.

### Automated mode

If the user explicitly asks this skill to run in automated or autonomous mode:

1. Understand the task.
2. Do the research needed to create a sound plan.
3. Create and verify the plan.
4. Proceed directly to execution without waiting for plan approval.
5. Replan as needed without approval.
6. Re-verify material replans before continuing.
7. Continue through final verification and delivery unless genuinely blocked on required user input or authorization.

Automated mode removes only this workflow's plan and replan approval gates. It does not remove planning, plan verification, replanning, final verification, permission boundaries, or any action-specific confirmation required by higher-priority instructions.

## Canonical plan artifact

Maintain the plan as a lightweight Markdown working artifact, not merely as prose in the conversation.

When a writable task/workspace filesystem is available, create or update a canonical `PLAN.md` in the task's natural working directory. If another plan filename is already established for the task, update that file instead of creating a duplicate. When persistent file storage is unavailable, maintain the same Markdown structure in the conversation and make it exportable on request.

The canonical plan represents the best current path from the present state to completion. Update it throughout execution.

Use checkboxes or equivalent status markers. Prefer concise numbered steps with enough detail that another capable agent could reasonably continue the work.

Example:

```markdown
# Plan

## Goal
Brief statement of the requested outcome.

## Success criteria
- Criterion one
- Criterion two

## Steps
- [x] 1. Inspect the existing implementation.
- [ ] 2. Research the API behavior needed for the implementation.
- [ ] 3. Implement the change.
- [ ] 4. Run relevant tests.
- [ ] 5. Verify the completed result against the request.
```

Add dependencies, decision points, risks, or verification criteria only when they materially help execution. Avoid turning the plan into project-management bureaucracy.

## Stage 1: Understand the task

Before planning:

- Identify the actual objective and expected deliverables.
- Identify constraints, success criteria, dependencies, permissions, available tools, files, systems, and relevant prior work.
- Distinguish required outcomes from suggested implementation details.
- Resolve ambiguities that would materially change the plan. If enough information is available to make a reasonable plan, state consequential assumptions rather than asking unnecessary questions.
- Do not begin substantive execution yet.

## Stage 2: Pre-plan research

Gather information that is necessary to create a sound plan.

Examples:

- Inspect relevant repositories, files, documents, configurations, or existing artifacts.
- Establish the current state of the system before deciding how to modify it.
- Determine which tools, APIs, connectors, commands, or capabilities are actually available.
- Research unfamiliar requirements, technologies, standards, constraints, or current facts when those facts affect the plan itself.

Use the dividing question:

**Do I need this information to decide how the work should be done?**

If yes, gather it before planning.

Research that is itself part of accomplishing the user's requested work belongs in the execution plan as an explicit step instead. Do not silently perform substantial task execution under the label of pre-plan research.

## Stage 3: Create the plan

Create the canonical Markdown plan.

The plan should:

- Translate the request into concrete execution steps.
- Order steps according to dependencies.
- Include research that must happen during execution.
- Include relevant testing and validation.
- Identify meaningful decision points, risks, or irreversible/external actions.
- Include the final verification work needed to demonstrate completion.
- Avoid unnecessary decomposition into trivial tool calls or mechanical actions.

Prefer outcome-oriented steps such as `Implement and test the parser change` over low-level sequences such as `open file`, `scroll`, `edit line`, and `save file`.

## Stage 4: Verify the plan

Before seeking approval or beginning automated execution, deliberately review the plan against the original task.

Check that:

- Completing the plan would actually satisfy the request.
- Every required deliverable and important success criterion is covered.
- Important constraints and permissions are respected.
- Necessary research, tests, inspections, and final verification are included.
- Dependencies are in a sensible order.
- The plan does not depend on unsupported assumptions when those assumptions can reasonably be checked.
- The plan does not include unnecessary work or broaden the scope without justification.
- External or consequential actions have the authorization they require.

Revise the canonical plan if the review reveals a problem. The user should see the verified version, not an unreviewed draft.

## Stage 5: Approval gate

In manual approval mode, present the verified plan clearly and stop before substantive execution.

The user may approve it, modify it, ask questions, or request the plan artifact.

Do not proceed until approval is given.

In automated mode, do not stop here. Continue directly into execution.

## Stage 6: Execute

Execute against the canonical plan rather than treating the plan as disposable preamble.

During execution:

- Mark completed steps as completed.
- Keep current and remaining work accurately represented.
- Use appropriate tools and evidence instead of guessing.
- Perform execution-time research where the plan calls for it.
- Produce and inspect intermediate artifacts when useful.
- Keep the plan synchronized with meaningful execution changes.
- Do not mechanically follow a step after evidence shows that it is wrong or obsolete.

For long-running work, give concise progress updates at meaningful milestones rather than narrating every tool call.

## Stage 7: Replan when necessary

Replan when new information changes the best path forward, including when:

- an assumption is invalidated;
- a planned approach fails;
- a better approach becomes clearly preferable;
- a new dependency or requirement appears;
- a planned step becomes unnecessary;
- verification exposes corrective work that was not anticipated.

Update the existing canonical plan rather than creating disconnected replacement plans.

Classify changes as **minor** or **material**.

A minor change is a tactical adjustment that does not significantly alter scope, requested deliverables, risk, cost, permissions, or the overall approach.

A material change significantly alters one or more of those dimensions, or changes a user-visible architectural/strategic choice on which the approved plan depended.

### Replanning in manual approval mode

For a minor change:

- Update the canonical plan.
- Explicitly tell the user what changed and why.
- Continue execution without waiting for approval.

For a material change:

- Update the canonical plan.
- Re-run plan verification on the revised plan.
- Explain the material change and its rationale.
- Stop and obtain user approval before continuing.

### Replanning in automated mode

For both minor and material changes:

- Update the canonical plan.
- Explicitly state meaningful changes and their rationale in progress reporting.
- Re-run plan verification for material changes.
- Continue without seeking approval.

Only stop when genuinely blocked on required information, permission, a choice the user reserved for themselves, or another dependency that cannot reasonably be resolved within the task.

## Stage 8: Verify the result

After execution, perform a deliberate final verification rather than assuming that completed steps imply a completed task.

Compare the result against:

- the original user request;
- the final canonical plan;
- stated success criteria;
- relevant tests, validation procedures, acceptance requirements, and constraints.

Where practical:

- run tests and inspect their results;
- inspect generated or modified files;
- check calculations;
- validate factual claims against suitable sources;
- confirm requested changes actually took effect;
- check for omissions, regressions, or unintended side effects;
- verify external actions by reading back state when possible.

If verification finds a correctable problem, add the corrective work to the canonical plan, execute it, and verify again. Do not merely report a defect that can reasonably be fixed within the task.

If the corrective work constitutes a material plan change in manual approval mode, apply the material-change approval rule before proceeding.

## Stage 9: Deliver

Return the completed result with a concise summary that states:

- what was accomplished;
- meaningful deviations or replans and why they occurred;
- how the result was verified and whether verification passed;
- unresolved limitations or blockers, if any.

The final canonical plan should accurately reflect completed, skipped, replaced, and unresolved work. Preserve it as the execution record and make it viewable or downloadable when requested.

## Guardrails

- System, developer, user, safety, permission, and tool rules always take precedence over this skill.
- Planning is not authorization. Automated mode only changes this skill's plan-approval behavior; all higher-priority permission and confirmation requirements still apply.
- Do not use this workflow to manufacture delays or extra approval steps. The purpose is better execution, not ceremony.
- In automated mode, do not request approval merely for the plan or for replanning unless a higher-priority rule or the user separately requires confirmation for the underlying action.
- Do not skip the initial approval gate in manual mode merely because execution appears straightforward after planning.
- A plan is allowed to change; an unexplained stale plan is not.
