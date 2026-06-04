---
title: Codex Agent Instructions Strategy
type: agent-instructions
status: approved
phase: technical-setup
owner: shared
created: 2026-05-27
updated: 2026-05-27
source_lore: []
related:
  [
    docs/architecture/control-manifest,
    docs/architecture/unity-technical-scheme,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    docs/architecture/multi-agent-operating-model,
    docs/architecture/unity-repo-agents-template,
  ]
approval: approved
---

# Codex Agent Instructions Strategy

## Decision

Neon Champions will use explicit repository-local agent instruction files for Codex and compatible coding agents.

The design repo has its own root `AGENTS.md`. The future Unity implementation repo must have a root `AGENTS.md` and may have scoped nested `AGENTS.md` files for high-risk areas such as domain logic, presentation, data, infrastructure, tests, and editor tooling.

These instruction files summarize approved rules. They do not replace GDDs, ADRs, READY stories, spikes, tests, CI, or human approval.

## Research Basis

Current Codex guidance treats `AGENTS.md` as a repository instruction file for agents. It is an open-format “README for agents” containing repo layout, build/test commands, conventions, constraints, and definition of done.

Key Codex conventions found during research:

- Codex reads global and project instruction files before work.
- Project `AGENTS.md` files can exist at repository root or in nested directories.
- A nested `AGENTS.md` applies to the directory tree below it.
- More deeply nested instruction files override broader ones for files in their scope.
- `AGENTS.override.md` overrides `AGENTS.md` in the same directory.
- Codex has a project-doc size budget, so instruction files should be concise and operational.
- Prompts should state goal, context, constraints, and done criteria.
- Complex or risky work should begin with plan/research before edits.
- Multiple agents should not modify the same working tree or same high-conflict files.

Relevant sources:

- OpenAI Codex AGENTS.md guide: `https://developers.openai.com/codex/guides/agents-md`
- OpenAI Codex best practices: `https://developers.openai.com/codex/learn/best-practices`
- OpenAI Codex sandbox: `https://developers.openai.com/codex/sandbox`
- OpenAI Codex non-interactive mode: `https://developers.openai.com/codex/noninteractive`
- OpenAI Codex worktrees: `https://developers.openai.com/codex/app/worktrees`
- Codex repository AGENTS example: `https://github.com/openai/codex/blob/main/AGENTS.md`
- Git worktree docs: `https://git-scm.com/docs/git-worktree`
- GitHub Copilot coding-agent best practices: `https://docs.github.com/en/copilot/how-tos/agents/copilot-coding-agent/best-practices-for-using-copilot-to-work-on-tasks`
- Anthropic Claude Code best practices: `https://www.anthropic.com/engineering/claude-code-best-practices`

## Design Repo Instruction Policy

The design repo root `AGENTS.md` exists to prevent agents from confusing design/control work with Unity implementation work.

It must state:

- this repo is the production-facing design/control repo;
- Unity runtime implementation belongs in the future Unity repo;
- agents may draft docs and handoffs but may not approve their own work;
- agents may not invent game rules, lore, balance, UX, architecture, assets, content, or production scope;
- durable artifacts require `index.md` and `log.md` updates;
- conflicting docs are stop conditions.

## Future Unity Repo Instruction Policy

The future Unity repo must include a root `AGENTS.md` as part of `SPIKE-001` or immediately after project creation.

The root Unity `AGENTS.md` must include:

- project identity and Unity defaults;
- mandatory source reading order;
- implementation authority rules;
- folder and assembly boundaries;
- domain/application/presentation/infrastructure/data responsibilities;
- testing/TDD/validator/PlayMode/CI requirements;
- Git/PR/evidence/omissions requirements;
- explicit stop conditions.

Nested `AGENTS.md` files should be added when a subsystem has rules that differ from the root. Recommended initial scoped files:

- `Assets/NeonChampions/Runtime/Domain/AGENTS.md`
- `Assets/NeonChampions/Runtime/Application/AGENTS.md`
- `Assets/NeonChampions/Runtime/Presentation/AGENTS.md`
- `Assets/NeonChampions/Runtime/Infrastructure/AGENTS.md`
- `Assets/NeonChampions/Runtime/Data/AGENTS.md`
- `Assets/NeonChampions/Tests/AGENTS.md`
- `Assets/NeonChampions/Editor/AGENTS.md`
- `production/evidence/AGENTS.md` or equivalent evidence folder instruction file

## Prompt Standard for Codex Tasks

Every implementation prompt should include:

1. Goal.
2. Approved source references.
3. In scope.
4. Out of scope.
5. Files or areas expected to change.
6. Files or areas forbidden to change.
7. Required tests/validators/CI.
8. Required evidence.
9. Stop conditions.
10. Final response format.

For production stories, Codex must be told to follow TDD for production logic and bug fixes.

For risky Unity work, Codex should first produce a plan listing expected files/scenes/prefabs/assets to touch. Implementation begins only after the plan is accepted, unless the story/spike explicitly authorizes immediate scaffold work.

## Sandbox and Permission Policy

Default Codex posture:

- Use workspace-write rather than full-system access.
- Require approval for network access, package installs, destructive commands, or writes outside the repo.
- Do not expose production secrets.
- Do not use `--yolo` / dangerous full-access modes except in an isolated, disposable environment with explicit human approval.

Agents may not disable CI, weaken tests, or rewrite broad project settings to make a task pass.

## Parallel Agent Policy

Parallel agents are allowed only when isolation and ownership are clear.

Rules:

- One agent = one task = one branch/worktree.
- Do not run multiple agents in the same working tree.
- Do not run parallel agents on the same scene, prefab, ScriptableObject database, animation controller, or other high-conflict Unity asset.
- Use branches/worktrees named for the story/spike.
- Use file/asset reservations for high-conflict assets.
- Reviewer agents must use fresh context and review against approved docs, not against the implementer's explanation alone.

## Approval Scope

This document approves the strategy and required instruction artifacts. It does not approve concrete Unity repo file contents as final implementation; use `docs/architecture/unity-repo-agents-template.md` as the starting template during `SPIKE-001`.

Current verdict: APPROVED.
