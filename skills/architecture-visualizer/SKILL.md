---
name: architecture-visualizer
description: Create a lightweight, evidence-based Mermaid view of how relevant parts of a software repository fit together. Use when a user asks to visualize system context, components, interactions, or data flow; no other toolkit skill is required first.
---

# Architecture Visualizer

Follow the [shared skills contract](../../docs/design-principles.md).

## Purpose

Help a user understand how relevant parts of the current repository fit together by producing a concise Mermaid diagram grounded in repository evidence. This skill models the existing system; it does not redesign it, plan a requested change, or implement anything.

## When to invoke

- The user wants an architecture or flow diagram for a repository, subsystem, or specific behavior.
- The user asks how components, external systems, interfaces, or data flows relate.
- A visual model would help understand or discuss a system or planned change.

This skill can be invoked independently. If a `repo-understanding` report or `change-planner` plan is provided, use it as context and verify diagram-relevant details against current repository evidence.

## When not to invoke

- The user wants a broad verbal repository tour without a diagram: use `repo-understanding`.
- The user wants a change-impact plan rather than a model of the existing system: use `change-planner`.
- The user requests implementation, a test plan, code review, a documentation impact assessment, or a change summary; route to the corresponding workflow or toolkit skill. Applying documentation edits requires an authorized editing workflow.

## Required inputs

- The repository or workspace to inspect.
- The system, subsystem, behavior, or question to visualize. If unspecified, choose a high-level system view only when repository evidence makes its scope clear; otherwise ask a focused question.
- Any supplied overview, plan, audience, or detail preference.

## Evidence to inspect

Inspect relevant repository instructions, documentation, source files, entry points, interfaces, configuration, and dependency or deployment definitions. Use targeted inspection to establish components and relationships; do not infer connections from filenames or directory names alone. Cite paths, symbols, or interface definitions for diagram elements and relationships.

Classify conclusions as:

- **Verified:** directly supported by repository evidence.
- **Hypothesis:** plausible but unconfirmed; label it in the diagram or evidence notes.
- **Unknown:** not established; do not draw it as fact.
- **Contradiction:** sources disagree; describe the conflict and cite both.

Never include secret values in diagrams or notes.

## Workflow

1. Confirm the target scope and the relationship the user wants to understand. Keep the investigation focused.
2. Inspect relevant files and trace only the components, boundaries, interactions, or data transformations needed to answer the question. A prior toolkit report is optional context, not a prerequisite.
3. Choose the smallest useful Mermaid view: system context for actors and boundaries; a component flowchart for structure and dependencies; a sequence diagram for interactions over time; or a data-flow view for movement and transformation. Use more than one view only when each answers a distinct, necessary question.
4. Keep the diagram easy to scan: include the important nodes and labeled relationships, omit unrelated implementation detail, and split or simplify an oversized view rather than compressing everything into one diagram.
5. Check that each material node and relationship is evidence-backed. Label inferred relationships as hypotheses, and state unknowns or contradictions separately.
6. If the workstation documents how to invoke its Mermaid CLI, use it to check syntax and layout. Do not guess the command or install anything; if the invocation is unavailable or rendering fails, report the diagram as unvalidated. Keep temporary files outside the repository and remove them. Do not run repository commands.
7. Provide brief reading guidance and an evidence map for important diagram elements.

## Allowed actions

Read, search, compare, and reason over repository files and supplied context. Produce Mermaid diagrams and concise explanatory notes. Use the preinstalled Mermaid CLI only to render and validate the generated diagram, and only with a documented invocation; any temporary artifacts must remain outside the repository and be removed afterward. Repository files remain read-only.

## Forbidden actions

Do not modify repository files, run repository commands, install dependencies, or use the Mermaid CLI for purposes other than rendering the generated diagram. Do not leave temporary artifacts behind. Do not invent components or relationships, present hypotheses as verified, expose secret values, or commit, push, merge, deploy, provision resources, or discard working-tree changes.

## Output format

Provide a short scope statement, then one primary fenced `mermaid` diagram. Add another diagram only when it answers a distinct necessary question. Follow with a brief explanation, a compact evidence map linking important nodes and edges to paths or symbols, and only material assumptions, unknowns, or contradictions. State whether CLI rendering succeeded; if it fails, report the limitation. Omit irrelevant or unsupported details.

## Completion checklist

- The diagram answers the stated question and uses the simplest useful Mermaid view.
- Important components and relationships are supported by repository evidence or clearly labeled as hypotheses.
- The diagram is scannable; unknowns, contradictions, and limitations are not hidden.
- Supporting paths or symbols are cited, no secret values are exposed, and any temporary render artifacts were removed without modifying the repository.

## Example invocations

- “Draw a Mermaid component view of this service and show how its main components depend on each other.”
- “Visualize the system context and the data flow for [behavior]. Keep it to the parts relevant to that flow.”
- “Use this change plan as context and diagram the existing execution path it affects; verify the relationships in the repository.”

## Failure and uncertainty handling

If access or evidence is insufficient, narrow the diagram or explain why a relationship cannot be established. Label unverified relationships as hypotheses and describe conflicting sources rather than choosing silently. Ask for scope clarification when a useful diagram cannot otherwise be selected. Decline requests to edit files or execute commands.
