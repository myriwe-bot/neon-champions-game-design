---
title: Technical Decision Priorities
type: adr
status: draft
phase: technical-setup
owner: shared
created: 2026-05-27
updated: 2026-05-27
source_lore: []
related:
  [
    docs/architecture/unity-technical-scheme,
    docs/architecture/control-manifest,
    docs/architecture/data-authoring-options,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: pending
---

# Technical Decision Priorities

## Purpose

This document records which Unity technical decisions must be locked before prototypes, before production implementation, or later.

Principle: do not decide everything now. Decide the choices that would cause rework, agent ambiguity, or bad architecture if left open.

## Tier 1 — Required Before First Unity Prototype / Spike

### 1. Unity Version

Decision: approved.

- Unity: Unity 6.4.
- Exact target version: `6000.4.8f1`, assuming it is available and practical on the implementation machine.

Rule:

- If `6000.4.8f1` is unavailable, the implementer must stop and ask before creating or upgrading the project.
- No agent may silently choose a different Unity version.

### 2. Presentation Model

Decision: approved.

- Working default: 2.5D.

Meaning:

- Gameplay may use grid/graph/tile abstractions under the hood.
- Presentation may use 3D or 2.5D assets/camera treatment for readability and atmosphere.
- This does not yet decide the exact camera, grid, tile geometry, or combat-map representation.

### 3. Render Pipeline

Decision: approved.

- URP.

Reason:

- Better fit than Built-in for a new Unity project.
- Lighter and more appropriate than HDRP.
- Supports stylized 2.5D/3D presentation, lighting, and post-processing.

### 4. Prototype Repository Boundary

Decision: approved.

- Early Unity spikes may live in the future production Unity repo.
- Spike/prototype code must be explicitly isolated and labeled.
- Spike/prototype code may not enter production runtime paths without review.

Required marking:

- prototype question;
- success/failure criteria;
- throwaway vs candidate-production status;
- reuse restrictions.

## Tier 2 — Required Before Production Implementation

### 5. Folder / Assembly Layout

Decision: approved as default.

Default layout and assemblies are defined in `docs/architecture/unity-technical-scheme.md`.

Still required before production:

- final confirmation in the Unity repo after project creation;
- assembly definition files;
- dependency validation.

### 6. Data Authoring and Tooling Direction

Decision: approved.

Approved direction: Option D — Phased Hybrid.

Rules:

- Earliest prototypes may use constrained ScriptableObjects.
- Domain/runtime logic must consume plain C# data/state objects, not require ScriptableObject references.
- All definitions require stable IDs and localization keys.
- Runtime state must be serializable.
- Validators are required early.
- Scenario/map structure should be designed as serializable DTOs even if first edited through Unity.
- Architecture must preserve future map editors, scenario tools, balancers, datapacks, and modloaders.

See `docs/architecture/data-authoring-options.md`.

### 7. Test Framework

Decision: open, but rigorous default desired.

Minimum requirement: at least three test/evidence layers.

Proposed rigorous baseline:

1. Pure/domain automated tests
   - EditMode NUnit tests for domain and application logic.
   - Should cover rules, formulas, state transitions, serialization boundaries, deterministic behavior, and edge cases.

2. Data/schema validation tests
   - Automated validators for definitions, scenario files, map data, localization keys, references, IDs, ranges, and balance sanity checks.
   - Should run without manually opening scenes where practical.

3. Unity integration / PlayMode / smoke tests
   - PlayMode tests or controlled scene smoke tests for scene wiring, prefabs, UI flows, and Unity-specific integration.

Additional evidence layer:

4. Manual UX/visual/feel evidence
   - screenshots, short videos, or review protocols for visuals, UI clarity, feel, animation, and tactical readability.

Recommended default:

- Unity Test Framework + NUnit for EditMode and PlayMode.
- Custom validation tests/scripts for data and localization.
- Manual evidence required where automation is not realistic.

### 8. Input System

Decision: approved.

- Unity Input System.

Constraint:

- Do not design detailed input architecture until UX/control requirements exist.

### 9. Save / Load Strategy

Decision: partially approved.

- Save/load should come early, but not in the first prototype.
- Runtime state must be designed to be serializable from the start.
- No agent may invent the final save format without a separate ADR/story.

Implication:

- Domain/application state models should avoid Unity-scene-only ownership.
- Static definitions, scenario data, runtime state, and save data must remain conceptually separate.

### 10. CI / Build Setup

Decision: approved. See `docs/architecture/ci-build-automation.md`.

CI means continuous integration: automated checks that run on GitHub when code is pushed or a PR is opened.

Possible checks:

- compile project;
- run EditMode tests;
- run PlayMode/smoke tests if practical;
- run data validators;
- run localization-key validation;
- optionally create a development build.

Approved strict stance:

- GitHub Actions is the default CI provider.
- CI is required immediately after the Unity project is created, including spike PRs.
- Production PRs require merge-blocking automated checks unless a human-approved exception is documented.
- Exact Unity CLI commands, license setup, runner image, caching, and artifact retention can be finalized when the Unity repo exists.

## Cross-Cutting Requirement — Localization From Start

Decision: approved as a requirement.

All player-facing strings must be localizable from the start.

Rules:

- Do not hardcode player-facing strings in production UI/gameplay code.
- Use stable string IDs/keys for UI, unit names, faction names, tooltips, events, resources, errors, and tutorial text.
- Prototype-only hardcoded strings are allowed only if marked as prototype-only and listed as an omission.
- Data validation must detect missing localization keys for production content.
- Localization should be considered in UI layout, text length, font support, and screenshot/manual evidence.

Open decision:

- Unity Localization package vs custom localization layer vs hybrid.

Default direction:

- Use localizable string IDs in data/domain from the beginning.
- Choose concrete localization implementation before production UI stories.

## Tier 3 — Can Wait

Can wait until later milestone:

- final asset import rules;
- full localization pipeline details beyond key discipline;
- full save/load format;
- mod packaging format;
- mod security/sandboxing;
- advanced performance budgets;
- release platform compliance;
- full content pipeline automation.

## Current Gate Status

Production implementation remains blocked.

First Unity spike is approved as `production/spikes/spike-001-unity-project-ci-foundation.md`.

It can proceed only under these conditions:

- Unity `6000.4.8f1` availability is confirmed or revised by approval;
- the approved spike question is followed;
- prototype boundaries are obeyed;
- no production story is implied;
- once the Unity project exists, CI is added before the spike is considered complete.
