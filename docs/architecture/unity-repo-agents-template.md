---
title: Unity Repo AGENTS.md Template
type: agent-instructions
status: approved
phase: technical-setup
owner: shared
created: 2026-05-27
updated: 2026-05-27
source_lore: []
related:
  [
    docs/architecture/codex-agent-instructions,
    docs/architecture/control-manifest,
    docs/architecture/unity-technical-scheme,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/spikes/spike-001-unity-project-ci-foundation,
  ]
approval: approved
---

# Unity Repo AGENTS.md Template

This file defines the approved starting content for the future Unity implementation repo's agent instructions. During `SPIKE-001`, create the Unity repo root `AGENTS.md` from this template and adapt only paths/commands that are discovered during project setup.

## Root `AGENTS.md`

Recommended future path:

```text
<unity-repo>/AGENTS.md
```

Recommended content:

````markdown
# AGENTS.md — Neon Champions Unity Repo

This repository contains the Unity implementation of Neon Champions.

Agents are implementers, not designers or architects. Implement only approved spikes or READY stories.

## Approved Technical Defaults

- Engine: Unity 6.4.
- Target version: `6000.4.8f1` unless unavailable and a human-approved replacement exists.
- Render pipeline: URP.
- Target first: desktop/PC prototype.
- Input: Unity Input System.
- Presentation model: 2.5D working default.
- Networking, multiplayer, live service, account systems: out of scope for MVP.

## Required Reading Order

Before editing, read in this order:

1. current approved spike or READY story;
2. linked GDD sections;
3. linked ADR / architecture / control-manifest sections;
4. this `AGENTS.md`;
5. nearest scoped `AGENTS.md` for files being touched;
6. relevant existing code, tests, scenes, prefabs, and data.

If any required source is missing, draft, unapproved, or contradictory, stop and report.

## Implementation Authority

Allowed:

- approved spike scope;
- READY story scope;
- tests/evidence required by the story/spike.

Not allowed:

- implementing from chat memory;
- implementing from epics;
- implementing from worldbuilding directly;
- inventing mechanics, balance, UX, lore, names, assets, content, architecture, save/load, data schemas, or package choices;
- changing ProjectSettings, packages, scenes, prefabs, or generated files outside approved scope.

## Architecture Boundaries

- `Domain` owns testable gameplay rules and state transitions.
- `Application` coordinates use cases and orchestration.
- `Presentation` adapts/displays state through Unity objects, UI, scenes, VFX, and audio.
- `Infrastructure` owns persistence/loading/platform glue only when approved.
- `Data` owns definitions, schemas, import helpers, and validators.

Default dependency direction:

```text
Presentation -> Application -> Domain
Infrastructure -> Application / Domain where approved
Tests -> tested assemblies
Domain -> no UnityEngine dependency unless explicitly approved
```
````

Do not add global state, event buses, service locators, dependency injection containers, save/load systems, serialization systems, asset-loading architecture, or data-authoring pipelines without approved ADR/story scope.

## Folder Layout

Use the approved scaffold:

```text
Assets/NeonChampions/
  Runtime/
    Domain/
    Application/
    Presentation/
    Infrastructure/
    Data/
  Editor/
  Tests/
    EditMode/
    PlayMode/
  Scenes/
  Prefabs/
  ScriptableObjects/
  Art/
  Audio/
  UI/
```

## Data Rules

- Approved direction: phased hybrid.
- Static definitions, scenario data, runtime state, and save data must remain separate.
- Definitions need stable IDs.
- Player-facing text uses localization keys.
- Runtime state must be serializable from the start.
- Domain/runtime logic must consume plain C# data/state objects, not require ScriptableObject references.
- Validators are required for data/schema/localization.
- Do not hardcode production tunable gameplay values unless explicitly approved.

## Testing and CI

Production logic and bug fixes require TDD unless a human-approved exception exists:

1. write failing test;
2. verify RED;
3. implement minimal code;
4. verify GREEN;
5. run relevant regressions;
6. refactor only while green.

Required evidence layers:

- EditMode tests for domain/application logic;
- validators for data/content/localization;
- PlayMode/smoke tests for Unity integration;
- screenshot/video/review evidence for visual/UX/feel work;
- CI evidence once CI exists.

CI is required immediately after Unity project creation. Production PRs require merge-blocking checks unless a human-approved exception is documented.

## Unity Asset Rules

- Do not delete `.meta` files casually.
- Do not edit scenes, prefabs, ScriptableObjects, animation controllers, ProjectSettings, Packages, or lockfiles outside story/spike scope.
- List every changed `.unity`, `.prefab`, `.asset`, `.controller`, `.meta`, package, and settings file in the final report.
- Prefer code/data changes over scene/prefab changes when both are valid.
- Scene objects may wire and present state; they may not own canonical gameplay rules.
- Prefabs may not define unapproved gameplay rules.

## Git / PR / Evidence Rules

- Use a story- or spike-scoped branch.
- Commit only scoped changes.
- PR must link story/spike ID, GDD sections, ADR/control rules, and evidence.
- PR must include omissions/stubs/mocks/assumptions/deferred work, or explicitly say `No known omissions`.
- PR must link CI evidence once CI exists.
- No direct push to main for production work.

## Stop Conditions

Stop and report if:

- story is not READY and no approved spike applies;
- required source docs are missing/conflicting;
- ambiguity check would fail;
- required tests/CI cannot run;
- implementation requires unapproved mechanics, balance, UX, lore, names, assets, content, architecture, save/load, localization, packages, or data schema;
- gameplay rules are being pushed into MonoBehaviours for convenience;
- work would exceed scope;
- unrelated uncommitted changes are present;
- legal/IP/asset provenance risk appears.

## Final Response Required Format

Report:

- summary of changes;
- files changed, especially Unity assets/settings/packages;
- tests/checks/CI run and result;
- manual evidence paths if applicable;
- omissions/stubs/mocks/assumptions/deferred work or `No known omissions`;
- any stop-condition risks.

````

## Scoped `AGENTS.md` Templates

### Domain

Future path:

```text
Assets/NeonChampions/Runtime/Domain/AGENTS.md
````

```markdown
# Domain Agent Rules

Domain code owns approved gameplay rules, formulas, and state transitions.

Rules:

- No `UnityEngine` dependency unless explicitly approved.
- No MonoBehaviours, scenes, prefabs, or ScriptableObjects as direct domain requirements.
- Use plain C# data/state/value objects.
- Runtime state must remain serializable.
- Production logic and bug fixes require TDD/EditMode tests.
- No hardcoded tunable values unless explicitly approved.
- Stop if a GDD rule, formula, range, edge case, or acceptance criterion is unspecified.
```

### Application

Future path:

```text
Assets/NeonChampions/Runtime/Application/AGENTS.md
```

```markdown
# Application Agent Rules

Application code coordinates approved use cases between Domain and Unity-facing layers.

Rules:

- Do not invent gameplay rules.
- Keep APIs testable from EditMode tests.
- Depend on Domain, not Presentation.
- Do not introduce service locators, event buses, DI containers, or new architecture patterns without ADR approval.
- Stop if ownership/API boundaries are unclear.
```

### Presentation

Future path:

```text
Assets/NeonChampions/Runtime/Presentation/AGENTS.md
```

```markdown
# Presentation Agent Rules

Presentation adapts and displays state through Unity objects. It does not own canonical gameplay rules.

Rules:

- Player-facing strings must be localizable.
- Scene/prefab/UI work requires PlayMode/smoke evidence.
- Visual/UX/feel changes require screenshot/video/review evidence.
- Prefab fields affecting gameplay must trace to approved data/GDD rules.
- Do not decide final camera, grid, tile, animation, or feedback behavior unless authorized.
- Stop if UX, text, animation, feedback, or accessibility behavior is unspecified.
```

### Infrastructure

Future path:

```text
Assets/NeonChampions/Runtime/Infrastructure/AGENTS.md
```

```markdown
# Infrastructure Agent Rules

Infrastructure adapts Unity/file/platform services to approved application/domain needs.

Rules:

- No save/load format without approved ADR/story.
- No asset-loading architecture without approval.
- No networking, multiplayer, live-service, account, telemetry, or platform systems unless approved.
- Do not make runtime state scene-only or non-serializable.
- Stop if persistence/loading/platform ownership is unclear.
```

### Data

Future path:

```text
Assets/NeonChampions/Runtime/Data/AGENTS.md
```

```markdown
# Data Agent Rules

Data code supports approved definitions, schemas, import helpers, and validators.

Rules:

- Keep static definitions, scenario data, runtime state, and save data separate.
- Every definition needs a stable ID.
- Player-facing text uses localization keys.
- ScriptableObjects may be constrained early authoring assets, not domain/runtime dependencies.
- Validators are required for data/schema/localization.
- Preserve future external data, editor, datapack, and mod paths.
- Stop before choosing final schema/file format unless approved.
```

### Tests

Future path:

```text
Assets/NeonChampions/Tests/AGENTS.md
```

```markdown
# Test Agent Rules

Tests are production evidence, not optional cleanup.

Rules:

- EditMode tests cover domain/application logic.
- PlayMode/smoke tests cover Unity integration paths.
- Validators cover data/content/localization.
- Production logic and bug fixes use TDD unless explicitly excepted.
- Do not weaken tests outside story scope.
- Evidence must list exact commands/checks and results.
```

### Editor

Future path:

```text
Assets/NeonChampions/Editor/AGENTS.md
```

```markdown
# Editor Agent Rules

Editor code is editor-only tooling.

Rules:

- Editor code must not become runtime dependency unless approved.
- Validators/importers must produce reviewable output.
- Generated files/assets must be declared.
- Tooling stories need automated or script-level verification evidence.
- Stop if a tool would define gameplay/data authority not approved by ADR/GDD.
```

### Evidence

Future path:

```text
production/evidence/AGENTS.md
```

```markdown
# Evidence Agent Rules

Evidence packages prove what happened.

Required fields:

- story/spike ID;
- exact tests/checks run;
- pass/fail summary;
- CI link;
- manual evidence paths where applicable;
- changed Unity assets/settings/packages;
- omissions/stubs/mocks/assumptions/deferred work or `No known omissions`.

Do not use evidence files to change design authority. If docs are stale, update the correct source-of-truth layer through review.
```
