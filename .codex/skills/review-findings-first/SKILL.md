---
name: review-findings-first
description: Review a PR, diff, branch, or changed files with a findings-first approach focused on regressions, risky drift, missing validation, adjacent impact, and unintended architecture or contract changes.
metadata:
  phase: review
  scope: repo-local
  applies_to: any-repo
---

# Review Findings First

## Purpose

Review a concrete change and surface the most important findings first.

Use this skill to identify regressions, risky drift, missing validation, adjacent impact, and unintended changes to architecture, contracts, runtime behavior, or repository patterns.

## Use when

Use this skill when any of the following apply:

- the user asks for a review
- a PR, diff, branch, or changed files need assessment
- a completed or in-progress change needs a findings-first quality check
- the change may have adjacent impact that should be called out before merge or handoff

## Do not use when

Do not use this skill when:

- no concrete change, diff, or touched surface exists yet
- the main need is planning, discovery, or risk-gating before implementation
- the main need is final validation execution rather than review
- the user wants implementation instead of review

## Working rules

- Review against the actual repository architecture, conventions, contracts, and risk profile.
- Prioritize findings that materially affect correctness, safety, compatibility, maintainability, or release confidence.
- Keep summaries secondary to findings.
- Prefer concrete evidence over vague concern.
- Call out missing validation or verification gaps when they materially affect confidence.
- Do not modify code while using this skill.

## What to look for

Focus only on issues that matter for the current change, such as:

- regressions or broken behavior
- risky architectural drift or pattern inconsistency
- unintended contract, schema, or compatibility changes
- auth, permission, secret-handling, or security-sensitive mistakes
- runtime, startup, configuration, deployment, or integration risks
- missing or insufficient validation for the type of change made
- unnecessary scope expansion or unclear change boundaries
- adjacent surfaces likely affected but not accounted for

## Process

1. Identify the concrete review surface: PR, diff, branch, or changed files.
2. Understand the intended change briefly enough to review it correctly.
3. Check the change against local repository patterns, contracts, and adjacent impact.
4. Identify the highest-value findings first.
5. Check whether validation is adequate for the risk and blast radius of the change.
6. State any review limits, unverified areas, or assumptions that affect confidence.
7. Return findings-first output, or explicitly say no material findings were found.

## Output

Return a concise review result containing only:

- findings ordered by importance, with severity labels when useful
- file references or concrete evidence when available
- missing validation or verification gaps
- open questions or assumptions that affect review confidence
- review coverage limits or unverified areas
- brief overall assessment only after findings

If no material findings are present, say so explicitly and still mention any residual risks, testing gaps, or review limits.

## Severity guidance

Use severity labels only when they improve clarity. Prefer simple, practical levels such as:

- high
- medium
- low

Do not inflate severity. Focus on impact and likelihood, not wording.

## Stop condition

Stop once the review has surfaced the material findings, or once it is clear that no material findings were found within the reviewed scope.

Do not expand into full redesign suggestions, speculative refactors, or unrelated cleanup.

## Efficiency notes

- Findings should be specific, not exhaustive.
- Prefer a few strong findings over many weak comments.
- Review only the touched or plausibly affected surfaces unless the change clearly requires broader inspection.
- Keep the output short enough to scan quickly and act on immediately.
