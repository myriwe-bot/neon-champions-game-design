---
title: STORY-STRAT-READ-002 Strategic Map Readability Pass
type: story
status: done
phase: production
owner: shared
created: 2026-06-17
updated: 2026-06-18
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-007-strategic-map-readability-bases-and-spatial-presentation,
    production/stories/story-tac-ai-001-neutral-guard-one-step-combat-ai,
    design/gdd/strategic-map,
    design/research/homm-like-strategic-map-topology-reference,
    production/planning/prototype-readability-and-map-next-steps-2026-06-15,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-STRAT-READ-002 Strategic Map Readability Pass

## Status

DONE / merged. Human approval recorded 2026-06-18 from chat: `STORY-STRAT-READ-002 approved`. Unity PR #55 merged 2026-06-18 as `e6e26835595db1cad51a3fbcdf3220d1391874cd`; post-merge Unity Foundation CI passed: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27745368044

Approved scope: a narrow strategic-map readability pass that improves reachable route/site feedback, path-cost preview, site category/state labels, interaction preview, and post-battle return summary without changing strategic topology or adding base/recruitment systems.

## Story type

Strategic UI / Playability Repair / Presentation Readability.

## Parent epic

- [EPIC-VSLICE-MVP-007 Strategic Map Readability, Bases, and Spatial Presentation](../epics/epic-vslice-mvp-007-strategic-map-readability-bases-and-spatial-presentation.md)

## User/player/system value

As a player, I want the strategic map to clearly show where I can go, what each site means, what an interaction will do, and what changed after battle, so the HoMM-like strategic layer becomes readable before larger base or map-presentation work begins.

## Source requirements

Exact source references:

- Parent epic:
  - `production/epics/epic-vslice-mvp-007-strategic-map-readability-bases-and-spatial-presentation.md` child story target: `STORY-STRAT-READ-002 Strategic Map Readability Pass`.
- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §§1-8 for MVP target, core loop, state contract, and UX/readability requirements.
  - `design/gdd/strategic-map.md` §9 for approved node-route topology and future tile/grid/region compatibility.
  - `design/gdd/strategic-map.md` §§10-13 for site state, resources/recruitment context, Champion movement, turn/scenario/victory structure.
- Planning source:
  - `production/planning/prototype-readability-and-map-next-steps-2026-06-15.md` §§7 Strategic map readability pass.
- Reference:
  - `design/research/homm-like-strategic-map-topology-reference.md` for map readability lessons; reference only, not direct implementation authority beyond cited story scope.
- ADR / architecture / control:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Prior prerequisite:
  - `production/stories/story-tac-ai-001-neutral-guard-one-step-combat-ai.md` DONE / merged.

## In scope

Concrete implementation tasks proposed by this story:

- Improve the current strategic map presentation/HUD for readability using existing graph-backed strategic state.
- Show clearer reachable route/site feedback from the active Champion's current movement/route state.
- Show path/route cost preview before committing movement, using existing route data only.
- Make site labels/cards more explicit for existing site categories and states, at minimum:
  - starting hub/base-like owned site;
  - resource site;
  - recruitment site;
  - guarded site;
  - central objective;
  - data/cache site if currently present in the scenario;
  - ownership/controlled/uncontrolled/guarded/cleared state where applicable.
- Improve interaction preview text before commitment: move, battle, recruit/reinforce if already supported, collect/reward if already supported, contest, blocked/invalid.
- Improve post-battle return summary text for already-supported outcomes: losses/damage summary if available, reward gained, site captured/controlled, objective countdown/progress if applicable.
- Keep changes presentation/application-facing where possible; domain rule changes are allowed only when needed to expose already-existing state through snapshots/results.
- Add focused tests for route/site/path/interaction/return-summary text and no-regression smoke for existing strategic-to-tactical flows.
- Add PlayMode PNG evidence under `production/evidence/STORY-STRAT-READ-002/` showing the improved strategic map readability state.

## Out of scope

Not authorized by this story:

- No full tile/hex strategic topology, freeform map movement, route construction/destruction, terrain pathfinding, procedural map generation, or map editor.
- No new base system, town-building tree, garrison management, recruitment economy, stock refresh, or new reinforcement rules.
- No strategic AI, fog/misinformation layer, weather/logistics/supply, market simulation, or full economy.
- No new tactical combat rules, tactical UI changes, unit roster/balance changes, or new site mechanics beyond presenting already-supported interactions.
- No final map art, final icons, VFX, audio, animation, portraits, final lore copy, or localization pass.
- No broad scene/prefab/ProjectSettings/package changes unless narrowly required for evidence/presentation and explicitly listed in the PR.

## Allowed stubs, mocks, placeholders, or temporary data

- Existing prototype node/site/route labels remain allowed.
- Placeholder presentation strings/icons/markers are allowed if clear and covered by tests/evidence.
- Existing graph topology and scenario content remain the rules source; no new strategic map data model is required unless needed to expose existing state.

## Dependencies

- Required prior stories:
  - `STORY-TAC-AI-001` DONE / merged.
- Required data/assets:
  - Existing strategic map scenario, nodes, routes, sites, Champion state, battle result application, objective state, and UI/presentation surfaces.
- Required architecture decisions:
  - Existing Unity technical scheme/control manifest; no new ADR required if this remains a presentation/readability pass.
- Required Unity/package setup:
  - Existing Unity project and CI.

## Acceptance criteria

- [ ] Given the active Champion is selected, the strategic map/HUD visibly communicates reachable route/site options or why no route/site is reachable.
- [ ] Given a route or destination is selected/previewed, the player-facing preview includes path/route cost or movement implication before committing.
- [ ] Given visible sites exist on the current map, site labels/cards distinguish current site category and state for existing base/start, resource, recruitment, guarded, objective, and data/cache-style sites where present.
- [ ] Given a site interaction is previewed, the preview clearly states the likely interaction type before commitment: move, battle, recruit/reinforce if already supported, collect/reward if already supported, contest, or blocked/invalid.
- [ ] Given a guarded battle resolves and returns to the strategic map, the return summary clearly communicates already-supported outcome facts such as site control, reward/resource change, and objective countdown/progress if applicable.
- [ ] Given invalid strategic actions are attempted, denial text remains visible and specific.
- [ ] Existing strategic movement, site interaction, guarded battle, Champion-vs-Champion, objective, Intel/cache, recruitment, and tactical handoff/return smoke behavior is not intentionally regressed.

## Verification requirements

- Unit tests: Required only if new pure formatting/state projection helpers are introduced.
- Unity edit-mode tests: Required for strategic snapshot/result text where testable outside scene.
- Unity play-mode tests: Required for visible strategic-map readability surfaces, interaction preview, and post-battle return summary.
- Integration/data validation tests: Existing placeholder validator must remain green; add validation only if new authored data files are introduced.
- Manual Unity scene/prefab checks: Supplemental only.
- Screenshot/video evidence: Required PNG evidence under `production/evidence/STORY-STRAT-READ-002/` in the Unity repo.
- Performance budget or N/A: N/A; readability projection must be deterministic and cheap.
- CI evidence: Unity Foundation CI exact-head before merge.
- Playtest evidence, if applicable: Optional after implementation; not required before PR.
- TDD evidence required? Yes for projection/preview/summary behavior where practical.
- Automation deferred? No broad exception approved.

## Ambiguity Check

Status: PASS. Human approval recorded 2026-06-18.

Human-approved answers:

1. Approved as the next implementation packet.
2. Narrow source-authority exception approved for the cited draft planning note and draft reference note only as bounded context for this story; approved GDD/ADR/control docs remain authoritative.

Approved assumptions:

- The pass improves readability of existing strategic mechanics only; it does not add new strategic rules.
- Placeholder labels/icons/markers may be used if clear, deterministic, and covered by evidence.
- Exact text may be implementation-owned if it communicates the acceptance criteria and avoids final lore/content lock.

Out of scope:

- Tile/hex topology, base/recruitment expansion, strategic AI, fog/logistics/weather, full economy, new tactical rules, final art/content.

Allowed stubs/mocks:

- Prototype labels, markers, and presentation strings for existing nodes/sites/routes/interactions.

Human-approved exceptions:

- The cited draft planning note `production/planning/prototype-readability-and-map-next-steps-2026-06-15.md` §7 and draft reference note `design/research/homm-like-strategic-map-topology-reference.md` are approved only as bounded context for this story's readability scope. They do not authorize broader topology, base/recruitment, economy, fog/logistics, strategic AI, or final-content work.

If status is FAIL, this story is not READY.

## Branch / PR requirements

- Branch name: `story/STORY-STRAT-READ-002-strategic-map-readability-pass`.
- PR title: `STORY-STRAT-READ-002 Strategic map readability pass`.
- Required linked story ID: `STORY-STRAT-READ-002`.
- Required linked GDD/ADR/control docs:
  - `design/gdd/strategic-map.md`.
  - `design/research/homm-like-strategic-map-topology-reference.md`.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: read Unity root `AGENTS.md` plus scoped AGENTS files for all touched Runtime/Application/Presentation/Tests/Evidence directories.
- Required evidence summary: tests run, PlayMode/PNG evidence path, CI URL.
- Required omissions section: explicitly list known omissions/stubs/placeholders/deferred work or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked or explicitly N/A.
- [x] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval has been given or delegated gate approval is recorded.

## DONE gate

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required verification evidence exists: `production/evidence/STORY-STRAT-READ-002/` in the Unity repo.
- [x] Required automated tests, validators, and PlayMode/smoke evidence pass.
- [x] No unauthorized design or architecture decisions were introduced.
- [x] Omissions/stubs/mocks/deferred work are explicitly documented in Unity PR #55.
- [x] PR/code review is complete: https://github.com/myriwe-bot/neon-champions-unity/pull/55
- [x] CI passes: PR exact-head Unity Foundation CI https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27744712697 and post-merge main CI https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27745368044
- [x] Required docs were updated in the correct source-of-truth layer.

## Verdict

DONE / merged.
