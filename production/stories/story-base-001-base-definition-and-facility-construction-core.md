---
title: STORY-BASE-001 Base Definition and Facility Construction Core
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-06-26
updated: 2026-06-26
source_lore: [greenland, white-sky]
related:
  [
    production/epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction,
    production/stories/story-map-real-001-scenario-authored-strategic-map-shell,
    design/gdd/strategic-map,
    design/research/homm-town-building-reference,
    design/research/homm-like-strategic-map-topology-reference,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: pending
---

# STORY-BASE-001 Base Definition and Facility Construction Core

## Status

READY-candidate / approval pending. Drafted after `STORY-MAP-REAL-001` merged and post-merge Unity main CI passed. This is the recommended next EPIC-009 implementation packet, but it is not READY until human approval is recorded and the guarded prompt is converted to runnable.

## Story type

Strategic Rules + UI + Validation.

## Parent epic

- [EPIC-VSLICE-MVP-009 Strategic Map Geography, Bases, and Facility Construction](../epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction.md)

## User/player/system value

As a player, I want my starting base to expose a small, understandable build choice with resource costs and one-build-per-turn timing, so that bases begin to feel like owned operational anchors without introducing the full economy, dwellings, capture, or town-tree systems yet.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §§1-11 for current MVP loop, resources, recruitment, sites, and graph-backed strategic rules.
  - `design/gdd/strategic-map.md` §12 for base/facility authoring posture, simple construction, resource costs, prerequisites, and one build per base per turn.
  - `design/gdd/strategic-map.md` §§13-16 for movement/turn boundaries, DTO boundaries, and acceptance criteria.
- Research / planning:
  - `design/research/homm-town-building-reference.md` for the town-building extraction: copy the shape of economic/recruitment/support investment, not the full HoMM town tree.
  - `design/research/homm-like-strategic-map-topology-reference.md` for preserving graph-backed map rules.
  - `production/epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction.md` human direction snapshot: resource-costed simple facilities, one build per base per turn, starting bases uncapturable, no editor UI.
- ADR / architecture / control-manifest:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

## In scope

Concrete implementation tasks authorized after approval:

- Add scenario-authored base facility definition data sufficient for the first build core:
  - stable facility ID;
  - display/localization key;
  - owning/available base reference or facility catalog reference compatible with authored bases;
  - facility lane/type such as `administration`, `recruitment`, or `support`;
  - resource cost list;
  - prerequisite facility IDs;
  - build-state metadata needed to serialize constructed/unbuilt facilities.
- Add runtime state for starting bases and constructed facilities:
  - base ID;
  - owning faction ID;
  - node ID;
  - constructed facility IDs;
  - whether this base has already built this turn.
- Add a build command/service for current-player base construction:
  - validates base exists and is owned by the active faction;
  - validates the facility exists, is available to that base/faction, is not already built, prerequisites are met, and resources are affordable;
  - deducts resource costs;
  - marks the facility constructed;
  - enforces one build per base per turn;
  - resets build availability on the next turn/round boundary according to the existing turn system.
- Add a minimal visible base panel/build preview path in the strategic UI:
  - selectable starting base or starting-hub surface;
  - visible owned base ID/display key;
  - visible constructed/unbuilt facility state;
  - visible build cost/affordability/prerequisite status;
  - visible action result/failure feedback.
- Seed the current two-faction scenario with a tiny prototype facility catalog:
  - at least one buildable facility for each starting base;
  - at least one unavailable/blocked case covered by validation or tests;
  - placeholder IDs/display keys allowed.
- Add validators/tests for facility definitions, base runtime construction, resource payment, prerequisites, duplicate IDs, missing references, and one-build-per-base-per-turn.
- Preserve current map topology, movement, site interaction, recruitment, tactical handoff, and objective behavior except for the added base construction affordance.

## Out of scope

Not authorized by this story:

- No recurring income chain behavior. Facility definitions may name an `administration` lane, but no per-turn income effect is applied yet.
- No recruitment/dwelling stock refresh or new recruitable unit behavior.
- No active facility effects beyond constructed/unbuilt state, resource cost, prerequisites, and UI feedback.
- No base capture, siege, garrison management, or ownership transfer.
- No full HoMM town tree, upgraded dwellings, marketplace/trading, or Capitol-equivalent economy.
- No map editor UI.
- No procedural map generation.
- No hex/tile/freeform movement rewrite.
- No strategic AI construction planning.
- No final map/base art, icons, VFX, audio, or animation.
- No new victory condition.

## Allowed stubs, mocks, placeholders, or temporary data

- Placeholder facility IDs and localization keys are allowed if scenario-authored/data-driven.
- Prototype facility costs may be simple and low, but must be validated and documented.
- Facility lanes/types may be strings/enums with only inert behavior in this story.
- Facility effects may be represented as inert/deferred metadata only; no income/recruitment effect should run yet.
- Base panel UI may be prototype uGUI/text as long as it is visible and test/evidence-backed.

## Dependencies

- Required prior stories:
  - `STORY-MAP-REAL-001` is DONE / merged and provides authored bases, map nodes, display keys, and validation foundation.
- Required data/assets:
  - Current authored scenario/base definitions in Unity.
- Required architecture decisions:
  - Existing Unity technical scheme, control manifest, testing strategy, and CI build automation.
- Required Unity/package setup:
  - Existing Unity project and Unity Foundation CI.

## Acceptance criteria

- [ ] Base runtime state exists for starting bases with stable base ID, owning faction ID, node ID, constructed facility IDs, and per-turn build availability.
- [ ] Facility definitions are scenario-authored/data-driven with stable ID, display/localization key, lane/type, costs, prerequisites, and base/faction availability.
- [ ] Validation catches duplicate facility IDs, missing display/localization keys, missing base/facility references, invalid prerequisite references, invalid/unsupported resource costs, and facilities assigned to missing bases/factions.
- [ ] A valid owned base can construct an affordable available facility exactly once, deducting the authored resource cost and marking the facility constructed.
- [ ] A second build at the same base in the same turn is rejected clearly without partial mutation.
- [ ] Build availability resets at the appropriate next-turn/round boundary under the existing turn system.
- [ ] Invalid build attempts fail clearly without partial mutation: missing base, non-owned base, unknown facility, already-built facility, unmet prerequisite, unaffordable cost, unavailable base/faction.
- [ ] Starting bases remain uncapturable and no siege/garrison/capture behavior is added.
- [ ] No recurring income or recruitment/dwelling refresh effect is applied by this story.
- [ ] Strategic UI shows a minimal base panel/build preview/action result for at least the current starting base.
- [ ] Current movement, site interaction, recruitment, tactical handoff, and objective smoke behavior still pass.

## Verification requirements

- Unit tests: Required for facility definition validation, build command success/failure, resource deduction, no partial mutation, and one-build-per-base-per-turn.
- Unity edit-mode tests: Required for scenario facility validation and runtime construction service behavior.
- Unity play-mode tests: Required for visible base panel/build affordance and existing strategic loop preservation where practical.
- Integration/data validation tests: Required for invalid facility/base/prerequisite/resource reference cases.
- Manual Unity scene/prefab checks: Supplemental only if needed for base panel layout.
- Screenshot/video evidence: Required PNG or short capture evidence under `production/evidence/STORY-BASE-001/` in the Unity repo showing base panel/build preview and a constructed-facility result or rejection feedback.
- CI evidence: Unity Foundation CI exact-head before merge and post-merge main CI.
- Playtest evidence, if applicable: N/A for this core construction story; QA/playtest closeout occurs later in EPIC-009.
- TDD evidence required? Yes for validation and build command behavior.
- Automation deferred? No broad exception approved; UI-only layout details may use PNG/manual evidence if not practical to assert automatically.

## Ambiguity Check

Status: PASS for READY-candidate.

Open human decision:

- Approve this story as the next EPIC-009 implementation packet, or revise scope before approval.

Assumptions:

- This story should build the construction substrate, not the economy payoff.
- Prototype facility names/costs can be simple placeholders if data-driven and documented.
- One build per base per turn is already locked at the epic level.
- Starting-base capture remains out of scope.

Out of scope:

- Income chain, dwelling refresh, capture/siege, full town tree, editor UI, strategic AI, topology rewrite, and final art.

Allowed stubs/mocks:

- Placeholder facility IDs/localization keys.
- Inert facility lane/effect metadata.
- Prototype text UI.

Human-approved exceptions:

- None yet. Human approval is still pending.

## Branch / PR requirements

- Branch name: `story/STORY-BASE-001-base-definition-and-facility-construction-core`
- PR title: `STORY-BASE-001 Base definition and facility construction core`
- Required linked story ID: `STORY-BASE-001`.
- Required linked GDD/ADR/control docs:
  - `design/gdd/strategic-map.md` §§1-16, especially §12.
  - `design/research/homm-town-building-reference.md`.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: read Unity root `AGENTS.md` plus scoped AGENTS files for all touched Runtime/Domain/Application/Presentation/Tests/Evidence directories.
- Required evidence summary: tests run, validation cases, PlayMode/smoke result, PNG/manual evidence path, CI URL.
- Required omissions section: explicitly list known omissions/stubs/placeholders/deferred work or state `No known omissions`.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked.
- [x] Exact ADR/architecture/control-manifest source is linked.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] UX/content/reference sources are linked.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
- [x] Ambiguity Check status is PASS for READY-candidate.
- [x] Branch / PR / CI traceability requirements are stated.
- [ ] Human approval has been given or delegated gate approval is recorded.

## DONE gate

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, validators, and PlayMode/smoke evidence pass, or human-approved exceptions are documented.
- [ ] No unauthorized design or architecture decisions were introduced.
- [ ] Omissions/stubs/mocks/deferred work are explicitly documented.
- [ ] PR/code review is complete.
- [ ] CI passes or human-approved exceptions are documented.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY-candidate / approval pending. No Unity implementation is authorized until human approval promotes this story to READY / approved.
