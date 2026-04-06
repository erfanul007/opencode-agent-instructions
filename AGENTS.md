# Generic .NET Repo Agent Policy Template

Intent: Policy

This repository is a documentation and template repo for OpenCode guidance in an existing `.NET` codebase. The commands, paths, and examples in this file are illustrative. After copying this template into a real repo, replace placeholders and align the policy with the actual architecture, validation commands, and deployment surfaces.

## Instruction Precedence

When guidance overlaps or appears to conflict, resolve it in this order:

1. Direct user instructions
2. `AGENTS.md`
3. Repo-local policy or practice docs referenced by config or this policy
4. `.opencode/skills/*/SKILL.md`

Skills extend this policy for specific workflows. They must not relax or override higher-priority guidance.

If the target repo already has engineering standards, architecture docs, or contribution guidance, either reference those files from `opencode.json` via `instructions` or fold the authoritative rules into `AGENTS.md`. Avoid parallel instruction sources that overlap without a clear precedence path.

## Core Priorities

- When tradeoffs are otherwise equal, prioritize efficiency, then quality, then consistency.
- Prefer the smallest sufficient change.
- Preserve the repo's established architecture and conventions unless the task explicitly requires changing them.
- Inspect the affected area plus adjacent contracts, policies, rollback surfaces, and runtime implications before choosing an approach.
- Do not broaden scope into cleanup or refactoring without a concrete need.
- Do not introduce or keep plaintext secrets in source-controlled config or key material.

## Pair Programming Model

Treat the user as your implementation partner, not just a ticket source.

- Restate the task intent before non-trivial work when it helps bound scope.
- Recommend the smallest viable approach before risky or cross-cutting changes.
- Surface objections, tradeoffs, and uncertainty before making high-cost moves.
- Use explicit status language when needed: `suggest`, `recommend`, `need clarification`, `blocked`.
- Pause for clarification when ambiguity materially affects behavior, architecture, schema, contracts, security, or runtime outcomes.
- For non-trivial work, maintain a live task list and reconcile the final result against it.

## Architecture Baseline

Do not assume one fixed `.NET` architecture across all repos. First discover what the target repo actually uses.

Possible patterns may include:

- minimal APIs or controllers
- MediatR or direct application services
- EF Core, Dapper, both, or another persistence pattern
- layered, vertical-slice, modular-monolith, or hybrid structures
- background jobs, messaging, eventing, or purely synchronous flows

Your default job is to preserve the repo's current patterns unless the user explicitly asks for architectural change.

## Workflow

For non-trivial, risky, or cross-boundary work, follow this sequence:

1. Intake: inspect the relevant code, config, contracts, and adjacent surfaces.
2. Spec: use `spec-breakdown` to produce a compact execution spec.
3. Challenge: use `spec-challenge` to debate the plan before implementation when the change is sensitive, cross-module, non-obvious, or hard to roll back.
4. Risk gate: use `risk-assessment` before implementation when the change touches sensitive surfaces.
5. Implement: make the smallest sufficient change that matches the bounded spec.
6. Validate: run the required checks based on the actual change and repo structure.
7. Summarize: report what changed, what was validated, what remains risky, and whether the task list was reconciled.

For small, local, low-risk fixes with obvious validation, you may compress the workflow, but do not skip required clarification or validation.

## Non-Trivial Work

Treat work as non-trivial when any of the following apply:

- more than 3 meaningful steps
- more than 1 file changed
- more than 1 concern touched
- schema, contracts, runtime config, auth, eventing, or deployment behavior may change
- validation requires more than a quick local check

For non-trivial work, a spec packet is required.

Default operating model for task and spec tracking:

- Keep the task list lightweight and live for the current session.
- Use an inline checklist or equivalent session-local task tracking by default.
- Persist spec or task docs only when the work is long-lived, highly cross-cutting, asynchronous, or explicitly requested.
- Reconcile the final result against the live task list before declaring completion.

Minimum spec packet content:

- goal
- in-scope and out-of-scope items
- affected files, modules, or layers
- chosen design
- alternatives considered, only when real
- smallest-sufficient-change rationale
- ordered task list
- adjacent surfaces checked
- validation plan
- risks, assumptions, unresolved questions
- runtime, schema, contract, or eventing impact
- confidence by dimension

## Debate And Challenge Rule

Use `spec-challenge` before implementation when any of the following are true:

- more than one plausible design exists
- rollback is unclear or expensive
- the work changes architecture or boundaries
- the work affects runtime, deployment, schema, contracts, auth, eventing, or background processing
- the first plan might be correct but has not been pressure-tested yet

The challenge step should include the strongest argument for the current plan, the strongest argument against it, at least one safer alternative when one exists, and a clear recommendation.

## Sensitive Surfaces

Sensitive changes commonly include:

- schema or data migrations
- public contracts or API behavior
- auth, permissions, secrets, or security-sensitive code
- background jobs, integration flows, messaging, or eventing
- runtime, environment, deployment, infrastructure, or app configuration
- new cross-project or cross-module dependencies
- startup behavior that can affect boot, migration, or service readiness

Use `risk-assessment` after a concrete spec exists and before implementing these changes.

## Confidence Score Gate

For `spec-challenge` and `risk-assessment`, score each dimension from `1` to `5`:

- scope confidence
- design confidence
- adjacent impact confidence
- validation confidence
- runtime risk confidence
- rollback confidence

All six dimensions are treated as critical for the confidence gate.

Scoring guide:

- `1`: largely unknown or unbounded
- `2`: weak confidence with material uncertainty
- `3`: adequate confidence to proceed carefully
- `4`: strong confidence supported by repo evidence
- `5`: very strong confidence with clear evidence and low ambiguity

Gate rules:

- Do not implement if any critical dimension is `1`.
- Do not implement sensitive work if scope, validation, runtime risk, or rollback confidence is `2` or lower.
- Clarify or escalate instead of coding when the confidence gate is not met.
- Make the reason explicit when proceeding with any dimension at `3`.

## Validation Policy

Discover the actual repo structure before choosing commands. Do not assume a specific solution name, project layout, validation entrypoint, or deployment layout.

When code changes are made:

- identify the active solution, affected project files, repo validation scripts if present, and relevant test projects
- run restore and build at the smallest level that still validates the change with confidence
- run targeted tests for the affected surface when they exist
- expand to broader validation when the change is cross-cutting or the targeted checks are insufficient

When runtime or config-sensitive surfaces are touched, inspect the repo-local equivalents of items such as:

- `appsettings*.json`
- environment-specific config files
- launch settings
- deployment manifests
- container or compose files, if present
- background job, messaging, or infrastructure wiring

Prefer targeted validation over broad validation when the scope is bounded and confidence remains high. Use broader validation when the change crosses boundaries or the risk profile requires it.

## Delivery And Completion

For non-trivial work, finish with a completion summary that includes:

- files, modules, or surfaces touched
- commands run
- expected checks versus actual checks run
- skipped checks and reasons
- residual risks
- rollback or follow-up notes
- task-list reconciliation result
- final delivery confidence

Use `validate-finish` when the work is ready for final verification.

Do not declare work complete if a required restore, build, or test check fails, or if a sensitive change cannot be verified safely.

## Review Style

Use `pr-review` for findings-first review work.

- prioritize bugs, regressions, risky drift, and missing validation
- include severity labels
- include file and line references when available
- mention review coverage limits and remaining blind spots
- keep change summaries secondary to findings

## Efficiency Rules

- Reuse context gathered earlier in the same task instead of re-exploring unchanged areas.
- Prefer targeted reads, searches, and validation over broad scans when the scope is already bounded.
- Keep specs compact and execution-focused.
- Avoid duplicate reasoning when the repo evidence already establishes the answer.

## Forbidden Actions

- Do not add plugins, MCP servers, custom agents, custom commands, or broad permission maps by default.
- Do not silently change architecture, contracts, or deployment behavior.
- Do not waive failed required checks.
- Do not revert unrelated worktree changes without explicit approval.
