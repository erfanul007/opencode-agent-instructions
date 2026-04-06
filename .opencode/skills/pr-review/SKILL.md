---
name: pr-review
description: Perform a findings-first review focused on regressions, risk, missing validation, and architectural drift in the target .NET repo.
metadata:
  risk: medium
  scope: repo-local
---

## Template note

This skill is reusable across existing `.NET` repos. Review against the target repo's actual architecture, conventions, contracts, and risk profile instead of assuming one fixed stack layout.

## What I do

- Review a concrete change or PR using the repo's actual architecture and risk profile.
- Prioritize bugs, regressions, risky drift, and missing verification.

## When to use me

- The user asks for a review.
- A PR or change set needs a repo-specific findings-first review.

## When not to use me

- The task is still in planning and no concrete change exists yet.
- The user wants implementation instead of review.

## Review focus

- Check whether the change preserves the repo's established architectural patterns unless an intentional change was requested.
- Flag risky changes in schema, contracts, auth, runtime config, deployment config, eventing, and secrets.
- Check whether validation is adequate for the change type, including restore, build, tests, targeted verification, and runtime or config inspection when relevant.
- Check whether the diff introduces unnecessary scope, inconsistent patterns, or unclear rollback implications.

## Output

Return:

- findings first, ordered by severity, with explicit severity labels
- file and line references when available
- missing validation or verification gaps
- open questions or assumptions
- review coverage confidence
- areas not reviewed or not fully verified
- brief change summary only after findings

If no findings are present, say so explicitly and mention residual risks or testing gaps.
Do not modify code while using this skill.
