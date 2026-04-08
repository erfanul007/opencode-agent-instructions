---
name: repo-context-discovery
description: Gather the minimum repository context needed before planning, reviewing, or editing. Prefer indexed, structural, or symbol-aware discovery before targeted file reads. Reuse and persist only durable findings that will improve future task execution or context efficiency.
metadata:
  phase: discovery
  scope: repo-local
  applies_to: any-repo
---

# Repo Context Discovery

## Purpose

Gather only the minimum repository context needed to support safe planning, review, or implementation.

Use this skill to reduce unnecessary scanning, improve context quality, and avoid loading broad or redundant repository content.

## Use when

Use this skill when any of the following apply:

- the task is non-trivial, cross-boundary, or sensitive
- repository structure or ownership is not yet clear
- affected files, modules, or entrypoints are uncertain
- review requires adjacent impact analysis
- validation paths are unclear
- the repository is large enough that broad reading would waste context

## Do not use when

Do not use this skill when:

- the task is small and the affected file or surface is already clear
- sufficient context has already been collected for the current task
- only a quick targeted read is needed

## Working rules

- Prefer indexed, structural, symbol-aware, or memory-backed discovery when available.
- Narrow to targeted file or symbol reads only after discovery identifies the likely surfaces.
- Avoid broad scans, repeated reads, and loading files that are unlikely to affect the task.
- Reuse already collected context before gathering more.

## What to discover

Discover only what is needed for the current task, such as:

- likely affected modules, components, or boundaries
- relevant entrypoints, interfaces, contracts, or configs
- adjacent dependencies or callers/callees
- validation entrypoints such as tests, build targets, or app/package boundaries
- repository patterns or local conventions that should be preserved

## Persistence rules

Persist or record findings only if they are durable, reusable, and likely to improve future work, such as:

- stable module boundaries
- important dependency relationships
- repository conventions
- validation entrypoints
- durable architecture notes

Keep task-local findings in the current execution context or spec unless they are clearly durable.

Do not persist temporary, task-local, speculative, or fast-changing details.

## Output

Produce a short context packet containing only:

- relevant surfaces
- likely affected boundaries or dependencies
- important local patterns to preserve
- validation entrypoints to consider
- open uncertainties that still require clarification

## Stop condition

Stop discovery once the agent can do one of the following with reasonable confidence:

- create an execution spec
- perform a focused review
- make a bounded change
- state a specific clarification need

Do not continue exploring once the next safe step is clear.

## Efficiency notes

- Discovery should reduce context load, not increase it.
- Prefer narrowing over collecting.
- Prefer durable findings over verbose summaries.
- Prefer one good context packet over many scattered notes.
