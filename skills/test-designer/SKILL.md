---
name: test-designer
description: Analyze repository behavior and requirements to propose focused, evidence-based test scenarios and identify coverage gaps. Use when a user wants to know what should be tested, not to write or run tests.
---

# Test Designer

Follow the [shared skills contract](../../docs/design-principles.md).

## Purpose

Turn a requested behavior, change, or existing requirement into focused test scenarios grounded in the current repository and its conventions. Identify relevant existing coverage and gaps without writing test code, modifying files, or executing tests.

This skill specifies concrete scenarios; `change-planner` may identify high-level test requirements as part of a broader implementation plan. Reviewing an implemented diff belongs to `code-reviewer`.

## When to invoke

- The user asks what should be tested for a feature, behavior, or proposed change.
- The user wants test scenarios, expected outcomes, suitable test levels, or coverage gaps identified.
- The user wants to assess existing test coverage for a specific behavior without running tests.

## When not to invoke

- The user wants tests written, files changed, or tests executed; use an authorized implementation or validation workflow.
- The user wants an implementation impact plan with only high-level test requirements: use `change-planner`.
- The user wants findings on defects in an existing code diff: use `code-reviewer`.
- The request is a specialized security, performance, or operational test assessment; use a focused process suited to that domain.

## Required inputs

- The repository or workspace to inspect.
- The behavior, requirement, feature, or change to assess.
- Acceptance criteria and constraints when available.

If expected behavior is unclear, ask focused questions when the answer changes the scenarios materially. Otherwise, provide conditional scenarios and label assumptions rather than inventing requirements.

## Evidence to inspect

Inspect evidence relevant to the target behavior, such as:

- Applicable repository instructions and user-provided acceptance criteria.
- Source code, public interfaces, and behavior on the relevant path.
- Existing tests and fixtures around the behavior.
- Test configuration, helpers, and neighboring test conventions.
- Relevant configuration, schemas, or documentation that define observable behavior.

Use a supplied `repo-understanding` report or `change-planner` plan as optional context, then verify relevant details against current repository evidence. If neither is available, do focused discovery; neither skill is a prerequisite. Cite paths, symbols, test names, or interfaces where practical. Classify conclusions as:

- **Verified:** directly supported by inspected repository evidence.
- **Hypothesis:** plausible but unconfirmed.
- **Unknown:** not established from available evidence.
- **Contradiction:** relevant sources disagree; cite both sides.

Do not claim existing coverage without inspecting the relevant tests. Do not treat current implementation behavior alone as proof of desired behavior.

## Workflow

1. Confirm the target behavior, constraints, and acceptance criteria; scope the investigation to the user's question.
2. Inspect the relevant code path, interfaces, existing tests, and repository testing conventions.
3. Translate supported requirements into observable outcomes. Flag ambiguous or missing expected behavior rather than guessing.
4. Identify a small set of meaningful scenarios: normal behavior, boundaries, invalid inputs, error paths, or regressions as relevant. Do not force every category into every design.
5. Recommend a suitable test level for each scenario (for example, unit, integration, contract, or end-to-end) based on the behavior and repository architecture. Follow existing project conventions; do not prescribe a test pyramid mechanically.
6. Compare proposed scenarios with inspected existing coverage and report material gaps, risks, assumptions, and unknowns.

## Allowed actions

Read, search, compare, and reason over repository files and supplied context. Propose test scenarios and validation requirements only.

## Forbidden actions

Do not create or modify files, write test code, run tests or other commands, install dependencies, or perform other side effects. Do not invent commands or claim unobserved test results. Never expose secret values, commit, push, merge, deploy, provision resources, or discard working-tree changes.

## Output format

Start with a brief scope statement. Summarize relevant existing coverage separately from proposed scenarios. Use a concise table when scenarios benefit from comparison, with fields such as **Scenario**, **Setup/input**, **Action**, **Expected observable result**, **Test level**, and **Evidence/rationale**. Include only relevant cases; label assumptions, unknowns, and contradictions. End with material coverage gaps or open questions, if any. Do not include test implementation code or commands.

## Completion checklist

- Scenarios address the requested behavior and have evidence-backed or clearly qualified expected outcomes.
- Existing coverage is distinguished from proposed coverage; material gaps and uncertainties are identified.
- Test levels fit the repository's architecture and conventions.
- No files, commands, tests, or other side effects were used; no secret values are exposed.

## Example invocations

- “For this behavior, propose focused test scenarios and expected outcomes. Do not write or run tests.”
- “Inspect the existing tests for [feature] and identify important coverage gaps.”
- “Use this change plan as context to design verification scenarios; validate relevant behavior and interfaces in the repository.”

## Failure and uncertainty handling

If repository evidence or access is limited, state the limitation and narrow the result. If requirements or expected outcomes are unclear, ask focused questions or label conditional scenarios and assumptions. For conflicting sources, cite both and describe the conflict. If existing coverage cannot be established, say so rather than inferring from filenames. Decline requests to write or execute tests and route them to an authorized workflow.
