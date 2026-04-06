---
name: spec-challenge
description: Debate a proposed implementation plan, pressure-test assumptions, and decide whether the work is bounded enough to implement safely.
metadata:
  risk: medium
  scope: repo-local
---

## Template note

This skill is reusable across existing `.NET` repos. It should challenge the target repo's actual architecture and constraints, not the examples in this template.

## What I do

- Challenge the first plausible plan before implementation starts.
- Improve quality by debating the proposed design, assumptions, adjacent impact, validation path, and rollback story.
- Act as the pair-programming debate step before risky work.

## When to use me

- A non-trivial spec already exists.
- More than one plausible implementation approach exists.
- The work is sensitive, cross-boundary, non-obvious, or expensive to undo.
- Confidence is not yet strong enough to implement without pressure-testing the plan.

## When not to use me

- The task is trivial or already bounded with no material ambiguity.
- There is no concrete spec or proposed approach to challenge yet.
- The main need is sensitive-surface gating for an already-bounded change. Use `risk-assessment` for that.

## Process

1. Restate the proposed approach and intended scope.
2. Surface hidden assumptions and unresolved unknowns.
3. Identify the strongest argument for the current plan.
4. Identify the strongest argument against the current plan.
5. Identify a safer alternative when one exists.
6. Check adjacent modules, contracts, policies, runtime-sensitive surfaces, irreversible mistakes, and rollback implications.
7. Score confidence and decide whether to proceed, proceed with constraints, clarify first, or escalate.

## Confidence gate

Score each dimension from `1` to `5`:

- scope
- design
- adjacent impact
- validation
- runtime risk
- rollback

Do not recommend implementation if any critical dimension is `1`, or if sensitive work has scope, validation, runtime risk, or rollback confidence at `2` or lower.

## Output

Return:

- recommended approach
- strongest argument for the current plan
- strongest argument against the current plan
- safer alternative, when one exists
- why the chosen path still wins, or why it should stop
- assumptions found
- unresolved questions
- adjacent surfaces checked
- irreversible or high-cost failure modes
- validation plan
- rollback considerations
- confidence by dimension: scope, design, adjacent impact, validation, runtime risk, rollback
- final recommendation: `proceed`, `proceed with constraints`, `clarify first`, or `escalate`

Do not write code. Stop once the plan is bounded enough to implement safely or clearly requires a user or maintainer decision.
