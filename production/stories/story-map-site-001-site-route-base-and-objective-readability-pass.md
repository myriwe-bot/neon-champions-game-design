---
title: STORY-MAP-SITE-001 Site, Route, Base, and Objective Readability Pass
type: story
status: done
phase: production
owner: shared
created: 2026-06-27
updated: 2026-06-27
source_lore: [greenland, blue-monday, white-sky]
related:
  [
    production/epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction,
    production/stories/story-map-real-001-scenario-authored-strategic-map-shell,
    production/stories/story-base-001-base-definition-and-facility-construction-core,
    production/stories/story-base-002-administration-income-chain-and-recruitment-dwellings,
    design/gdd/strategic-map,
    design/research/homm-like-strategic-map-topology-reference,
    production/planning/strategic-map-realism-brief-2026-06-25,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-MAP-SITE-001 Site, Route, Base, and Objective Readability Pass

## Status

READY / approved. Human approval recorded 2026-06-27 with message: `Approved`. This story is the current authorized EPIC-009 implementation packet.

## Story type

Strategic UI + Playability + Evidence.

## Parent epic

- [EPIC-VSLICE-MVP-009 Strategic Map Geography, Bases, and Facility Construction](../epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction.md)

## User/player/system value

As a player, I want the strategic map to make bases, sites, routes, ownership, objectives, and available actions easier to read at a glance, so that the new base-building/economy layer can be judged in play without mistaking UI clutter for system confusion.

## Source requirements

Exact source references:

- GDD path + section/rule:
  - `design/gdd/strategic-map.md` §§1-11 for MVP strategic loop, site control, resources, recruitment, and map UX/readability expectations.
  - `design/gdd/strategic-map.md` §12 for base/facility presentation context after BASE-001/002.
  - `design/gdd/strategic-map.md` §§13-16 for Champion movement, turn/scenario/victory boundaries, DTO boundaries, and acceptance criteria.
- Research / planning:
  - `design/research/homm-like-strategic-map-topology-reference.md` for graph-backed map readability, site hierarchy, route clarity, and player orientation lessons.
  - `production/planning/strategic-map-realism-brief-2026-06-25.md` for EPIC-009 direction: preserve node-route graph rules while improving map readability and scenario-authored geography.
  - `production/epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction.md` child-story sequence and out-of-scope boundaries.
- ADR / architecture / control-manifest:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

## In scope

Concrete implementation tasks authorized by this story:

- Improve strategic-map readability using existing scenario-authored map/base/site/route/objective data:
  - clearer visual distinction between bases, sites, routes, objective sites, and current Champion position;
  - clearer ownership/faction state for bases and relevant sites;
  - clearer active objective direction and strategic goal text;
  - clearer selected-site/base panel labels and action affordance text;
  - route readability/presentation improvements that do not alter topology or movement rules.
- Add or refine lightweight presentation metadata only if needed and scenario-authored/data-driven.
- Preserve current graph movement, site interaction, recruitment, base construction, income, dwelling recruitment, tactical handoff, and objective rules.
- Add automated coverage where the presentation snapshot can assert labels, categories, ownership, objective markers, selected-site/base information, and available-action text.
- Add PlayMode/evidence PNGs showing the strategic map after the readability pass, including at least one base, one recruitment/dwelling or resource site, route context, and current objective direction.

## Out of scope

Not authorized by this story:

- No new strategic rules, resource economy, facility effects, recruitment mechanics, or balance changes.
- No base capture, siege, garrison management, or ownership transfer.
- No full geography art replacement, final map art, animation, VFX, audio, or icon polish beyond prototype-readable markers/text.
- No map editor UI.
- No procedural map generation.
- No hex/tile/freeform movement rewrite.
- No new sites, objectives, factions, units, victory conditions, or tactical combat changes unless a tiny test fixture is required.
- No strategic AI construction/recruitment planning.

## Allowed stubs, mocks, placeholders, or temporary data

- Prototype colors, text labels, simple markers, line thicknesses, and icon-like shapes are allowed if data-driven or localized in existing presentation conventions.
- Placeholder visual/theme keys are allowed if documented.
- Manual PNG evidence is allowed for visual readability, but automated snapshot/PlayMode assertions must cover non-visual semantic outputs where practical.
- Final art is not required.

## Dependencies

- Required prior stories:
  - `STORY-MAP-REAL-001` DONE / merged.
  - `STORY-BASE-001` DONE / merged.
  - `STORY-BASE-002` DONE / merged.
- Required data/assets:
  - Current authored scenario/base/site/route/facility data in Unity `main` after PR #81.
- Required architecture decisions:
  - Existing Unity technical scheme, control manifest, testing strategy, CI build automation.
- Required Unity/package setup:
  - Existing Unity project and Unity Foundation CI.

## Acceptance criteria

- [ ] Strategic-map presentation clearly distinguishes bases, generic sites, objective-relevant sites, routes, and Champion position using visible prototype-readable text/markers/colors.
- [ ] Base ownership and current active faction context are visible or more clearly represented without adding capture/siege rules.
- [ ] Selected base/site panels show clearer display text, ownership/category, and currently available actions/reasons than the BASE-002 baseline.
- [ ] Objective direction/status remains visible and easier to connect to the map/site context.
- [ ] Route presentation is easier to follow without changing node-route connectivity, route costs, or legal movement behavior.
- [ ] Existing base construction, income feedback, and gated dwelling recruitment still work after the readability pass.
- [ ] Existing site interaction, recruitment, tactical handoff, and objective smoke behavior still pass.
- [ ] No new rule systems, balance changes, capture/siege/garrison behavior, editor UI, topology rewrite, or final art dependency is introduced.
- [ ] Evidence shows before/after or final-state strategic readability for base/site/route/objective context under `production/evidence/STORY-MAP-SITE-001/`.

## Verification requirements

- Unit tests: Required where helper/formatter/presentation-metadata logic is added.
- Unity edit-mode tests: Required for presentation snapshot semantics, labels, ownership/category/objective markers, and preservation of map/base/site data contracts where touched.
- Unity play-mode tests: Required for strategic map smoke preservation and screenshot/evidence capture where current PlayMode framework supports it.
- Integration/data validation tests: Required only if new authored presentation metadata fields are added.
- Manual Unity scene/prefab checks: Supplemental for visual readability and layout.
- Screenshot/video evidence: Required PNG evidence under `production/evidence/STORY-MAP-SITE-001/` showing map readability, base/site/route/objective context, and selected panel/action clarity.
- Performance budget or N/A: N/A; no large map generation or simulation changes.
- CI evidence: Unity Foundation CI exact-head before merge and post-merge main CI.
- Playtest evidence, if applicable: Not required for this implementation story; human playtest/closeout remains a later EPIC-009 QA story.
- TDD evidence required? Yes for presentation-snapshot/formatter/data-contract changes where practical.
- Automation deferred? No broad exception approved; purely visual layout judgment may be covered by PNG/manual evidence in addition to semantic automated assertions.

## Ambiguity Check

Status: PASS. Human approval recorded 2026-06-27.

Open questions:

- None.

Assumptions:

- This story is a readability pass over existing EPIC-009 mechanics, not a new rules story.
- Prototype-readable markers/text are acceptable; final art remains deferred.
- The implementation should prefer adapting current strategic presentation snapshots and PlayMode evidence capture over introducing a new UI framework.

Out of scope:

- New mechanics, capture/siege/garrisons, editor UI, topology rewrite, final art, and strategic AI.

Allowed stubs/mocks:

- Prototype visual markers and labels.
- Placeholder visual/theme keys if data-driven and documented.

Human-approved answers:

- Approved as the next EPIC-009 implementation packet on 2026-06-27.
- Approved assumptions: readability pass over existing EPIC-009 mechanics; prototype-readable markers/text are acceptable; final art remains deferred; prefer adapting current strategic presentation snapshots and PlayMode evidence capture over introducing a new UI framework.

Human-approved exceptions:

- None.

## Branch / PR requirements

- Branch name: `story/STORY-MAP-SITE-001-site-route-base-and-objective-readability-pass`
- PR title: `STORY-MAP-SITE-001 Site, route, base, and objective readability pass`
- Required linked story ID: `STORY-MAP-SITE-001`.
- Required linked GDD/ADR/control docs:
  - `design/gdd/strategic-map.md` §§1-16, especially §§9-12 and §16.
  - `design/research/homm-like-strategic-map-topology-reference.md`.
  - `production/planning/strategic-map-realism-brief-2026-06-25.md`.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: read Unity root `AGENTS.md` plus scoped AGENTS files for all touched Runtime/Application/Presentation/Tests/Evidence paths.
- Required evidence summary: tests run, semantic presentation assertions, PlayMode/smoke result, PNG evidence path, CI URL.
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
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval has been given or delegated gate approval is recorded.

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

READY / approved for Unity implementation. Codex may implement only this story scope and must stop rather than expanding into new mechanics, capture/siege/garrisons, editor UI, topology rewrite, final art, or strategic AI.
