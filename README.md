# OpenCode Agent Instructions Demo

This repository is a small demonstration of how to structure repo-local OpenCode guidance for an existing `.NET` backend.

It is intended for learning, onboarding, and presentation use.

It is a documentation and template repo, not a runnable backend application.

## What This Repo Contains

- `AGENTS.md`: the main repo policy for agent behavior
- `opencode.json`: a minimal OpenCode configuration where the default `plan` agent has direct file edits disabled
- `.opencode/skills/`: reusable task-focused skills for planning, challenge, risk checks, review, and final validation

## Included Skills

- `spec-breakdown`: turn larger requests into a compact execution spec
- `spec-challenge`: pressure-test and debate a proposed approach before implementation
- `risk-assessment`: gate changes that affect sensitive runtime or architecture surfaces
- `pr-review`: review a change with findings first
- `validate-finish`: confirm required checks and produce a completion summary

## Workflow Model

The template is optimized for a spec-driven, pair-programming style workflow:

1. Inspect the existing repo before choosing an approach.
2. Write a compact spec for non-trivial work.
3. Challenge the plan before risky implementation.
4. Apply an explicit risk and confidence gate for sensitive changes.
5. Implement the smallest sufficient change.
6. Validate with repo-local commands and summarize the result clearly.

This keeps efficiency, quality, and consistency high without forcing one fixed `.NET` architecture.

## Default Agent Behavior

`opencode.json` sets the default `plan` agent with direct file edits disabled.

- This is intentional so planning and challenge happen before code edits.
- The workflow guidance lives primarily in `AGENTS.md` and `.opencode/skills/`, not in extra config modes.
- If a real repo needs stricter non-mutating or specialized agents, add them only when there is a concrete need.

## Why This Exists

The files in this repo show one practical way to organize agent instructions for a modular `.NET` codebase that uses patterns such as minimal APIs, handlers, layered data access, and runtime-sensitive infrastructure.

All content is intentionally generic. Project-specific names, paths, and business context have been removed so the material can be used as a neutral reference.

The commands and paths shown in the policy and skills are examples. Replace placeholders and map them to the target repo's real solution, projects, config files, and deployment surfaces.

## Folder Layout

```text
.
|-- AGENTS.md
|-- opencode.json
`-- .opencode/
    `-- skills/
        |-- pr-review/SKILL.md
        |-- risk-assessment/SKILL.md
        |-- spec-breakdown/SKILL.md
        |-- spec-challenge/SKILL.md
        `-- validate-finish/SKILL.md
```

## Adapting This To A Real Repo

1. Merge these files with any existing `AGENTS.md`, `opencode.json`, `.opencode/skills/`, and repo standards docs instead of overwriting blindly.
2. Replace placeholders like `<solution-or-project>` with the real solution, project, or repo-local validation entrypoint.
3. Decide which existing docs should stay authoritative and either reference them from `opencode.json` via `instructions` or fold the needed rules into `AGENTS.md`.
4. Treat example config references such as `appsettings*.json`, launch settings, deployment manifests, or compose files as illustrative conventions, not required structure.
5. Align the policy with the target repo's real architecture and validation commands.
6. Add or remove skills based on the team workflow and tech stack.
