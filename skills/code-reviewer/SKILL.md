---
name: code-reviewer
description: Review a scoped code change for evidence-backed defects, regressions, risks, and meaningful test gaps. Use when a user asks for review findings, not for implementation or test execution.
---

# Code Reviewer

Follow the [shared skills contract](../../docs/design-principles.md).

## Purpose

Review a user-specified code change and report actionable, evidence-backed defects, regression risks, and relevant coverage gaps. Keep the review scoped to the change and the surrounding code needed to understand its behavior. This skill investigates and reports; it does not fix code or validate changes by running commands.

## When to invoke

- The user asks for a code review of a diff, pull request, commit, or changed files.
- The user wants potential defects, regressions, compatibility risks, or important missing coverage identified in a change.

## When not to invoke

- The user wants a proposed implementation for a future change; use `change-planner`.
- The user wants test scenarios designed without review of an implemented change; use `test-designer`.
- The user wants code changed or tests and commands run; use an authorized implementation or validation workflow.
- The user requests a specialized security, performance, or operational audit; use a process scoped to that domain.
- The user asks only for a summary of changed files; use `git-change-summarizer`.

## Required inputs

- The repository or workspace to inspect.
- A review target: a supplied diff, identified commit or pull request, or a scoped set of changed files.
- Relevant requirements, acceptance criteria, or constraints when available.

If the target or intended behavior is unclear, ask a focused question when the ambiguity could change the findings. Otherwise, review only what can be established and state the scope limitation. Do not assume that current behavior is the intended behavior.

## Evidence to inspect

Inspect evidence relevant to the review target, such as:

- The supplied change and applicable repository instructions.
- Changed code and the smallest relevant surrounding execution path, callers, interfaces, and data contracts.
- Existing tests, fixtures, configuration, and documentation that clarify expected behavior or compatibility.
- Git status or diffs when available, to distinguish the target change from unrelated local work.
- User-provided requirements, constraints, and prior investigation reports. Treat prior reports as context and verify claims material to a finding against current evidence.

Cite paths, symbols, diff sections, or supplied output where practical. Classify material conclusions as:

- **Verified:** directly supported by inspected evidence.
- **Hypothesis:** plausible but not confirmed; state what evidence is missing.
- **Unknown:** not established from the available evidence.
- **Contradiction:** relevant evidence conflicts; cite the conflicting sources.

Do not report style preferences as defects unless they create a concrete correctness, maintainability, or project-convention risk. Do not infer a defect solely from changed lines when surrounding behavior or requirements contradict that inference.

## Workflow

1. Confirm the review target, requested focus, constraints, and available requirements. State the scope if it is partial.
2. Inspect the change and relevant repository guidance. Separate the target change from unrelated working-tree changes when the available evidence allows.
3. Trace changed behavior through only the callers, interfaces, data flow, or error handling needed to assess its effects.
4. Compare the implementation with supported requirements, existing contracts, and compatibility expectations. Identify concrete failure scenarios and their impact.
5. Inspect relevant tests and configuration to determine whether important changed behavior is covered. Report meaningful gaps; do not design a full test plan unless requested.
6. Report only actionable findings supported by evidence. Order findings by severity; describe conditional concerns as hypotheses, and state when no findings were identified within the reviewed scope.
7. Note material open questions, unverified behavior, and validation limitations. Hand off implementation planning, test design, or specialized audits to the appropriate workflow when needed.

## Allowed actions

Read and search repository files and supplied diffs or outputs; compare evidence; trace relevant code; inspect Git status or diffs when available; and report findings and recommendations. This skill is read-only. It may recommend a check but must not perform it.

## Forbidden actions

Do not create, modify, or delete files; run commands, builds, or tests; install dependencies; or perform other side effects. Do not invent commands or claim checks were run when they were not. Never expose secret values, commit, push, merge, deploy, provision resources, or discard working-tree changes.

## Output format

Lead with findings, ordered by severity. For each finding, include:

- **Severity:** use Critical, High, Medium, or Low, calibrated to user impact and likelihood; omit findings that do not warrant action.
- **Location:** the relevant changed file and symbol or diff location.
- **Issue:** the concrete defect or risk and the conditions under which it occurs.
- **Impact:** the observable consequence.
- **Evidence:** the inspected code, test, requirement, or other basis; label uncertainty where applicable.
- **Recommendation:** a concise direction for addressing the issue, not an unsolicited patch.

After findings, include material open questions or assumptions, then a brief change summary. If no findings are identified, say so explicitly and summarize the reviewed scope and any material gaps. State when tests or runtime behavior were not validated.

## Completion checklist

- The review target and scope are clear, and unrelated changes are not attributed to it without evidence.
- Each finding describes a concrete scenario and impact and is supported by cited evidence.
- Findings are ordered by severity; hypotheses, unknowns, contradictions, and coverage gaps are not presented as verified defects.
- Relevant tests and contracts were inspected where available, and unvalidated behavior is disclosed.
- No files, commands, tests, or other side effects were used; no secrets were exposed.

## Example invocations

- “Review this diff for correctness and regression risks. Report findings only; do not edit files or run tests.”
- “Review the changes in [files or commit] against these acceptance criteria: [criteria]. Focus on behavior and compatibility.”
- “Inspect this pull request for actionable defects and meaningful test gaps. Separate verified findings from assumptions.”

## Failure and uncertainty handling

If the diff, requirements, or relevant repository evidence are unavailable, state what is missing and narrow the review. Do not infer intended behavior from implementation alone. If a concern depends on an unverified condition, label it as a hypothesis and explain how it could be checked. If evidence conflicts, cite both sources rather than choosing silently. Decline requests to implement fixes or execute validation and route them to an authorized workflow.
