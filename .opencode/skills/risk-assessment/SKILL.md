---
name: risk-assessment
description: Assess whether a concrete change touches sensitive .NET repo surfaces and determine the validation, approval, and escalation needed before implementation.
metadata:
  risk: high
  scope: repo-local
---

## Template note

This skill is reusable across existing `.NET` repos. Sensitive surfaces and validation must be mapped to the target repo's actual runtime, deployment, and contract boundaries.

## What I do

- Evaluate concrete change risk for schema, contracts, auth, runtime, deployment, eventing, or cross-boundary work.
- Decide whether the change can proceed normally, needs clarification, or must be escalated.
- Act as a narrow sensitive-change gate, not a general planning or review workflow.

## When to use me

- A concrete proposed change or spec touches sensitive surfaces.
- The work affects schema or data migrations.
- The work affects public contracts, APIs, auth, permissions, secrets, background processing, messaging, or deployment behavior.
- The work affects startup behavior, runtime configuration, or new cross-project dependencies.

## When not to use me

- The task is a normal local code change with no sensitive surfaces.
- You still need an initial spec. Use `spec-breakdown` first.
- The main need is to compare implementation approaches or debate a general plan. Use `spec-challenge` for that.

## Process

1. Identify the sensitive surfaces the change can affect.
2. Check adjacent modules, contracts, policies, runtime behavior, and rollback implications.
3. Determine the minimum safe validation path.
4. Score the risk and the confidence in safe execution.
5. Identify whether user or maintainer confirmation is needed.
6. Decide whether to proceed, clarify, or escalate.

## Sensitive surfaces checklist

When relevant, explicitly assess:

- schema changes and data migrations
- public contracts, API behavior, and compatibility impact
- auth, permissions, secrets, and security-sensitive logic
- background jobs, messaging, integrations, and eventing
- runtime, environment, configuration, or deployment changes
- new project, package, or module dependencies
- startup behavior and service readiness impact
- repo-local equivalents of `appsettings*.json`, launch settings, environment config, deployment manifests, and container or compose files

## Scoring

Return a compact risk matrix with `1` to `5` scores for:

- likelihood of failure
- impact if failure occurs
- detectability before release
- rollback ease
- confidence in the validation path

Also return confidence-by-dimension scores required by repo policy:

- scope confidence
- design confidence
- adjacent impact confidence
- validation confidence
- runtime risk confidence
- rollback confidence

Use the confidence gate from repo policy. Do not recommend autonomous implementation when critical confidence is too low or approval boundaries are unclear.

## Output

Return:

- risk summary
- sensitive surfaces affected
- adjacent impact checked
- risk matrix: likelihood, impact, detectability, rollback ease, validation confidence
- confidence by dimension: scope, design, adjacent impact, validation, runtime risk, rollback
- required validation
- user or maintainer confirmation needed
- exact gating reason for `clarify` or `escalate`
- rollback considerations
- final status: `proceed`, `clarify`, or `escalate`

Keep this narrow. Do not expand into general planning or PR review.
Use this only after there is a concrete proposed change to assess.
Do not write code while using this skill.
