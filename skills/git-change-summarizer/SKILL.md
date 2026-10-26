---
name: git-change-summarizer
description: Summarize a scoped Git change set as a concise, evidence-based handoff or pull request summary. Use for describing what changed, not reviewing quality or modifying Git state.
---

# Git Change Summarizer

Follow the [shared skills contract](../../docs/design-principles.md).

## Purpose

Produce a concise, accurate summary of a user-specified repository change set for handoff, a pull request, or another communication purpose. Describe what the available evidence shows changed, without evaluating correctness or inferring intent. This skill is read-only and does not alter Git state.

## When to invoke

- The user asks for a summary of current changes, a diff, commit, pull request, or specified revision range.
- The user wants a concise handoff or draft change summary grounded in the actual changed files.

## When not to invoke

- The user wants defects, regressions, or risk findings; use `code-reviewer`.
- The user wants to know what implementation work is needed; use `change-planner`.
- The user wants to assess documentation affected by a change; use `documentation-maintainer`. Applying documentation updates requires an authorized editing workflow.
- The user wants test scenarios or coverage gaps assessed; use `test-designer`.
- The user wants files staged, committed, pushed, merged, or otherwise changed in Git; use an explicitly authorized workflow for that action.

## Required inputs

- The repository or workspace to inspect.
- A target change set: for example, current working-tree changes, a supplied diff, a commit, a pull request, or a user-specified revision range.
- The intended audience or format, if the user has a preference.

When the user says “current changes” without further scope, summarize the available staged, unstaged, and untracked changes, and state which categories were actually accessible. For a commit, pull request, or revision range, use the user's specified target; do not guess a comparison base. If the target cannot be determined, ask a focused question or summarize only the supplied evidence with an explicit scope limitation.

## Evidence to inspect

Inspect evidence relevant to the target, such as:

- Applicable repository instructions and the user's requested audience, format, or constraints.
- Git status and the target diff or revision information, using available read-only Git inspection or supplied output.
- Changed files as needed to understand the actual behavior or purpose of their changes; do not infer purpose from filenames alone.
- Relevant documentation or requirements when they clarify what the change does.

Distinguish verified changes from interpretations. Cite changed paths or symbols where practical. Label material hypotheses, unknowns, or contradictions rather than presenting them as facts. Do not reproduce secret values found in a diff; describe the affected setting or file without exposing the value.

## Workflow

1. Confirm the requested target, audience, and format. Establish whether the scope is current working-tree changes, supplied changes, or a specified commit, pull request, or revision range.
2. Inspect available status and diff evidence. Avoid double-counting staged and unstaged changes; identify whether untracked files were included or whether only their names were visible.
3. Read changed-file content only as needed to characterize the changes. Separate source, tests, documentation, configuration, generated files, and other meaningful categories when useful.
4. Summarize the change in plain language, grounded in the diff and files. Describe observable changes; do not invent motivations, outcomes, or unverified behavior.
5. Note important scope limits, inaccessible files, and material uncertainty. If evidence is insufficient for a reliable summary, ask for the missing diff or clarify the target.
6. Return the summary in the requested format, or use the default output format below. Do not make changes to repository files or Git state.

## Allowed actions

Read and search repository files and supplied diff output; compare change evidence; and inspect Git status, diffs, or revision metadata with available read-only Git operations. Summarize and report only. If Git inspection is unavailable, request the diff or state the limitation rather than guessing.

## Forbidden actions

Do not edit, create, or delete repository files; stage, commit, amend, push, pull, merge, rebase, reset, or otherwise alter Git state. Do not install dependencies, run builds or tests, or perform other side effects. Do not claim to have inspected changes or run checks that were not available and actually performed. Never expose secret values or discard working-tree changes.

## Output format

Provide a concise report with:

- **Summary:** one or two sentences describing the overall change, when supported.
- **Changes:** a short list grouped by behavior or area, with relevant file paths where helpful.
- **Scope and limitations:** the target inspected, categories included or unavailable, and material unknowns.

Adapt the format to a requested audience, such as a pull request description, but preserve evidence boundaries. Avoid a per-file inventory when grouping communicates the changes more clearly. If the diff is empty or unavailable, say so; do not fabricate a summary. Do not include code-review findings or claim that the change is tested or correct.

## Completion checklist

- The target and scope are explicit, including whether staged, unstaged, and untracked changes were available.
- The summary describes observed changes and does not invent intent, correctness, or validation results.
- Material uncertainties, omissions, and inaccessible evidence are disclosed.
- Secret values are not repeated, and Git state and repository files remain unchanged.

## Example invocations

- “Summarize my current changes for a pull request description. Include staged, unstaged, and untracked changes where accessible; do not stage or commit anything.”
- “Write a concise handoff summary of this diff, grouped by behavior. Mention any parts you could not inspect.”
- “Summarize commit [revision] relative to [base]. Keep it factual and do not review the code for defects.”

## Failure and uncertainty handling

If Git status, the requested diff, or changed-file content is unavailable, state what could not be inspected and narrow the summary to accessible evidence. If the comparison base or target is ambiguous, ask a focused question rather than choosing one silently. If a change's purpose cannot be verified from the diff, describe the observed modification without guessing its motivation. For conflicting evidence, cite both sources. Decline requests to alter Git state or perform code review and route them to an appropriate authorized workflow.
