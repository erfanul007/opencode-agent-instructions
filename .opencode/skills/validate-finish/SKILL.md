---
name: validate-finish
description: Run or confirm the required final validation steps for a change and produce a deterministic completion summary.
metadata:
  risk: medium
  scope: repo-local
---

## Template note

This skill is reusable across existing `.NET` repos. Discover the target repo's actual solution, project, script, test, and runtime validation commands before applying this template.

## What I do

- Determine the required completion checks from repo policy and actual change type.
- Produce a consistent completion summary tied to the executed task list.

## When to use me

- A non-trivial change is ready for final verification.
- The task touched multiple files, modules, layers, or any sensitive surface.
- The user asks whether the work is actually complete.

## When not to use me

- The task is still being planned.
- Required implementation or verification work is still in progress.

## Process

1. Determine which checks are required for the actual change type.
2. Discover the smallest repo-local command set that still validates the change with confidence.
3. Run or confirm required checks in the correct order.
4. Record skipped checks only when justified by missing capability or infeasible verification.
5. Compare expected validation with actual validation performed.
6. Reconcile the completed work against the task list.

## Example baseline checks

For code changes, discover and use the repo-local equivalents of:

```bash
dotnet restore <solution-or-project>
dotnet build <solution-or-project>
```

Also run targeted tests for the affected surface when they exist.
When config or runtime-sensitive surfaces changed, inspect repo-local config and deployment files such as `appsettings*.json`, launch settings, deployment manifests, and container or compose files when present.

## Output

Return a completion summary with:

- files, modules, or surfaces touched
- commands run
- expected checks
- actual checks run
- evidence of success or failure
- skipped checks and reasons
- residual risks
- rollback or follow-up notes
- task reconciliation result
- delivery confidence
- completion gate result: `pass` or `fail`

If a required check fails or a sensitive change cannot be safely verified, stop and escalate instead of declaring completion.
Do not modify code while using this skill.
