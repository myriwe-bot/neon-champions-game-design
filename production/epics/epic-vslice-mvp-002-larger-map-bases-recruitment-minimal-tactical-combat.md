---
title: EPIC-VSLICE-MVP-002 Larger Map, Bases, Recruitment, and Minimal Tactical Combat
type: epic
status: approved
phase: production
owner: shared
created: 2026-06-04
updated: 2026-06-09
source_lore: []
related:
  [
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    design/gdd/faction-unit-rosters,
    production/epics/epic-strat-mvp-001-strategic-mvp-core-loop,
  ]
approval: approved
---

# Epic: EPIC-VSLICE-MVP-002 Larger Map, Bases, Recruitment, and Minimal Tactical Combat

## Status

Approved / Story Ready. Direction approved by user on 2026-06-04 as option C, tightly scoped: modest larger map + one simple real tactical battle + one recruitment site. `STORY-TAC-005`, `STORY-MAP-001`, and `STORY-STRAT-006` are DONE / merged. `STORY-LOOP-003 Larger Map Recruitment and Neutral Capture Vertical Slice` is READY after explicit human approval on 2026-06-09.

## Priority tier

Vertical Slice / MVP.

## Phase

Production.

## Owner

Shared.

## Related systems

- Strategic Map.
- Tactical Combat.
- Faction Unit Rosters.
- Resources/Intel minimum.
- UI/HUD/readability.

## Capability goal

Enable a small but legible two-faction strategic vertical slice where a player can use bases/cities, move across a larger map, recruit or reinforce through one simple site, reuse the minimal real hex-grid tactical combat foundation, capture a neutral site, and see strategic consequences.

## Player / design value

This epic should move Neon Champions from "strategic systems prototype" toward a recognizable HoMM-like MVP slice: bases, map expansion, neutral-site capture, recruitment pressure, and real tactical escalation.

Relevant pillars:

- [x] Cyberpunk strategy/RPG.
- [x] Infrastructure-first conflict.
- [x] Champions as legitimacy and force projection.
- [ ] Intel as secrets turned into power.
- [ ] Dirty information.
- [x] HoMM-like exploration, capture, and tactical escalation.

## Source requirements

- GDDs:
  - `design/gdd/strategic-map.md` §§6, 8, 10, 11, 12, 13, 14.
  - `design/gdd/tactical-combat.md` §§3-7, with MVP hex-grid decision recorded on 2026-06-04.
  - `design/gdd/faction-unit-rosters.md` for any unit/stack fixtures; if insufficient, child stories must use clearly labeled placeholder units and remain non-final content.
- ADRs / architecture docs / control-manifest sections:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Worldbuilding/lore-facing content:
  - No new final city/base/site names unless separately approved. Placeholder/localization keys only.

## Scope

### In scope

- Modest larger strategic map, not a final campaign map.
- Two starting bases/cities as faction anchors.
- One recruitment/reinforcement site with simple fixed offer/stock/cost rules.
- One or more neutral guarded sites that can be captured.
- Integration with the minimal real hex-grid tactical combat foundation from `EPIC-STRAT-MVP-001`.
- Visible capture/recruitment feedback and evidence-ready smoke path.

### Out of scope

- Full town building trees.
- Full economy or market simulation.
- Full tactical combat system, roster balance, ability catalogue, morale, operations, cover, LOS sophistication, animation, audio, final UI, or final art.
- Strategic AI.
- Online/networking.
- Campaign persistence or final save/load.
- Deep Intel/dirty-information systems.
- Final map/scenario editor.

### Deferred

- Multiple city/base types.
- Multiple recruitment sites and faction-specific recruitment economies.
- Central objective victory polish.
- Enemy-faction site contests beyond the minimum needed for the slice.
- Tactical ability/status/deck/operation depth.

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story                                                                    | Status            | Type                              | Depends On                                   | Evidence                                                   |
| ------------------------------------------------------------------------ | ----------------- | --------------------------------- | -------------------------------------------- | ---------------------------------------------------------- |
| [STORY-TAC-005 Basic Tactical Player Controls](../stories/story-tac-005-basic-tactical-player-controls.md) | DONE / merged | Tactical UI/Input + Integration + UX/Smoke | STORY-LOOP-002, existing minimal tactical domain | Unity PR #20, command tests, PlayMode smoke, screenshot artifact, CI |
| [STORY-MAP-001 Larger Two-Base Strategic Map Slice](../stories/story-map-001-larger-two-base-strategic-map-slice.md) | DONE / merged | Config/Data + Visual/Feel + Strategic Integration | STORY-TAC-005, strategic-map §§2/3/4/6/8/9 | Unity PR #21, map validation, real base/hub site type, central objective interaction, two-choice PlayMode smoke, screenshot/video, CI |
| [STORY-STRAT-006 Simple Recruitment Site and Fixed Offers](../stories/story-strat-006-simple-recruitment-site-fixed-offer.md) | DONE / merged | Logic + UI/Integration + Config/Data | MAP-001, strategic-map §§4/6/8/10/11/12 | Unity PR #22, normal/upgraded offer validation, cost/stock/apply tests, screenshot evidence, CI |
| [STORY-LOOP-003 Larger Map Recruitment and Neutral Capture Vertical Slice](../stories/story-loop-003-larger-map-recruitment-and-neutral-capture-vertical-slice.md) | READY | Playtest + Integration + UX/Smoke | MAP-001, STRAT-006, existing tactical controls | connected recruitment-to-capture smoke, screenshot/video, checklist, CI |

Allowed story statuses: Draft, NEEDS WORK, READY, IN PROGRESS, REVIEW, DONE, BLOCKED.

## Dependencies

- Upstream epics:
  - `EPIC-STRAT-MVP-001` should be closed or have the guarded-site capture loop and minimal tactical combat foundation merged before this epic starts in production.
- Required GDDs:
  - Strategic Map approved sections.
  - Tactical Combat MVP sections; hex-grid decision now recorded.
- Required technical decisions:
  - Existing Unity technical scheme and control manifest.
- Required testing/evidence strategy:
  - TDD for logic, EditMode tests for domain, PlayMode/manual screenshot/video for visible slice.
- Required CI/build automation:
  - Existing Unity CI and design-site CI.
- Required agent instruction scopes / AGENTS.md updates:
  - Unity root and scoped AGENTS.md at implementation time.
- Required data/assets:
  - Placeholder/localized IDs only unless content is separately approved.
- Blocking open questions:
  - Exact child story boundaries need story drafting before READY.
  - Minimal tactical combat rules must stay extremely small; do not import full tactical GDD scope.

## Risks

| Risk                                      | Type                     | Impact                                                                | Mitigation / Owner                                                                                     |
| ----------------------------------------- | ------------------------ | --------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| Tactical combat scope explodes            | Scope                    | Epic becomes a full tactics game before the strategy loop is testable | Limit tactical stories to hex board, stack placement, movement, attack, defeat, result return / shared |
| Larger map becomes content design         | Lore-Cultural-IP / Scope | Agents invent final city/site names or faction content                | Use placeholders/localization keys until content is approved / implementer + reviewer                  |
| Recruitment grows into town-building      | Scope                    | Vertical slice loses focus                                            | One fixed recruitment/reinforcement offer only / shared                                                |
| UI readability regresses                  | UX                       | Demo becomes hard to judge                                            | Require screenshot/video evidence and optional QA packet / reviewer                                    |
| Hex grid decision conflicts with old docs | Design                   | Agents treat square/hex as undecided                                  | Update tactical GDD and cite exact hex decision in stories / shared                                    |

## Epic readiness gate

An epic may enter production only when all items are true:

- [x] Capability goal is clear.
- [x] Relevant GDD sections exist.
- [x] Relevant technical decisions exist or are explicitly N/A.
- [x] Required test/evidence layers are known for expected child story types.
- [x] Required CI/build checks are known for expected child story types, or explicitly N/A with reason.
- [x] Required agent instruction scopes / AGENTS.md updates are known, or explicitly N/A with reason.
- [x] Scope and out-of-scope are explicit.
- [x] Child stories are identified as placeholders.
- [x] Dependencies are known.
- [x] Major risks are documented.
- [x] At least one child story can pass the Story Readiness Standard: `STORY-TAC-005`.

If no child story can become READY, the epic is not production-ready.

## Epic DONE gate

- [ ] All required child stories are DONE.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, validators, PlayMode/smoke evidence, and manual evidence are complete or accepted as documented exceptions.
- [ ] Unresolved omissions are documented.
- [ ] Docs have been updated in the correct source-of-truth layer.
- [ ] Playtest/QA evidence exists if required.
- [ ] No open blocker remains hidden.
- [ ] Human review accepts the epic as complete.

## Anti-pattern check

Invalid epic behavior:

- [ ] This epic authorizes production implementation directly.
- [ ] This epic replaces READY stories.
- [ ] This epic hides ambiguous design decisions.
- [ ] This epic bundles unrelated work for convenience.
- [ ] This epic asks agents to figure out missing details.

If any box above is checked, the epic needs revision.

## Verdict

Approved / Story Ready. `STORY-STRAT-006` is DONE / merged. `STORY-LOOP-003` is the current READY implementation packet; later larger-loop child stories remain placeholders until drafted and approved individually.
