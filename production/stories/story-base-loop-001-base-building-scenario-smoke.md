---
title: STORY-BASE-LOOP-001 Base-Building Scenario Smoke
type: story
status: done
phase: production
owner: shared
created: 2026-06-27
updated: 2026-06-27
source_lore: [greenland, white-sky, digital-net]
related:
  [
    production/epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction,
    production/stories/story-map-real-001-scenario-authored-strategic-map-shell,
    production/stories/story-base-001-base-definition-and-facility-construction-core,
    production/stories/story-base-002-administration-income-chain-and-recruitment-dwellings,
    production/stories/story-map-site-001-site-route-base-and-objective-readability-pass,
    design/gdd/strategic-map,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# Story: STORY-BASE-LOOP-001 Base-Building Scenario Smoke

## Status

DONE / merged. Unity PR #83 merged 2026-06-27 as `e37c2c92d27329020a3d6ae4ce99b4a4767391e4`; exact-head PR Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28291273686. Post-merge `main` Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/28291619707.

Approved scope was one narrow connected smoke over existing EPIC-009 systems: base build, income/recruitment refresh, movement/site interaction or battle, and objective readability. No new mechanics, rules, content, or tactical combat changes were authorized.

## Player value

Prove the EPIC-009 base-building work as one connected playable loop instead of isolated feature panels: select Champion, inspect home base, build a facility, see income/recruitment pressure, move to a site, fight or interact, and keep objective pressure readable.

## Design intent

This is a smoke/connection story, not a new systems story. It should use the existing scenario-authored map, existing base/facility data, existing income/recruitment services, existing route/site/objective systems, and existing tactical handoff. The goal is one demonstrable base-building scenario path with clear feedback and evidence.

## Scope

### In scope

- Add or refine a narrow PlayMode smoke path that exercises:
  - selected active Champion on the strategic map;
  - home base selection and facility build preview;
  - committing one legal base facility build;
  - ending turns enough to observe recurring income/recruitment refresh from the built facility;
  - route movement to a meaningful site;
  - a site interaction or guarded battle handoff/result path;
  - objective status remaining visible after the loop.
- Add snapshot/domain tests only where needed to lock the connected loop state and prevent regressions.
- Add player-facing feedback strings only where the loop is currently ambiguous.
- Add committed evidence under `production/evidence/STORY-BASE-LOOP-001/generated/`.
- Keep evidence README with commands, CI link placeholder, changed asset inventory, and omissions.

### Out of scope

- New facility tiers, costs, effects, resources, factions, units, routes, sites, objectives, or victory rules.
- Balance tuning beyond exact values already authored in the scenario.
- Base capture, siege, garrisons, marketplace, supply/logistics, fog, strategic AI, or map editor UI.
- Tactical combat rule changes.
- Final art, icons, animation, audio, VFX, or localization pass.
- Refactoring unrelated systems for style.

## Acceptance criteria

- `STORY-BASE-LOOP-001` has one deterministic PlayMode smoke that can run in CI and proves the base-building loop from base action through downstream strategic pressure.
- The smoke verifies concrete state, not only screenshots:
  - facility was constructed;
  - resources changed by build cost and/or later recurring income;
  - recruitment/dwelling stock or offer availability reflects the existing built-facility rules where applicable;
  - Champion movement/site interaction still works after base actions;
  - objective status remains visible and non-regressed.
- Player-facing UI/evidence shows readable steps for:
  - base selected;
  - facility build result;
  - income/recruitment refresh after turn advance;
  - movement/site interaction or battle handoff;
  - objective status.
- Existing MAP-REAL-001, BASE-001, BASE-002, and MAP-SITE-001 tests continue passing.
- No new Unity asset/settings/package/lockfile changes unless explicitly required and documented.
- Evidence README lists exact commands and generated PNGs.

## Required verification

- Placeholder validator passes.
- EditMode tests pass.
- PlayMode tests pass with story evidence generated.
- Standalone Windows64 build passes.
- Unity Foundation CI passes at exact PR head before merge.
- Post-merge `main` Unity Foundation CI passes before marking DONE.

## Suggested evidence captures

- `story-base-loop-001-base-build-result.png`
- `story-base-loop-001-income-refresh.png`
- `story-base-loop-001-move-site-interaction.png`
- `story-base-loop-001-objective-pressure.png`

## Implementation notes

Prefer adding one named PlayMode test over broad UI rewrites. If the existing UI already exposes the needed state, assert against existing `StrategicMapPresentationSnapshot` fields and visible text. If a feedback line is missing, add the smallest presentation/session text needed to make the smoke understandable.

## Readiness / ambiguity gate

- [x] Human approval is recorded.
- [x] Implementer can complete the story without inventing new design, content, rules, balance, UX, canon, or architecture decisions.
- [x] Existing source systems and exact story scope are enough to implement the smoke.
- [x] Out-of-scope list blocks likely scope creep.

## DONE gate

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required verification evidence exists.
- [x] Required automated tests, validators, and PlayMode/smoke evidence pass.
- [x] Docs have been updated in the correct source-of-truth layer.
- [x] No open blocker remains hidden.
- [x] Human review accepts the story as complete.

## Verdict

DONE / merged. EPIC-009 implementation train is complete enough for the next QA/playtest closeout candidate: `STORY-QA-012`.
