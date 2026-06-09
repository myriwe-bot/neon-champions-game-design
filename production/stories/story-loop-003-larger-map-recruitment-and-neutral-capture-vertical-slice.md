---
title: STORY-LOOP-003 Larger Map Recruitment and Neutral Capture Vertical Slice
type: story
status: draft
phase: production
owner: shared
created: 2026-06-09
updated: 2026-06-09
source_lore: []
related:
  [
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat,
    production/stories/story-map-001-larger-two-base-strategic-map-slice,
    production/stories/story-strat-006-simple-recruitment-site-fixed-offer,
    production/stories/story-tac-005-basic-tactical-player-controls,
  ]
approval: pending
---

# Story: STORY-LOOP-003 Larger Map Recruitment and Neutral Capture Vertical Slice

## Status

DRAFT / READY-candidate for human review after Unity PR #22 merged `STORY-STRAT-006` and post-merge main CI passed on 2026-06-09.

This story is not implementation authority until explicitly approved and promoted to READY.

## Story type

Playtest + Integration + UX/Smoke.

## Estimate

- Size: S/M.
- Basis: should mostly compose existing larger-map, recruitment, guarded-site handoff, tactical controls, battle result, and capture behavior into one visible vertical-slice smoke path. Any missing glue must remain narrow.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat.md`.

## User/player/system value

As a designer/player, I want one evidence-backed smoke path that recruits from the larger map and then captures a neutral guarded site, so the current vertical slice can be judged as a connected HoMM-like loop instead of separate feature proofs.

## Source requirements

- `design/gdd/strategic-map.md` §§2, 3, 4, 6, 8, 10, 11, 12, 14.
- `design/gdd/tactical-combat.md` MVP implementation contract sections for minimal board/handoff/player controls already implemented by prior stories.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.
- Parent epic: `EPIC-VSLICE-MVP-002`.

## In scope

- Add or update exactly one PlayMode smoke scenario that exercises the current larger-map vertical slice end to end:
  1. start the deterministic two-base larger-map scenario;
  2. show active faction/controller/Champion/resources and reachable routes;
  3. move to the existing single recruitment site;
  4. preview both fixed recruitment offers;
  5. apply one selected affordable offer;
  6. show resource deduction, new placeholder stack, selected-stock decrement, and readable feedback;
  7. continue to one existing neutral guarded site using existing route/site interaction paths;
  8. launch the existing tactical handoff;
  9. use existing minimal tactical controls to finish the battle;
  10. return a `BattleResult` to the strategic layer and show guarded-site capture/reward feedback.
- Capture screenshot evidence for the connected path: pre-recruit preview, post-recruit state, tactical handoff, post-capture strategic result.
- Add an evidence package under `production/evidence/STORY-LOOP-003/README.md`.
- Fix only narrow integration/readability issues found while composing the existing path, if required for the smoke path to be trustworthy.
- Preserve existing standalone tests for recruitment, guarded-site battle handoff, tactical controls, BattleResult application, central objective interaction, hotseat turn ownership, route movement, and map readability.

## Out of scope

- New recruitment mechanics, more recruitment sites/offers, town/base production, building trees, full economy, dynamic pricing, recurring stock refresh, reserves/caravans/garrisons, faction-specific recruitment economies, final unit/site/base names, final balance, strategic AI, save/load format changes, new tactical mechanics, tactical AI improvements, ability systems, animation/audio/art polish, or campaign victory polish.
- Enemy-faction site contests beyond existing neutral guarded-site capture unless separately approved.
- Reworking map topology, tactical board rules, or recruitment service architecture.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Existing placeholder site, offer, unit, Champion, faction, and localization IDs.
- Existing deterministic tactical smoke shortcuts/control affordances from prior READY stories.
- Minimal smoke-only screenshot labels and evidence helper code.

Not allowed:

- Fake success screenshots that bypass the runtime path.
- Hidden test-only mutation of resources, armies, site ownership, or battle result outside public application/domain paths.
- New final lore/content names.

## Dependencies

- Required prior stories:
  - `STORY-TAC-005` DONE / merged in Unity PR #20.
  - `STORY-MAP-001` DONE / merged in Unity PR #21.
  - `STORY-STRAT-006` DONE / merged in Unity PR #22.
  - Existing tactical handoff/result chain through `STORY-STRAT-004`, `STORY-TAC-002`, `STORY-TAC-003`, `STORY-TAC-VIS-001`, `STORY-TAC-004`, `STORY-STRAT-005`, and `STORY-LOOP-002`.
- Required data/assets:
  - Existing deterministic larger-map fixture and placeholder recruitment/tactical data.
- Required architecture decisions:
  - Current Unity data/runtime/presentation boundaries remain binding.
- Required Unity/package setup:
  - Existing Unity CI and Windows self-hosted runner path.

## Acceptance criteria

- [ ] Given the larger-map scenario starts, the smoke path shows the active faction/controller/Champion/resources and a route to the recruitment site.
- [ ] Given the Champion reaches the recruitment site, both fixed offers are previewed with readable IDs/unit labels/costs/stock/affordability before commitment.
- [ ] Given the selected offer is affordable and in stock, committing it deducts only the selected cost, adds a new placeholder stack to the active Champion army, decrements only selected offer stock, consumes major interaction, and shows readable feedback.
- [ ] Given the recruited Champion continues to a neutral guarded site, existing guarded-site preview/handoff starts a tactical battle without bypassing the battle setup DTO path.
- [ ] Given the tactical battle is resolved through existing minimal player controls, the returned `BattleResult` captures the guarded site and shows readable strategic result feedback.
- [ ] Given this connected smoke is added, existing isolated regression tests for recruitment, guarded-site handoff, BattleResult application, route movement, hotseat ownership, central objective interaction, and tactical controls still pass.
- [ ] Given screenshot evidence is reviewed, the path is legible enough to judge the connected loop at prototype fidelity.
- [ ] CI passes.

## Verification requirements

- Unity EditMode tests: Required only for any new or fixed domain/application edge case found while wiring the smoke; otherwise existing coverage may be referenced.
- Unity PlayMode tests: Required for the connected recruitment-then-neutral-capture smoke path.
- Integration/data validation tests: Existing validators must pass; add targeted validation only if data shape changes are introduced.
- Manual Unity scene/prefab checks: Required only if scene/prefab assets change; prefer no scene/prefab changes.
- Screenshot/video evidence: Required screenshots for preview, successful recruitment, tactical handoff, and post-capture result. Video optional.
- Performance budget: N/A for this small smoke story.
- CI evidence: Required on PR branch and post-merge main.
- Playtest evidence: Lightweight design/playtest note required in evidence README: what the connected path proves and what remains thin.
- TDD evidence required? Yes for any new domain/application behavior or regression fix; PlayMode smoke may be added test-first where feasible.
- Automation deferred? No known exception at draft time.

## Ambiguity Check

Status: FAIL until human approves this as the next READY packet.

Open questions:

- Should this next packet remain a smoke/evidence composition story only, or should it also fix one small usability blocker if the connected path reveals it?

Assumptions:

- Use the existing normal offer for the recruited stack unless human prefers upgraded-offer proof.
- Use an existing neutral guarded site and existing tactical smoke combat path.

Out of scope:

- Full economy/base/town production, deeper tactical combat, strategic AI, save/load, final content/balance, enemy-faction contesting.

Allowed stubs/mocks:

- Existing placeholders from prior stories only.

Human-approved exceptions:

- None.

If this story is approved as the next step, change Ambiguity Check to PASS, `status` to `ready`, and `approval` to `approved` before implementation.

## Branch / PR requirements

- Branch name: `story/STORY-LOOP-003-larger-map-recruitment-neutral-capture-smoke`
- PR title: `STORY-LOOP-003 Larger map recruitment and neutral capture vertical slice`
- Required linked story ID: `STORY-LOOP-003`
- Required linked GDD/ADR/control docs: strategic-map §§2, 3, 4, 6, 8, 10, 11, 12, 14; tactical-combat minimal implementation contract; control-manifest; testing strategy; CI/build automation.
- Required root/scoped AGENTS.md instructions: game-design repo `AGENTS.md`; Unity root/scoped `AGENTS.md` files for touched runtime, presentation, tests, and evidence paths.
- Required evidence summary: connected smoke checklist, tests, screenshot/video status, CI, omissions/stubs, design/playtest note.
- Required omissions section: placeholder content, no production economy/base systems, no tactical mechanics expansion, no final content/balance.

PR must explicitly list known omissions, stubs, mocks, assumptions, deferred work, or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source sections are linked.
- [x] Exact ADR/architecture/control-manifest sources are linked.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] UX/content/art/worldbuilding references are linked if relevant or explicitly N/A.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
- [ ] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [ ] Human approval has been given or delegated gate approval is recorded.

## DONE gate

A story may be marked DONE only when all items are true:

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

DRAFT / READY-candidate. Prepared as the next likely packet, but not yet approved for implementation.
