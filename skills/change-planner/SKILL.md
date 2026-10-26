---
name: change-planner
description: Investigate a desired software change and produce an evidence-based, ordered implementation plan for the current repository. Use when a user wants to understand change impact and plan work, not have the change implemented.
---

# Change Planner

Follow the [shared skills contract](../../docs/design-principles.md).

## Purpose

Assess how a user-requested change fits the current repository and produce a practical implementation plan. Describe current versus desired behavior, affected execution paths, files and interfaces, risks, test requirements, documentation impact, non-goals, and an ordered sequence of changes. This is an investigation and planning skill: it does not implement, test, or otherwise modify the project.

## When to invoke

- The user has a desired change, feature, or implementation goal and wants its impact assessed or work planned.
- The user asks what would need to change, what parts of the repository are affected, or how to approach an implementation.

## When not to invoke

- The user wants code changed or commands/tests run; this skill only plans. Use an authorized implementation or validation workflow.
- The user needs a general repository tour without a specific desired change; use `repo-understanding`.
- The user wants a detailed architecture diagram, test-case design, review of an existing diff, documentation impact assessment, or a change summary; use `architecture-visualizer`, `test-designer`, `code-reviewer`, `documentation-maintainer`, or `git-change-summarizer` respectively. Applying documentation edits requires an authorized editing workflow.

## Required inputs

- The repository or workspace to inspect.
- The requested outcome or desired behavior.
- Any stated constraints, priorities, or non-goals.

If the request is ambiguous, identify the decisions that materially affect the plan. Ask concise clarifying questions when necessary; otherwise present a clearly labeled conditional plan rather than silently choosing assumptions.

## Evidence to inspect

Inspect evidence relevant to the requested change, such as:

- Applicable repository instructions and existing documentation.
- Current Git status and diffs when available, to avoid planning against or overwriting unrelated work.
- Source files, symbols, callers, and interfaces on the affected execution path.
- Related tests, configuration, dependency manifests, and documented developer workflows.

Use a `repo-understanding` report if the user provides one, but treat it as a starting point: verify relevant details against the current repository. If no report is available, perform focused discovery sufficient to plan this change; do not require or reproduce a full repository tour. Cite paths, symbols, interfaces, or other evidence for repository-specific claims. Classify conclusions as:

- **Verified:** directly supported by current repository evidence.
- **Hypothesis:** plausible but not confirmed.
- **Unknown:** not established from available evidence.
- **Contradiction:** relevant sources disagree; cite both sides.

Restate desired behavior as the user's goal, not as a verified repository fact.

## Workflow

1. Restate the desired outcome, constraints, and non-goals. Resolve or flag ambiguities that would materially change the plan.
2. Inspect relevant repository guidance and current working-tree state. Use a supplied repository overview if available and verify details relevant to the change; otherwise perform targeted discovery.
3. Establish current behavior from the affected code, interfaces, tests, configuration, and documentation. Trace the execution path from entry point through affected components to observable behavior.
4. Compare current behavior with the desired outcome. Identify affected files, symbols, interfaces, dependencies, and compatibility boundaries; distinguish verified impact from hypotheses.
5. Define the ordered implementation steps, including dependencies between steps and the intended outcome of each. Keep recommendations scoped to the requested change.
6. Identify test requirements, validation risks, and documentation updates. Recommend checks or test scenarios, but do not add or run them. Only cite commands verified in repository sources; if none are verified, describe validation needs without inventing commands.
7. Check risks, non-goals, open questions, unknowns, and contradictions. Hand off detailed design, test-case authoring, implementation, or review to the appropriate workflow or toolkit skill.

## Allowed actions

Read, search, compare, and reason over repository files and user-provided context. Inspect Git status or diffs when available. Produce recommendations and a plan only.

## Forbidden actions

Do not edit files, run commands or tests, install dependencies, or perform other side effects. Do not invent commands or claim unobserved execution results. Never expose secret values, commit, push, merge, deploy, provision resources, or discard working-tree changes.

## Output format

Provide a concise, evidence-linked plan with these fields. Include each field when relevant; mark materially important unknowns or contradictions explicitly rather than filling the plan with unsupported or empty sections.

1. **Goal and behavior delta:** Desired behavior and verified current behavior.
2. **Affected path and interfaces:** Execution path, files, symbols, APIs, data contracts, or other boundaries affected.
3. **Ordered implementation plan:** Sequenced steps, dependencies, and expected outcome for each.
4. **Test and validation requirements:** Behaviors and layers to verify; do not execute checks.
5. **Documentation impact:** Documents or guidance likely to change, if any.
6. **Risks and assumptions:** Evidence-backed risks, hypotheses, unknowns, and contradictions.
7. **Non-goals and open questions:** Explicit exclusions and unresolved decisions that affect scope or sequencing.

## Completion checklist

- Current and desired behavior are distinguished and grounded appropriately.
- The affected path, files, and interfaces and an ordered sequence are identified, or their uncertainty is explicit.
- Test requirements, documentation impact, risks, and non-goals are addressed when relevant.
- Recommendations cite evidence; assumptions and contradictions are labeled.
- No files, commands, tests, or other side effects were used to implement or validate the plan.

## Example invocations

- “I want to add [behavior]. Inspect this repository and give me an evidence-based implementation plan; do not make changes.”
- “What would need to change to support [desired outcome]? Include affected interfaces, risks, tests, and docs.”
- “Use this repository overview as context, verify the relevant details, and plan [change].”

## Failure and uncertainty handling

If repository evidence or access is limited, state the limitation and narrow the plan. If current behavior or impact cannot be verified, label it using the classifications above and make dependent steps conditional. For conflicting evidence, cite both sources. If the goal is underspecified, ask focused questions or state the assumptions a provisional plan depends on. Decline implementation or execution requests and route them to an authorized workflow.
