---
title: STORY-TERRAIN-001 Strategic Terrain Tags and Tactical Layout Family Contract
type: story
status: ready
phase: production
owner: shared
created: 2026-06-27
updated: 2026-06-27
source_lore: [greenland, white-sky, digital-net]
related:
  [
    production/epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    design/gdd/tactical-combat/statuses-terrain-and-objectives,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-TERRAIN-001 Strategic Terrain Tags and Tactical Layout Family Contract

## Status

READY / approved for Unity implementation. Human approval recorded 2026-06-27: "Excellent, now prepare first story for implementation, approved". This approves the listed scope, assumptions, exclusions, allowed placeholders, branch/PR requirements, and verification requirements as written.

## Story type

Data + Contract + Validation.

## Parent epic

- [EPIC-VSLICE-MVP-010 Terrain, Tactical Battlefields, and Map-Space Readability](../epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability.md)

## User/player/system value

As a designer and player, I want strategic map places to carry readable terrain/context tags that select tactical layout families, so that future tactical battles can feel tied to where they occur without adding strategic movement terrain rules yet.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §9 for approved node-route graph topology and the rule that graph rules remain separate from visual terrain.
  - `design/gdd/strategic-map.md` §9.5 for EPIC-010 strategic terrain/context contract.
  - `design/gdd/strategic-map.md` §10 for site mechanical categories and infrastructure/theme types.
  - `design/gdd/tactical-combat.md` §§3-6 for tactical principles, MVP scope, flat hex board, strategic battle context, and deployment.
  - `design/gdd/tactical-combat.md` §6.2A for EPIC-010 tactical battlefield/layout family contract.
  - `design/gdd/tactical-combat/statuses-terrain-and-objectives.md` §Terrain Hazards is reference only; hazards are not authorized by this story.
- Parent epic:
  - `production/epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability.md`.
- ADR / architecture / control-manifest:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

## In scope

Concrete implementation tasks authorized by this READY story:

- Add or formalize strategic terrain/context metadata in scenario-authored map data for map regions, sites, nodes, and/or routes where current architecture supports it.
- Define stable terrain/context tag IDs suitable for prototype use, such as:
  - `urban_ruins`;
  - `corporate_facility_zone`;
  - `glacier_road`;
  - `data_center_perimeter`;
  - `white_sky_exposed_plain`;
  - `base_outskirts`;
  - `infrastructure_hub`.
- Define tactical layout family IDs selected from strategic battle context, such as:
  - `server_yard` for data-cache / data-center encounters;
  - `fortified_approach` for base-adjacent encounters;
  - `open_route_clash` for route/open-field clashes;
  - `infrastructure_hub` for central objective fights.
- Add a data-driven mapping from strategic context to tactical layout family without hardcoded one-off switch logic in presentation code.
- Preserve current node-route strategic movement rules, route costs, Champion placement, site interaction, recruitment, tactical handoff, objective behavior, and base/facility behavior.
- Add validation for terrain/context tags and layout-family references, including missing/unknown IDs and invalid mappings where current data model can validate them.
- Surface selected terrain/context and tactical layout family in debug/evidence output or existing battle setup DTO evidence so later stories can consume it.
- Add tests and evidence proving the current scenario can select at least two different tactical layout families from authored strategic context.

## Out of scope

Not authorized by this story:

- No tactical board cell terrain implementation yet; `STORY-TERRAIN-002/003` own authored layout cells, deployment zones, blockers, and cover/defensive cells.
- No strategic terrain movement costs, route movement modifiers, supply/logistics, weather, fog, stealth, scouting uncertainty, or strategic AI terrain valuation.
- No strategic topology rewrite, tile/hex/freeform movement, route generation, procedural map generation, or map editor UI.
- No tactical cover/defense combat modifier yet unless it already exists and is only referenced inertly.
- No new unit abilities, Champion Commands/Operations, hazards, objectives, resources, factions, units, sites, base facilities, victory rules, or balance changes.
- No final art, icons, animation, VFX, audio, or localization pass.

## Allowed stubs, mocks, placeholders, or temporary data

- Prototype terrain/context tag IDs and display strings are allowed if data-driven and documented as provisional.
- Prototype tactical layout family IDs are allowed without implementing their final layout contents.
- Existing strategic map labels and site/theme metadata may be reused as inputs to terrain/context mapping.
- Debug/evidence-only display of selected layout family is allowed if production UI is not ready.
- Final art assets are not required.

## Dependencies

- Required prior stories:
  - EPIC-009 is DONE / closed.
  - EPIC-006 tactical readability/defender-agency implementation stories are DONE / merged.
- Required data/assets:
  - Existing scenario-authored map/site/base/route data from EPIC-009.
  - Existing battle setup / tactical handoff DTOs.
- Required architecture decisions:
  - Existing Unity technical scheme, control manifest, testing strategy, and CI build automation.
- Required Unity/package setup:
  - Existing Unity project and Unity Foundation CI.

## Acceptance criteria

- [ ] Scenario-authored strategic map data can express terrain/context tags for relevant current map regions, sites, nodes, and/or routes without changing graph topology.
- [ ] Battle setup or equivalent handoff data can carry a tactical layout family ID derived from strategic battle context.
- [ ] At least two current scenario contexts select distinct layout families from authored data, for example data-cache/server-yard and base-outskirts/fortified-approach or route/open-route clash.
- [ ] Unknown terrain/context tag IDs and unknown layout family IDs fail validation clearly instead of silently falling back to hardcoded defaults.
- [ ] Current strategic movement remains node-route based; no strategic terrain movement costs or topology changes are introduced.
- [ ] Existing site interaction, recruitment, base/facility behavior, objective flow, tactical battle handoff, and result return are not intentionally changed.
- [ ] Evidence shows selected strategic terrain/context and layout family for at least two battle contexts.
- [ ] The implementation leaves a clean extension point for later authored tactical layout definitions and deployment zones.

## Verification requirements

- Unit tests: Required for terrain/context tag validation, layout-family mapping, and fallback/error behavior.
- Unity edit-mode tests: Required where scenario data or battle setup definitions are loaded/validated in Unity.
- Unity play-mode tests: Required if current architecture can smoke a battle setup/handoff with selected layout family.
- Integration/data validation tests: Required for unknown tag/family IDs and at least two valid context-to-family cases.
- Manual Unity scene/prefab checks: Supplemental only if selected context/family evidence cannot be fully asserted automatically.
- Screenshot/video evidence: Required PNG or text evidence under `production/evidence/STORY-TERRAIN-001/` in the Unity repo showing or recording selected context/family outputs.
- Performance budget or N/A: N/A; data/contract story with no heavy generation.
- CI evidence: Unity Foundation CI exact-head before merge and post-merge main CI before marking DONE.
- Playtest evidence, if applicable: N/A; EPIC-010 playtest closeout occurs later.
- TDD evidence required? Yes for validators and mapping behavior.
- Automation deferred? No broad exception approved; UI-only evidence may be manual/PNG if not practical to assert automatically.

## Ambiguity Check

Status: PASS. Human implementation approval recorded 2026-06-27.

Open questions:

- None blocking READY implementation. Exact final tag names and layout family IDs may be adjusted during implementation only if they remain prototype, data-driven, documented, and do not add gameplay rules.

Assumptions:

- The implementation should prefer adapting existing scenario/site/theme/battle setup data over a broad architecture rewrite.
- Terrain/context tags are not hard canon geography; they are scenario-authored prototype metadata.
- This story creates the bridge, not the tactical terrain board itself.

Out of scope:

- Strategic terrain movement rules, tactical terrain cells, cover modifiers, hazards, fog, weather, supply, topology rewrite, and final art.

Allowed stubs/mocks:

- Prototype tag IDs, display strings, and layout family IDs.
- Debug/evidence-only family display.

Human-approved answers:

1. Promote `STORY-TERRAIN-001` for implementation.
2. Keep the approved EPIC-010 boundary: strategic terrain identity/layout-family bridge now; no strategic movement terrain rules, tactical terrain cells, hazards, fog, weather, supply, topology rewrite, or final art.
3. Use the story's listed assumptions, exclusions, allowed placeholders, branch/PR requirements, and verification requirements as the implementation contract.

Approved source-authority note:

- `design/gdd/tactical-combat/statuses-terrain-and-objectives.md` remains `draft` / `pending` and is reference-only for terrain terminology and future hazard context. It is not binding implementation authority for this story; hazards and tactical terrain cells remain out of scope.

Human-approved exceptions:

- None.

## Branch / PR requirements

- Branch name: `story/STORY-TERRAIN-001-strategic-terrain-tags-layout-family-contract`
- PR title: `STORY-TERRAIN-001 Strategic terrain tags and tactical layout family contract`
- Required linked story ID: `STORY-TERRAIN-001`.
- Required linked GDD/ADR/control docs:
  - `design/gdd/strategic-map.md` §§9, 9.5, 10.
  - `design/gdd/tactical-combat.md` §§3-6 and §6.2A.
  - `production/epics/epic-vslice-mvp-010-terrain-tactical-battlefields-and-map-space-readability.md`.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: read Unity root `AGENTS.md` plus scoped AGENTS files for all touched Runtime/Domain/Application/Presentation/Tests/Evidence directories.
- Required evidence summary: tests run, validation cases, at least two selected layout family contexts, evidence path, CI URL.
- Required omissions section: explicitly list known omissions/stubs/placeholders/deferred work or state `No known omissions`.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked.
- [x] Exact ADR/architecture/control-manifest source is linked.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] UX/content/reference sources are linked if relevant.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human implementation approval has been given and recorded.

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

READY / approved for Unity implementation. Runnable Codex prompt prepared at `production/sprints/codex-story-terrain-001.prompt.txt`.
