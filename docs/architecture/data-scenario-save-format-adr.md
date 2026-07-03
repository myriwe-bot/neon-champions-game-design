---
title: Data, Scenario, and Save Format ADR
type: adr
status: approved
phase: technical-setup
owner: shared
created: 2026-07-03
updated: 2026-07-03
source_lore: []
related:
  [
    production/planning/post-audit-foundation-pivot-2026-07-03,
    production/epics/epic-vslice-mvp-015-post-audit-foundation-pivot-and-reconciliation,
    docs/architecture/data-authoring-options,
    docs/architecture/control-manifest,
    design/registry/entities,
    design/registry/formulas,
    design/registry/terms,
  ]
approval: approved
---

# Data, Scenario, and Save Format ADR

## Decision

Use a thin external-text data contract as the first canonical data path for static definitions and scenario authoring, imported into plain C# domain/application DTOs and validated before runtime use.

For the next implementation slice:

- represent the current playable scenario in reviewable text data, preferably JSON for Unity/.NET importer simplicity;
- keep static definitions, scenario data, runtime state, and save data separate;
- keep runtime/domain models engine-free and serializable;
- validate IDs, references, ranges, and required fields before creating runtime state;
- preserve existing gameplay behavior during extraction.

This refines the approved `Data Authoring Direction` phased-hybrid decision after the audit showed that the project has not actually used ScriptableObjects or external data yet, while the single scenario has grown inside C#.

## Context

The audit found three linked problems:

1. `design/registry/entities.yaml`, `formulas.yaml`, and `terms.yaml` are empty stubs despite being named as anti-drift foundations.
2. Unity has no meaningful Data layer yet; the current playable scenario is hardcoded in C#.
3. The control manifest says tunables should not be hardcoded, but most scenario/content values are currently code constants.

The existing implementation is still well-positioned: runtime/domain state uses stable IDs and serializable plain C# objects, and Domain/Application layering is engine-free.

## Boundaries

### Static definitions

Examples: factions, unit types, site types, resources, tactical actions, facility definitions, operation definitions, status definitions, localization keys.

Rules:

- Immutable at runtime.
- Stable human-readable IDs.
- Validated independently from scenarios.
- May later move to ScriptableObject importers or generated assets, but text remains reviewable source or export.

### Scenario data

Examples: scenario metadata, map nodes/routes, site placement, starting factions/Champions/armies/resources, base ownership/facilities, objectives, authored terrain/context tags, initial Intel visibility.

Rules:

- Authored content, not save data.
- References static definitions by stable ID.
- Must be loadable without Unity scene/prefab mutation.
- First goal is to represent the current smoke scenario without changing behavior.

### Runtime state

Examples: active turn, current resources, positions, army losses, site ownership, verified/stale Intel, constructed facilities, tactical battle state.

Rules:

- Created from static definitions + scenario data.
- Mutated only by domain/application services.
- Serializable plain C# remains required.
- Not authored directly as scenario content.

### Save data

Save data is a serialized runtime-state snapshot plus references to static/scenario data identity and version.

Rules for now:

- No full save/load UI is approved by this ADR.
- Save shape must not be blocked by the scenario extraction path.
- Future save ADR may choose exact versioning/migration semantics.

## First implementation implication

`STORY-DATA-001` should not build a full editor. It should:

1. inspect `StrategicMapPresentationSmokeScenario` and related factories;
2. define the smallest data schema needed for the current scenario;
3. add a checked-in sample scenario data file;
4. add validation for duplicate/missing/unknown IDs and basic ranges;
5. load/convert that data into the same runtime definitions/state currently produced by code;
6. prove with tests and PlayMode smoke that gameplay-visible behavior did not change.

## Registry policy

The empty registry files must stop being implied authority.

Near-term rule:

- scenario/static data files become the authority for implemented content values;
- registry files may either be populated by reverse-sync from implemented data or explicitly demoted to glossary/planning aids;
- no story may claim registry coverage while the relevant registry file is still a stub.

## Determinism note

This ADR assumes deterministic runtime behavior remains valid. It does not resolve damage variance or seeded RNG. A separate determinism decision record should either:

- embrace determinism as identity and move uncertainty into dirty/source-tagged information; or
- require a seeded RNG service with replay/test controls.

Until then, scenario extraction must not introduce randomness.

## Consequences

Positive:

- unblocks scenario variation, balancing, dumb AI playtests, save/load planning, and future editor work;
- makes hardcoded tunables visible;
- gives the placeholder validator a real target;
- reduces GDD/code drift.

Costs:

- requires schema/version discipline earlier than a throwaway prototype would;
- creates importer/validator surface area;
- may expose many hardcoded constants that need triage instead of immediate cleanup.

## Non-goals

- Full map editor.
- Full save/load feature.
- Mod/datapack packaging.
- Localization system completion.
- Rewriting all tactical/unit/faction data at once.
- Replacing every existing code constant in one story.

## Gate

APPROVED as a thin direction. If implementation discovers that JSON is materially worse than another text format for Unity/CI/tooling, stop and update this ADR before extraction proceeds.
