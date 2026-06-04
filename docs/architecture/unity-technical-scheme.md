---
title: Unity Technical Scheme
type: adr
status: approved
phase: technical-setup
owner: shared
created: 2026-05-27
updated: 2026-05-28
source_lore: []
related:
  [
    docs/architecture/architecture,
    docs/architecture/control-manifest,
    docs/architecture/technical-decision-priorities,
    docs/architecture/data-authoring-options,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    design/workflow,
  ]
approval: approved
approval_scope: SPIKE-001 foundation scaffold and technical setup boundaries; unresolved architecture areas remain explicit blockers for later production stories.
---

# Unity Technical Scheme

## Purpose

The Unity Technical Scheme defines the approved technical boundaries for Neon Champions production implementation.

It exists so Codex and other agents cannot silently decide:

- Unity version;
- project structure;
- scene ownership;
- data format;
- testing strategy;
- architecture patterns;
- prototype vs production-code boundaries.

No production Unity implementation may begin until the relevant parts of this scheme are approved or explicitly marked N/A.

## Core Technical Principle

Gameplay rules should be implemented as testable C# domain logic wherever practical.

Unity objects should present, adapt, serialize, and connect systems. They should not be the primary owner of complex game rules unless explicitly approved.

In short:

- GDDs define rules.
- Domain logic implements rules.
- Unity presents and orchestrates rules.
- Data assets configure rules.
- Tests verify rules.

## Initial Unity Defaults

Unless later revised:

- Engine: Unity 6.4.
- Exact target version: `6000.4.8f1`, subject to confirmation on the implementation machine.
- Language: C#.
- Target first: desktop prototype / PC.
- Game type: single-player turn-based strategy/RPG.
- Presentation model: 2.5D working default.
- Render pipeline: URP.
- Input: Unity Input System.
- Networking: out of scope for MVP.
- Multiplayer: out of scope.
- Live service/account systems: out of scope.
- Mobile-first constraints: out of scope.
- Production implementation: blocked until READY stories exist.

Open decisions:

- concrete data schemas and tooling for the approved phased-hybrid data direction;
- save/load format;
- exact Unity CI commands, Unity license/activation, runner image, caching, and artifact retention policy;
- localization implementation package/layer.

Approved CI/build stance: see `docs/architecture/ci-build-automation.md`. GitHub Actions is the default provider, and CI is required immediately after Unity project creation, including spike PRs.

## Project Layout Standard

The production Unity repo should separate game logic, Unity adapters, content/data, tests, and docs.

Proposed top-level layout:

```text
Assets/
  NeonChampions/
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
Packages/
ProjectSettings/
docs/
  architecture/
production/
  evidence/
```

Meaning:

- `Domain`: pure or mostly pure C# gameplay rules.
- `Application`: use cases and orchestration between domain and Unity-facing layers.
- `Presentation`: MonoBehaviours, UI controllers, scene interaction, VFX/audio triggers.
- `Infrastructure`: persistence, loading, Unity services, file IO, platform glue.
- `Data`: schemas, definitions, validators, import helpers.
- `Editor`: editor tooling only.
- `Tests`: Unity EditMode and PlayMode tests.

## Assembly Boundary Standard

Use assembly definitions to prevent everything from depending on everything.

Proposed assemblies:

- `NeonChampions.Domain`
- `NeonChampions.Application`
- `NeonChampions.Infrastructure`
- `NeonChampions.Presentation`
- `NeonChampions.Tests.EditMode`
- `NeonChampions.Tests.PlayMode`

Dependency direction:

```text
Presentation -> Application -> Domain
Infrastructure -> Application / Domain where approved
Tests -> all tested assemblies
Domain -> no UnityEngine dependency unless explicitly approved
```

Rule: `Domain` should not depend on `UnityEngine` by default.

If a domain system needs vectors, randomization, time, or serialization, use approved abstractions or simple project-owned value types.

## Data Authoring Policy

Default direction:

- Game definitions should be data-driven.
- Tuning values should not be hardcoded in production gameplay code.
- Data authoring requires a separate decision because map editors, scenario editors, balancing tools, datapacks, and modloaders are likely project goals.
- See `docs/architecture/data-authoring-options.md`.
- Runtime mutable state must be separate from static definitions.
- Runtime state must be serializable from the start.

Data categories:

1. Static definitions
   - unit types;
   - Champion archetypes;
   - faction definitions;
   - site definitions;
   - resource definitions;
   - tactical action definitions.

2. Scenario data
   - map layout;
   - starting factions;
   - sites;
   - scripted crisis state;
   - starting Champions/resources.

3. Runtime state
   - current turn;
   - unit positions;
   - resource amounts;
   - site ownership;
   - tactical battle state;
   - discovered/hidden information.

Rule: do not mix static definitions and runtime state in the same asset unless explicitly approved.

## Scene Ownership Policy

Scenes should be thin containers, not hidden game-state owners.

Initial proposed scenes:

- `Boot`
- `MainMenu`
- `StrategicMap`
- `TacticalBattle`
- `Loading` / `Transition`, if needed later

Rules:

- Scene objects may wire dependencies and present state.
- Scene objects may not own canonical gameplay rules.
- Persistent game state must not live only in scene objects.
- Scene-specific hacks must be marked prototype-only or documented as omissions.

## Prefab Policy

Prefabs are presentation/configuration assets, not design authority.

Rules:

- Prefabs may represent UI panels, map nodes, units, effects, and interactables.
- Prefabs may not define unapproved gameplay rules.
- Prefab fields that affect gameplay must trace to approved data definitions or GDD rules.
- Manual Unity verification is required for prefab changes.

## Save / Load Boundary

Save/load should come early, but not in the first prototype.

Default:

- Save/load architecture is a known early need.
- Production systems should not make save/load difficult or impossible.
- Runtime state must be serializable from the start.
- Do not implement the final save system until a READY story and ADR exist.
- No agent may invent the save format.

Open decision:

- exact save format and versioning strategy.

## Input Policy

Decision: Unity Input System.

Temporary default:

- Do not build detailed input architecture until UX/control requirements exist.
- Tactical and strategic interactions must eventually be specified in UX docs.

## Testing Strategy

Approved policy: see `docs/architecture/testing-strategy.md`.

Required layers:

1. Pure/domain automated tests
   - Unity Test Framework / NUnit EditMode tests for domain and application logic.
   - Covers rules, formulas, state transitions, serialization boundaries, deterministic behavior, and edge cases.

2. Data/schema validation tests
   - Automated validators for definitions, scenario files, map data, localization keys, references, IDs, ranges, and balance sanity checks.

3. Unity integration / PlayMode / smoke tests
   - Automated PlayMode tests are the target for scene wiring, prefabs, UI flows, and Unity-specific integration.
   - Manual Unity evidence is supplemental, or temporary only when automation is not practical yet and the exception is documented.

4. Manual UX/visual/feel evidence
   - Screenshots, short videos, or review protocols for visuals, UI clarity, feel, animation, and tactical readability.

Preferred testing split:

- Domain rules: automated EditMode tests.
- Data definitions: validation tests.
- Application orchestration: EditMode or integration tests.
- Presentation/UI: PlayMode/smoke tests plus screenshots/video where player-facing.
- Visual/feel: screenshot/video/review protocol plus PlayMode/smoke coverage when Unity wiring changes.

Production logic and bug fixes should follow TDD: write a failing test first, verify RED, implement, verify GREEN, then refactor.

## Localization Requirement

Localization must be considered from the start.

Rules:

- All player-facing strings must be localizable.
- Production UI/gameplay code may not hardcode player-facing strings.
- Use stable string IDs/keys for UI labels, unit names, faction names, tooltips, events, resources, error text, tutorials, and narrative text.
- Prototype-only hardcoded strings are allowed only if marked as prototype-only and listed as omissions.
- Data validation must detect missing localization keys for production content.
- UI work must consider text expansion, fonts, readability, and layout constraints.

Open decision:

- Unity Localization package vs custom localization layer vs hybrid.

## Prototype vs Production Code

Prototype code is allowed only when explicitly marked Spike/Prototype.

Prototype code must declare:

- question being answered;
- success/failure criteria;
- throwaway or candidate-production status;
- what cannot be reused without review.

Rules:

- Prototype code does not authorize production architecture.
- Prototype code cannot be promoted silently.
- Production code must come from READY stories.
- If prototype code is reused, a review must identify what is kept, rewritten, or discarded.

## Package Policy

Default:

- Do not add third-party Unity packages during feature work.
- New packages require architecture approval.
- Package approval must document:
  - purpose;
  - license;
  - maintenance risk;
  - alternatives considered;
  - impact on builds/tests;
  - whether it is allowed in prototype only or production.

## Agent Stop Conditions

Codex must stop if:

- Unity version is needed but not approved;
- render pipeline choice affects the task but is undecided;
- folder/assembly ownership is unclear;
- data should be ScriptableObject vs external file but no rule exists;
- scene/prefab ownership is unclear;
- task requires save/load decisions;
- task requires input architecture decisions;
- tests cannot be written or run as required;
- implementation would put gameplay rules into MonoBehaviours because it is convenient;
- implementation would hardcode tunable gameplay values.

## Approval Scope

This scheme is approved for SPIKE-001 foundation work and technical setup boundaries. Approving this scheme does not approve the full future Unity architecture.

It approves:

- the separation of domain logic from Unity presentation;
- the need for explicit assembly boundaries;
- the default data-driven approach;
- the scene/prefab ownership constraints;
- the prototype vs production boundary;
- the strict layered testing expectations;
- the list of open Unity decisions.

Still not approved:

- concrete data schemas and tooling for the approved phased-hybrid data direction;
- save/load format and versioning;
- localization implementation package/layer;
- exact Unity CI commands, Unity license/activation, runner image, caching, and artifact retention policy.

Current verdict: APPROVED for SPIKE-001 foundation scaffold and technical setup boundaries; full production architecture remains gated by the open decisions above.
