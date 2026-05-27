---
title: Testing Strategy
type: adr
status: approved
phase: technical-setup
owner: shared
created: 2026-05-27
updated: 2026-05-27
source_lore: []
related: [docs/architecture/architecture, docs/architecture/unity-technical-scheme, docs/architecture/control-manifest, docs/architecture/ci-build-automation, production/stories/story-template, production/epics/epic-template]
approval: approved
---

# Testing Strategy

## Decision

Neon Champions adopts a strict layered testing strategy for production implementation.

No production story is DONE without evidence from the correct test or evidence layer. Agents may not claim completion from compilation, manual inspection, or editor play alone.

The stricter option is approved: Unity integration should become automated PlayMode coverage wherever feasible. Manual Unity evidence is allowed as supplemental evidence, or as a temporary exception only when automation is not practical yet and the exception is explicitly documented.

## Rationale

Neon Champions is intended to be built through strict AI-assisted implementation. The project therefore needs tests and evidence that prevent agents from silently inventing behavior, hiding Unity wiring problems, or treating visual/editor success as production correctness.

The strategy separates:

- pure gameplay correctness;
- data/content validity;
- Unity integration correctness;
- UX/visual/feel review;
- per-story implementation accountability.

## Required Test and Evidence Layers

### 1. Domain / Rules Tests

Type: automated Unity EditMode NUnit tests.

Covers:

- pure gameplay rules;
- formulas;
- tactical and strategic state transitions;
- turn resolution;
- deterministic random behavior;
- serialization-safe state objects;
- edge cases from GDD acceptance criteria.

Rules:

- Domain code should be testable without scenes, prefabs, MonoBehaviours, or ScriptableObject references.
- Production gameplay rules require automated tests unless a human-approved exception is documented.
- New production logic should follow TDD: failing test first, verify RED, implement, verify GREEN, then refactor.

### 2. Data / Schema / Content Validation

Type: automated validators and validation tests.

Covers:

- stable IDs;
- duplicate IDs;
- missing references;
- localization keys;
- invalid numeric ranges;
- missing required fields;
- scenario/map structure sanity;
- balance sanity checks where ranges are approved.

Rules:

- Data is not valid merely because Unity loads it.
- Data is valid only when the approved validators pass.
- Data schema changes require validation evidence.
- Player-facing content must satisfy localization-key validation.

### 3. Unity Integration / PlayMode / Smoke Tests

Type: automated Unity PlayMode tests, supplemented by explicit smoke protocols where needed.

Covers:

- scene boot;
- prefab wiring;
- UI flows;
- scene transitions;
- presentation/application integration;
- save/load smoke when the save system is approved;
- Unity package/configuration integration.

Rules:

- Unity-specific behavior should have automated PlayMode coverage wherever feasible.
- Manual Unity checks alone are not enough for recurring production integration paths.
- If a Unity behavior cannot yet be automated, the story must document why, provide manual evidence, and identify whether a later automation story is required.
- Scene/prefab/UI stories must define their PlayMode or smoke evidence before they can be READY.

### 4. UX / Visual / Feel Evidence

Type: screenshots, short clips, checklist-based review, or playtest notes.

Covers:

- readability;
- feedback clarity;
- animation/feel;
- tactical legibility;
- player understanding of cause and effect;
- accessibility basics.

Rules:

- Subjective presentation work needs recorded evidence, not only code tests.
- Visual/feel work should still include PlayMode/smoke coverage if scene, prefab, or UI wiring changes.
- Review protocols must be explicit enough that another reviewer can repeat them.

### 5. Story Evidence Package

Type: per-story evidence section in the story and PR.

Required for every implementation story:

- exact tests run;
- pass/fail output or log location;
- manual evidence path if applicable;
- known omissions, stubs, mocks, assumptions, and deferred work, or `No known omissions`;
- links to exact GDD sections and ADR/control-manifest rules;
- CI status when CI exists.

## Story Type to Required Evidence Matrix

| Story type | Required evidence |
|---|---|
| Logic | Domain/EditMode tests. Data validation if definitions are touched. |
| Config/Data | Validator tests. Representative load/parse test. Localization validation if player-facing strings exist. |
| Integration | EditMode or integration tests plus PlayMode/smoke tests for Unity-facing behavior. |
| UI | PlayMode/smoke tests for flow and wiring; screenshot/video evidence for layout/readability. |
| Visual/Feel | Screenshot/video/review protocol; PlayMode/smoke tests if Unity wiring changes. |
| Content | Data validation; localization validation; lore/design source traceability; review evidence if player-facing. |
| Tooling | Automated tests or script-level verification; sample input/output evidence. |
| Test | Demonstrates the intended failing/passing behavior or improves coverage with evidence. |
| Playtest | Playtest protocol, notes, findings, and resulting decisions: keep, revise, reject, or retest. |

## TDD Requirement

For production logic and bug fixes:

1. Write the smallest failing test first.
2. Run it and verify it fails for the expected reason.
3. Implement the smallest change that passes.
4. Run the focused test and verify it passes.
5. Run relevant regression tests.
6. Refactor only while tests remain green.

Prototype/spike work may skip strict TDD only if explicitly marked prototype-only and not silently promoted to production.

## Automation Direction

The project should move toward:

- EditMode tests for domain/application logic;
- automated validators for data/content/localization;
- PlayMode tests for recurring Unity integration paths;
- CI commands that can run all relevant test layers, governed by `docs/architecture/ci-build-automation.md`;
- evidence folders under `production/evidence/` or an equivalent approved location.

Exact Unity test commands and evidence folder conventions remain implementation details to be finalized when the Unity project exists. CI is required immediately after Unity project creation under `docs/architecture/ci-build-automation.md`.

## Agent Stop Conditions

Agents must stop instead of implementing or claiming DONE if:

- required tests cannot be run and no approved alternate evidence exists;
- the required test/evidence layer is unclear;
- acceptance criteria are not observable;
- a story lacks exact evidence requirements;
- implementation would require unapproved architecture, data, save/load, input, or localization decisions;
- gameplay rules are being placed in MonoBehaviours because pure/domain testing is inconvenient;
- a Unity integration path needs automation but the story does not define whether automation is in-scope or deferred.

## Approval Scope

This ADR approves:

- strict layered testing as production policy;
- TDD for production gameplay logic and bug fixes;
- automated validators for data/content/localization;
- automated PlayMode coverage as the target for Unity integration;
- manual evidence as supplemental or explicitly temporary evidence;
- per-story evidence packages as mandatory.

This ADR does not yet approve:

- exact Unity test runner commands;
- exact Unity CI commands and runner/license details;
- final evidence folder naming conventions;
- full list of validators for concrete schemas;
- performance benchmark thresholds.

Current verdict: APPROVED.
