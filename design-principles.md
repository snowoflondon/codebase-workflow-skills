# Shared Skills Contract

## Goal and scope

This repository contains seven reusable agent skills for investigating software projects:

1. `repo-understanding` (Understand)
2. `change-planner` (Plan)
3. `architecture-visualizer` (Visualize)
4. `test-designer` (Test)
5. `code-reviewer` (Review)
6. `documentation-maintainer` (Document)
7. `git-change-summarizer` (Deliver)

## Workflow phases

The skills are grouped into five optional phases:

| Phase | Skills |
| --- | --- |
| Orient | `repo-understanding` |
| Plan and model | `change-planner`, `architecture-visualizer` |
| Design verification | `test-designer` |
| Review | `code-reviewer` |
| Document and deliver | `documentation-maintainer`, `git-change-summarizer` |

This is a flexible path, not a required pipeline: use only the skills relevant to the task and revisit a phase when new evidence warrants it. Implementation is outside this toolkit; its skills investigate, plan, and report but do not make project changes.

Each skill should be reusable across projects, languages, and technology stacks. Its purpose is investigative: inspect relevant evidence, explain findings, and produce a clearly scoped artifact.

## Shared contract

Every skill must document and follow each section below. A skill may tailor the details to its purpose, but should not omit a section. Project-specific instructions and the user's request take precedence where they explicitly define scope or constraints.

### Name

Use the skill's canonical name consistently in its directory, metadata, and documentation.

### Purpose

State the single primary investigative outcome and define its ownership boundary and handoffs. Do not duplicate another skill's core responsibility.

### When to invoke

List the user goals, questions, or conditions that make this skill a good fit. Prefer observable triggers over vague advice.

### When not to invoke

Identify nearby tasks that belong to another skill, situations with insufficient scope or evidence, and requests that require changes or execution beyond this skill's permissions.

### Required inputs

Specify the minimum context needed to begin, optional context that improves results, and how to proceed when inputs are missing. Do not imply that absent inputs were inspected.

### Evidence to inspect

Inspect relevant source files, symbols, tests, configuration, documentation, Git status and diffs, execution output, and user-provided constraints before drawing conclusions. Cite paths, symbols, diff sections, or output where practical. In the result, distinguish verified findings (directly supported by inspected evidence), hypotheses (plausible but unverified), unknowns (not established), and contradictions (conflicting evidence); never present an inference as verified fact.

### Workflow

Describe a repeatable, appropriately scoped investigation. Start by confirming scope, inspect the most relevant evidence, analyze it against the skill's purpose, and validate conclusions where feasible. Avoid broad repository exploration when a targeted check is sufficient. The workflow may be iterative and should state when to hand off to another skill.

### Allowed actions

Default to read-only actions: search, read, compare, reason, and report. Skills may propose changes or tests without applying or running them. Any side effect must be explicitly permitted by that skill and authorized by the user for the current task.

### Forbidden actions

Do not modify, create, or delete project files without explicit authorization, or claim to have run checks that were not run. Never invent run, test, build, or deployment commands: verify them in repository scripts, configuration, or documentation, or state that they are unknown. Do not commit, push, merge, deploy, provision cloud resources, install dependencies, discard working-tree changes, or perform other delivery or environment-changing actions without explicit user permission. Do not expose secret values or expand scope based on assumptions. Authorization permits an action only when the skill and applicable instructions allow it.

### Output format

Define a predictable, concise structure suited to the skill, with clear headings or fields. Separate findings from recommendations, link findings to evidence when possible, and state what was not inspected or validated if that affects confidence.

### Completion checklist

Before responding, confirm that the requested scope was addressed, conclusions are supported by inspected evidence, assumptions and gaps are explicit, the output uses the defined format, and no unauthorized side effects occurred.

### Example invocations

Examples should show the intended investigation and its scope. Adapt these patterns to the project:

- `repo-understanding`: "Explain this repository's main components and how a request flows through them."
- `change-planner`: "Investigate what a change to [behavior] would affect and outline a plan; do not edit files."
- `architecture-visualizer`: "Inspect [subsystem] and diagram its components and dependencies."
- `test-designer`: "Review [behavior] and propose focused tests, without running or adding them."
- `code-reviewer`: "Review this diff for correctness and regression risks; report findings only."
- `documentation-maintainer`: "Identify documentation that may be affected by [change] and recommend updates; do not edit files."
- `git-change-summarizer`: "Summarize the current diff as a concise change report; do not stage or commit anything."

### Failure and uncertainty handling

If inputs or evidence are unavailable, say what is missing and how it limits the result. If evidence conflicts, describe the conflict rather than choosing silently. Mark conclusions as uncertain when they rely on assumptions, and propose a small next investigation that could resolve material uncertainty. If the request exceeds the skill's permissions or scope, explain the boundary and provide a read-only result or handoff where possible.

## Design considerations

The seven-stage model is easy to understand, but should not imply every task needs all seven skills. Make skipping and iteration explicit, keep ownership and handoffs distinct, and state the read-only boundary in each skill. Evidence-linked outputs and transparent uncertainty make the skills more reusable and trustworthy across projects.
