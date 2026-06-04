---
title: Architecture
type: adr
status: draft
phase: technical-setup
owner: shared
created: 2026-05-22
updated: 2026-05-27
source_lore: []
related:
  [
    docs/architecture/control-manifest,
    docs/architecture/unity-technical-scheme,
    docs/architecture/technical-decision-priorities,
    docs/architecture/data-authoring-options,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    docs/architecture/codex-agent-instructions,
    docs/architecture/multi-agent-operating-model,
    docs/architecture/unity-repo-agents-template,
  ]
approval: pending
---

# Architecture

Draft pending. This file will be authored after concept and MVP system GDDs are approved.

The current approved technical direction is captured in:

- `docs/architecture/control-manifest.md`
- `docs/architecture/unity-technical-scheme.md`
- `docs/architecture/technical-decision-priorities.md`
- `docs/architecture/data-authoring-options.md`
- `docs/architecture/testing-strategy.md`
- `docs/architecture/ci-build-automation.md`
- `docs/architecture/codex-agent-instructions.md`
- `docs/architecture/multi-agent-operating-model.md`
- `docs/architecture/unity-repo-agents-template.md`

Currently approved defaults:

- Unity 6.4, target version `6000.4.8f1` if available.
- 2.5D presentation model.
- URP render pipeline.
- Unity Input System.
- Folder/assembly default from the Unity Technical Scheme.
- Data-authoring direction: Option D / Phased Hybrid.
- Runtime state must be serializable from the start.
- All player-facing strings must be localizable from the start.
- Testing strategy: strict layered testing with TDD for production logic, automated validators for data/content/localization, and automated PlayMode coverage as the target for Unity integration.
- CI/build automation: GitHub Actions by default; CI required immediately after Unity project creation, including spike PRs; production PRs require merge-blocking checks unless a human-approved exception is documented.
- Agent instructions: use repo-local `AGENTS.md` files; future Unity repo must create root/scoped AGENTS.md during SPIKE-001 from `docs/architecture/unity-repo-agents-template.md`.
- Multi-agent model: many agents are allowed only with clear roles, gates, branch/worktree isolation, file/asset ownership, evidence, and human final approval.

## Decisions needed

- Concrete data schemas and tooling for the approved phased-hybrid data direction.
- Save/load format and versioning.
- Localization implementation package/layer.
- Final project/repo layout after Unity project creation.
- Final assembly definitions after Unity project creation.
- Exact Unity CI commands, Unity license/activation, runner image, caching, and artifact retention policy.
