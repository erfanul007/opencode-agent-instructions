# Agent Policy Core

Intent: concise, tool-agnostic policy for spec-driven development in existing repositories.

## Instruction Precedence

Resolve overlaps in this order:

1. Direct user instructions
2. Repository policy
3. Repository engineering standards and architecture docs
4. Task-specific process instructions, skills, or commands
5. Runtime capability settings

If runtime behavior appears to conflict with repository policy, follow policy intent unless the user explicitly overrides it.

## Core Rules

- Prefer the smallest sufficient change, keep scope tight, and avoid opportunistic cleanup or unrelated refactors.
- Preserve existing architecture and repository patterns unless change is explicitly requested.
- Reuse collected context; avoid re-exploring unchanged areas.
- Prefer targeted reads and symbol-aware navigation over broad scanning.
- Never introduce plaintext secrets into source-controlled files.

## Clarify First When Needed

Clarify before proceeding if ambiguity could materially change:

- architecture or boundaries
- schema or data behavior
- API or contract behavior
- auth, security, or secret handling
- runtime, deployment, or environment behavior
- external integrations
- rollback expectations

## Spec-First Trigger

Create a compact execution spec before editing when work is non-trivial, risky, cross-boundary, sensitive, or likely to require more than quick validation.

Treat work as non-trivial if any apply:

- more than 3 meaningful steps
- more than 1 file is likely to change and scope or validation is not obvious
- more than 1 concern is touched
- a sensitive change may occur
- validation is more than a quick local check

For small, low-risk work, compress the workflow.

## Compact Spec

When a spec is needed, keep it short and execution-focused.

Include only:

- goal
- scope and out-of-scope
- affected files or surfaces
- proposed approach and why it is the smallest sufficient change
- ordered task list
- validation plan
- key risks, assumptions, and open questions

## Risk Gate

Pressure-test the approach before implementation when multiple plausible designs exist, rollback is unclear, boundaries may shift, or schema, contracts, auth, runtime, deployment, or integrations may change.

If confidence is too low to proceed safely on sensitive work, stop and clarify rather than forcing implementation.

## Workflow Routing

Use the lightest workflow that preserves safety and clarity:

- use focused discovery only when affected boundaries, entrypoints, or validation paths are not yet clear
- use an execution spec when the spec-first trigger applies
- use a risk gate only after a concrete approach exists and material uncertainty remains about adjacent impact, validation, rollback, or sensitivity
- validate before declaring implementation complete
- use findings-first review when the task is review rather than implementation

## Execution

- Make bounded changes only.
- Do not silently change architecture, contracts, or deployment behavior.
- Do not revert unrelated worktree changes without explicit approval.

## Capability Usage

Use capabilities only when they improve quality, reduce risk, or keep context focused.

- Prefer focused exploration and targeted retrieval over broad context loading.
- Keep discovery handoffs compact, factual, and limited to what the next safe step needs.
- Use skills or task-specific process instructions for repeatable workflows and non-trivial work.
- Use focused helper agents or equivalent runtime capabilities for isolated exploration, plan drafting, or other non-trivial subtasks.
- Pull external references only when repository context is insufficient.
- Avoid loading heavy process or external context unless the task needs it.

## Validation

Discover actual repository structure before choosing commands. Do not assume a specific stack or repository layout.

When code changes are made:

- identify the relevant solution, project, package, app, or test entrypoints
- run the smallest validation that still gives reasonable confidence
- run targeted tests for affected surfaces when available
- broaden validation only when risk or blast radius justifies it

For runtime- or config-sensitive work, inspect relevant local config and wiring before concluding.

## Completion

Do not claim completion if required checks failed, important validation was skipped without saying so, sensitive changes remain unverified, or major uncertainty remains unresolved.

For non-trivial work, briefly summarize:

- touched files or surfaces
- checks run
- checks not run and why
- residual risks or follow-ups
- whether the delivered change stayed within requested scope

## Review Mode

When reviewing, use findings-first:

- prioritize bugs, regressions, risky drift, and missing validation
- keep summaries secondary to findings
- mention evidence and coverage limits when relevant

## Efficiency Rule

Keep this instruction layer thin.
Move curated process detail, scoring frameworks, stack-specific validation, migration rules, and deep review checklists into task-specific process instructions or skills.
