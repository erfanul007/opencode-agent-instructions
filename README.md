# Agent Instructions Template Demo

This repository is a reusable instruction template for spec-driven agentic development in existing repositories.

It is intended for learning, onboarding, and presentation use.

It is a documentation/template repo, not a runnable product application.

## What This Repo Contains

- a concise, tool-agnostic policy core in `AGENTS.md`
- a Claude-compatible policy mirror in `CLAUDE.md`
- focused process skills for discovery, planning, risk gating, validation, review, and docs retrieval
- mirrored skill copies for Claude and Codex in `.claude/skills/*/SKILL.md` and `.codex/skills/*/SKILL.md`
- runtime adapter examples (`opencode.json`, `.mcp.json`, `.codex/config.toml`, `.claude/settings.local.json`, `.serena/project.yml`)
- an example slash-command style review prompt for `.NET` diffs in `.opencode/commands/review-dotnet.md`

## Included Skills

- `repo-context-discovery`: gather only the context needed to proceed safely
- `execution-spec`: produce a compact, implementation-ready spec
- `plan-risk-gate`: pressure-test a bounded approach before editing
- `validate-complete`: run the minimum final validation and reconcile scope
- `review-findings-first`: review diffs with findings first
- `docs-retrieval`: retrieve only the external docs needed to unblock work

## Workflow Model

For non-trivial or risk-sensitive work, the expected flow is:

1. `repo-context-discovery` (only when boundaries are unclear)
2. `execution-spec`
3. `plan-risk-gate` (only when material uncertainty remains)
4. implementation
5. `validate-complete` or `review-findings-first` based on task intent

Use `AGENTS.md` as the normative source for precedence, scope control, and completion standards.

## Adapting This To A Real Repo

1. Merge this template with existing repo policy instead of overwriting it.
2. Keep one clear precedence model where user instructions are explicit.
3. Map validation and risk terms to real repo commands, test targets, and deployment/runtime surfaces.
4. Keep skills concise; remove ones without a recurring use case.
5. Keep runtime adapters consistent with the same MCP/tooling choices across environments.
