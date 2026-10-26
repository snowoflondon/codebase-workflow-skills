---
name: repo-understanding
description: Build or refresh an evidence-based, high-level understanding of a software repository so a developer can explain what it does, how it is structured, and how its main execution or usage flow works. Use for onboarding, repository refreshers, or before making changes.
---

# Repository Understanding

Follow the [shared skills contract](../../docs/design-principles.md).

## Purpose

Help a developer understand or refresh their understanding of a repository well enough to explain it to someone else. Investigate the orientation topics below, but report only what is relevant and useful. Detailed planning, diagramming, test design, review, and documentation work belong to their respective toolkit skills.

## When to invoke

- The user is onboarding to or returning to a repository, preparing to work in it, or asks for a refresher or high-level walkthrough.

## When not to invoke

- The user wants a detailed proposed implementation: use `change-planner`.
- The user wants a diagram or detailed component relationship analysis: use `architecture-visualizer`.
- The user wants test cases, a diff review, a documentation impact assessment, or a change summary: use `test-designer`, `code-reviewer`, `documentation-maintainer`, or `git-change-summarizer` respectively. Applying documentation edits requires an authorized editing workflow.
- The request is limited to a narrow bug, security audit, performance investigation, or operational diagnosis; use a more focused investigation rather than implying this orientation covers it.

## Required inputs

- The repository or workspace to inspect.
- Any user-stated focus, audience, or depth preference.

If the repository is unavailable, partial, or unusually large, state the limitation and scope the investigation to accessible, high-signal evidence. Do not imply an exhaustive audit.

## Evidence to inspect

Inspect relevant repository guidance, documentation, layout, manifests, scripts, source, configuration, tests, CI/deployment files, and Git status or diffs when local changes affect the explanation. Verify directory responsibilities from contents, not names alone. Cite paths, symbols, or configuration where practical.

Classify conclusions as:

- **Verified:** directly supported by inspected repository evidence.
- **Hypothesis:** plausible interpretation that is not confirmed.
- **Unknown:** not established by available evidence.
- **Contradiction:** relevant sources disagree; cite both sides.

Do not infer purpose, users, or behavior from the repository name alone.

## Workflow

1. Confirm the repository, user focus, and applicable instructions; scale the investigation to the requested depth.
2. Establish the repository's purpose and users from documentation, metadata, examples, interfaces, or deployment evidence.
3. Map architecture and core directories, verifying responsibilities from representative contents.
4. Identify inputs, outputs, and entry points; trace a representative execution or usage flow to an observable result. If none applies or the trace is incomplete, say so.
5. Identify dependencies, configuration assumptions, and documented developer commands from repository evidence. Report exact commands with their sources; do not run them or expose secret values.
6. Suggest a short learning order and areas to defer when evidence supports them; tailor these to the user's familiarity.
7. Check for material risks, missing links, and contradictions. Apply the evidence classifications above and route deeper work to the appropriate skill.

## Allowed actions

Read and search repository files or supplied context, compare evidence, and report documented commands without running them. Inspect Git status or diffs when relevant.

## Forbidden actions

Do not modify files, run commands, install dependencies, or perform side effects. Never expose secret values, invent commands, claim unobserved execution results, or commit, push, merge, deploy, provision resources, or discard working-tree changes.

## Output format

Start with a concise, plain-language refresher. The workflow topics are mandatory to consider, not mandatory report sections: include only repository-relevant, evidence-supported details and materially useful, labeled unknowns. Omit irrelevant or empty sections. Use a short walkthrough or clear headings, citing paths or symbols for claims; apply the evidence labels above where useful.

## Completion checklist

- All workflow topics were considered; the response includes only relevant findings and material uncertainties, supported by evidence.
- Commands and other repository-specific details are verified; no commands were run and no secrets exposed.
- The response fits the user's familiarity and depth, notes material limitations, and involves no side effects.

## Example invocations

- “I’m returning to this repository after a few months. Can you remind me what it does and walk me through the main flow?”
- “I’m new to this repository. Give me a high-level tour so I can explain the demo to my team.”

## Failure and uncertainty handling

If evidence or access is limited, state the limitation and narrow the result. Label unverified conclusions and conflicting evidence using the classifications above; never guess. Decline edits or execution and route those requests to an appropriate authorized workflow.
