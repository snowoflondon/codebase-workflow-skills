# Codebase Workflow Skills

Codebase Workflow Skills is a collection of reusable agent skills for common software-engineering workflows.

The skills aim to help understand a codebase, reason about change, and communicate evidence-based findings without taking unrequested action.

## Investigation lifecycle

The skills are organized around this progression:

**Understand → Plan → Visualize → Test → Review → Document → Deliver**

This is a menu, not a required pipeline. Use only the skills relevant to the question, and revisit earlier work if new evidence changes the investigation.

## Skills

| Stage | Skill | Intended focus |
| --- | --- | --- |
| Understand | [`repo-understanding`](skills/repo-understanding/SKILL.md) | Map the repository, its components, and important flows. |
| Plan | [`change-planner`](skills/change-planner/SKILL.md) | Investigate the impact and outline an approach to a proposed change. |
| Visualize | [`architecture-visualizer`](skills/architecture-visualizer/SKILL.md) | Explain architecture and relationships with diagrams or structured views. |
| Test | [`test-designer`](skills/test-designer/SKILL.md) | Identify behavior to verify and propose focused tests. |
| Review | [`code-reviewer`](skills/code-reviewer/SKILL.md) | Examine changes for defects, risks, and missing coverage. |
| Document | [`documentation-maintainer`](skills/documentation-maintainer/SKILL.md) | Identify documentation affected by a change and recommend updates. |
| Deliver | [`git-change-summarizer`](skills/git-change-summarizer/SKILL.md) | Summarize the current change set for clear handoff. |

## Shared principles

All skills follow the [shared skills contract](docs/design-principles.md). In brief, they are:

- **Reusable and investigative:** inspect relevant project evidence and report scoped findings.
- **Evidence-based:** support conclusions with inspected files, symbols, tests, configuration, documentation, Git state, or execution output; distinguish facts from assumptions.
- **Read-only by default:** do not edit files or perform side effects unless explicitly authorized and permitted by the skill.
- **Non-delivering by default:** never automatically commit, push, merge, deploy, provision resources, install dependencies, or discard working-tree changes.

## Project status

This repository is an initial proof of concept. All seven skills have defined workflows. No setup or invocation tooling is included yet.
