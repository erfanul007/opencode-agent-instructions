---
name: spec-breakdown
description: Turn a non-trivial .NET repo request into a compact, implementation-ready spec with clear scope, validation, and confidence.
metadata:
  risk: medium
  scope: repo-local
---

## Template note

This skill is reusable across existing `.NET` repos. Commands, paths, and architecture examples must be discovered from the target repo instead of assumed from this template.

## What I do

- Convert a non-trivial request into an execution-ready spec packet.
- Keep the result compact, reviewable, and aligned with the smallest sufficient change.
- Prepare the work for efficient implementation, challenge, and validation.

## When to use me

- The work spans multiple files, modules, layers, or concerns.
- The work touches schema, contracts, auth, runtime behavior, deployment, or eventing.
- The implementation path needs clear ordering, validation planning, or collaboration checkpoints.

## When not to use me

- The task is a small local fix with obvious scope and obvious validation.
- The plan is already bounded and no meaningful spec refinement is needed.

## Process

1. Restate the goal and explicit out-of-scope items.
2. Identify affected files, modules, layers, contracts, and adjacent surfaces that must be checked.
3. Discover the existing repo patterns that should be preserved.
4. Choose the smallest sufficient design. Mention alternatives only when they are real options.
5. Produce an ordered task list with validation points and collaboration checkpoints.
6. Capture risks, assumptions, unresolved questions, and runtime, schema, contract, or eventing impact.
7. Score confidence from `1` to `5` for scope, design, adjacent impact, validation, runtime risk, and rollback, then state whether the work is safe to implement now or should be challenged first.

## Output

Return a compact spec packet with:

- goal
- in scope
- out of scope
- affected areas
- repo patterns or constraints to preserve
- proposed change
- alternatives considered, only when real
- why the proposal is the smallest sufficient change
- ordered task list
- validation plan
- risks and assumptions
- questions to resolve with the user or maintainer before coding
- runtime, schema, contract, or eventing impact
- confidence by dimension: scope, design, adjacent impact, validation, runtime risk, rollback
- decision checkpoint: `safe to implement now` or `needs challenge or clarification first`

Keep the spec inline by default. Recommend persisting it only when the work is long-lived, highly cross-cutting, or needs asynchronous review.
Do not write code while using this skill.
