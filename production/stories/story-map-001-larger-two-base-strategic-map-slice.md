---
title: STORY-MAP-001 Larger Two-Base Strategic Map Slice
type: story
status: ready
phase: production
owner: shared
created: 2026-06-05
updated: 2026-06-08
source_lore: []
related:
  [
    design/gdd/strategic-map,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat,
    production/stories/story-tac-005-basic-tactical-player-controls,
  ]
approval: approved
---

# Story: STORY-MAP-001 Larger Two-Base Strategic Map Slice

## Status

READY implementation packet after `STORY-TAC-005` merged in Unity PR #20. Ambiguity questions were resolved by user direction on 2026-06-05; explicit implementation approval recorded on 2026-06-08.

## Story type

Config/Data + Visual/Feel + Strategic Integration.

## Estimate

- Size: M.
- Basis: expands the existing small strategic graph and presentation without adding recruitment, bases-as-systems, strategic AI, economy depth, or final content naming.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-002-larger-map-bases-recruitment-minimal-tactical-combat.md`.

## User/player/system value

As a player/designer, I want the prototype to move from a tiny guarded-site lane into a modest two-faction map with visible starting anchors and multiple neutral choices, so that the next vertical slice can test HoMM-like route planning before recruitment and base loops are added.

## Source requirements

- `design/gdd/strategic-map.md` §2 Approved MVP Direction.
- `design/gdd/strategic-map.md` §3 First Scenario Shape.
- `design/gdd/strategic-map.md` §4 MVP In Scope.
- `design/gdd/strategic-map.md` §6 Core Loop Contract.
- `design/gdd/strategic-map.md` §8 UX / Readability Requirements Draft.
- `design/gdd/strategic-map.md` §9 Strategic Map Topology.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.

## In scope

- Replace or extend the current minimal strategic graph into a modest two-faction test map with:
  - two visible real hub/base site nodes, one per faction;
  - one Champion per faction placed at the correct starting anchor;
  - 6-10 total strategic nodes;
  - multiple route choices between starts and neutral sites;
  - at least two guarded neutral sites that reuse the existing guarded-site tactical handoff path;
  - one clearly marked central/high-value objective site with a minimal non-victory interaction.
- Use stable placeholder IDs/localization keys only; no final city, faction, base, or site names.
- Preserve current hotseat turn ownership, route movement, site interaction, guarded battle trigger, player-driven tactical controls, BattleResult return, and site-control application.
- Update strategic presentation/HUD enough that the larger map is readable: active faction/champion, reachable routes/sites, owned/neutral/guarded states, and recent capture/result feedback.
- Implement base/hub as a real site type in the data/domain model at the minimum needed for ownership, placement, and UI/state display; do not add recruitment, production, construction, or economy behavior in this story.
- Keep map data deterministic and serializable through the current domain/runtime structures.
- Add evidence package under `production/evidence/STORY-MAP-001/README.md`.

## Out of scope

- Recruitment/reinforcement rules, stock, costs, base production, town buildings, market/economy depth, victory-condition completion, strategic AI, enemy Champion tactical contests, final map art, final names, save/load format, map editor, fog/intel systems, route blocking/weather/logistics, and tactical mechanics beyond what already exists.
- Any base/hub behavior beyond minimal real site typing, ownership display, starting placement, and stable interaction/readability hooks.
- Adding new final data-authoring architecture or replacing the approved graph topology model.

## Allowed stubs, mocks, placeholders, or temporary data

Allowed:

- Placeholder node/site/base/objective labels and localization keys.
- Placeholder central objective interaction with no final victory rule yet.
- Simple fixed route costs if current movement code needs them.
- Reuse of existing minimal guarded-site fixtures and tactical battle setup.

Not allowed:

- Final lore names or final balance values.
- Hidden deterministic auto-capture that bypasses existing tactical handoff where a guarded site is in scope.
- Implementing recruitment/base systems inside this map story.
- Treating base/hub as only a visual label; it must be a real minimal site type.

## Dependencies

- Required prior stories:
  - `STORY-TAC-005` DONE / merged in Unity PR #20.
  - Existing strategic map graph, hotseat turn, route input, guarded-site battle trigger, tactical handoff, BattleResult application, visible loop, and basic tactical controls must remain on Unity `main`.
- Required data/assets:
  - Placeholder-only map/site/base/objective IDs are sufficient.
- Required architecture decisions:
  - Strategic-map §9 graph topology remains binding.
  - Current Unity data/runtime/presentation boundaries remain binding.
- Required Unity/package setup:
  - Existing Unity CI and self-hosted Windows runner path.

## Acceptance criteria

- [ ] Given a new scenario starts, both factions have visible starting hub/base sites and one Champion each at their own start.
- [ ] Given the strategic map is displayed, 6-10 total nodes and their route choices are visible/readable enough for screenshot review.
- [ ] Given the active Champion selects routes/sites, reachable destinations and ownership/guarded states are clear before committing movement or interaction.
- [ ] Given the active Champion reaches a guarded neutral site, the existing tactical handoff launches and the player can resolve the fight using the STORY-TAC-005 controls.
- [ ] Given the player wins the guarded fight, the real `BattleResult` returns and the correct site becomes controlled without corrupting other sites or faction ownership.
- [ ] Given the map has two starting bases and multiple neutral choices, existing hotseat turn ownership and route movement remain deterministic across turns.
- [ ] Given a Champion reaches the central objective site, the player can perform a minimal non-victory interaction and receives readable state/feedback without ending the scenario.
- [ ] Given base/hub nodes exist, they are represented as a real minimal site type in data/domain state and presentation, not only as visual labels.
- [ ] Given two possible guarded neutral choices exist, PlayMode smoke proves both are reachable/legible and that guarded-site tactical handoff remains valid from the larger map.
- [ ] Given placeholder map/base/site/objective labels are used, they are explicitly documented as non-final and stable enough for tests/evidence.
- [ ] CI passes.

## Verification requirements

- Unity EditMode tests: Required for map definition validation, real base/hub site typing, starting base/champion placement, central objective minimal interaction, route connectivity/reachability, guarded-site preservation, and no unintended ownership corruption after BattleResult application.
- Unity PlayMode tests: Required for visible larger-map smoke covering route selection/readability, both possible guarded neutral choices, and at least one guarded-site capture on the larger map.
- Integration/data validation tests: Required if new map fixture/schema validation is added.
- Manual Unity scene/prefab checks: Required if presentation wiring or scene layout changes.
- Screenshot/video evidence: Required for larger-map readability and post-capture state.
- CI evidence: Required.
- TDD evidence required? Yes for new map/state validation and regression fixes.
- Automation deferred? No known exception at draft time.

## Ambiguity Check

Status: PASS.

Resolved user decisions, 2026-06-05:

- Central objective: include at least a minimal non-victory interaction; do not leave it purely visual.
- Base/hub: implement as a real minimal site type now, not only a labeled starting anchor.
- Guarded neutral choices: PlayMode smoke should prove two possible neutral choices.

Assumptions:

- The next safe step is map expansion plus minimal site typing/interaction only; recruitment/base mechanics remain a later story.
- Placeholder labels are acceptable if clearly non-final.

Out of scope:

- Recruitment, base production, strategic AI, final content naming, and full victory rules.

Allowed stubs/mocks:

- Placeholder labels, minimal central objective interaction, real minimal base/hub site type, and fixed map fixture data.

Human-approved exceptions:

- User explicitly approved the central objective as minimal non-victory interaction, base/hub as a real site type, and two possible neutral choices in PlayMode smoke on 2026-06-05.

## Branch / PR requirements

- Branch name: `story/STORY-MAP-001-larger-two-base-strategic-map-slice`
- PR title: `STORY-MAP-001 Larger two-base strategic map slice`
- Required linked story ID: `STORY-MAP-001`
- Required linked GDD/ADR/control docs: strategic-map §§2, 3, 4, 6, 8, 9; control-manifest; testing strategy; CI/build automation.
- Required root/scoped AGENTS.md instructions: game-design repo `AGENTS.md`; Unity root/scoped `AGENTS.md` files for touched runtime, presentation, tests, and evidence paths.
- Required evidence summary: map checklist, tests, screenshot/video status, CI, omissions/stubs.
- Required omissions section: placeholder map/site/base/objective labels, no recruitment/base mechanics beyond minimal real base/hub site type, no final victory rule unless separately approved.

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
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval has been given or delegated gate approval is recorded on 2026-06-08.

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

READY. Human implementation approval recorded on 2026-06-08. No known story-readiness blockers; implement exactly this story scope.
