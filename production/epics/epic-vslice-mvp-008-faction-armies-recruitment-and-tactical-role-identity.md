---
title: EPIC-VSLICE-MVP-008 Faction Armies, Recruitment, and Tactical Role Identity
type: epic
status: approved
phase: production
owner: shared
created: 2026-06-18
updated: 2026-06-25
source_lore: [greenland, white-sky, digital-net, qxz-meridian]
related:
  [
    design/gdd/faction-unit-rosters,
    design/gdd/tactical-combat,
    design/gdd/strategic-map,
    design/gdd/intel-resource,
    design/research/homm-like-tactical-battle-ui-reference,
    design/research/homm-like-strategic-map-topology-reference,
    production/stories/story-army-001-mvp-faction-unit-definitions-and-roster-seed,
    production/planning/epic-008-faction-armies-recruitment-and-role-identity-plan,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# Epic: EPIC-VSLICE-MVP-008 Faction Armies, Recruitment, and Tactical Role Identity

## Status

CLOSEOUT REJECTED AGAIN / REPAIR STORY READY. Human `STORY-QA-010` playtest on 2026-06-25 rejected closeout because map camera state, recruitment truthfulness, and tactical drone stack interaction still block judging army composition. `STORY-ARMY-006 Map Camera, Recruitment, and Tactical Stack Interaction Repair` is READY / approved as the current repair packet.

This epic is not direct implementation authority. Agents and Codex may only implement READY child stories.

## Priority tier

Vertical Slice / MVP.

## Phase

Production.

## Owner

Shared.

## Human direction snapshot

Accepted choices:

1. Direction: faction armies + recruitment + tactical roles.
2. First pair: Home Rule Coalition vs QXZ Meridian, with Home Rule treated as a provisional soft-canon game-facing faction name.
3. Unit depth: 3 unit lines per faction; no upgraded variants yet.
4. Tactical complexity: roles plus one readable status/effect; QXZ owns the first Sensor Lock / Marked expression.
5. Recruitment model: fixed offer at starting hubs plus one neutral recruitment site.
6. Story sizing: 4 medium-batched implementation slices + QA closeout.

## Related systems

- Faction unit rosters.
- Tactical unit definitions.
- Tactical role behavior.
- Recruitment/reinforcement.
- Strategic army summary.
- Strategic-to-tactical BattleSetup generation.
- Post-battle result/loss persistence.

## Capability goal

Make the prototype stop feeling like cloned placeholder stacks. By the end of the epic, the player can recruit and field early faction-specific units, see those units behave differently in tactical combat, and understand army composition as a strategic choice.

## Player / design value

This epic turns faction philosophy into playable army composition. Home Rule Coalition and QXZ Meridian should not be different colors of the same soldier stack; they should express rival answers to who owns survival under White Sky:

- Home Rule Coalition: local legitimacy, terrain knowledge, civic defense, rescue, consent, proof.
- QXZ Meridian Arctic Mandate: proprietary climate stability, infrastructure security, sensor/control tech, liability logic.

## Source requirements

- GDDs:
  - `design/gdd/faction-unit-rosters.md` for Greenland faction roster concepts and MVP 3-line roster scale.
  - `design/gdd/tactical-combat.md` §§3-6 for stack-first tactical identity, simple AP, actions, retaliation, range, statuses, and Champion off-board posture.
  - `design/gdd/strategic-map.md` §§2-8 and §§10-13 for two-faction hotseat, recruitment/reinforcement, site interaction, Champion movement, and tactical handoff.
  - `design/gdd/intel-resource.md` for future upgrade/resource hooks; Intel spending is not required in this epic unless a child story explicitly promotes it.
- World / lore bridge:
  - World vault `design-bridges/greenland-faction-unit-rosters.md` for Home Rule Coalition, QXZ Meridian, roster names, and the cultural naming guardrail against using Kalaallit as a faction brand.
- References:
  - `design/research/homm-like-tactical-battle-ui-reference.md` for readable stack battle UI.
  - `design/research/homm-like-strategic-map-topology-reference.md` for recruitment/site/town analogues.
- Architecture / process:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

## MVP roster seed

Home Rule Coalition:

1. **Settlement Watch** — defensive infantry / baseline melee; holds space and retaliates.
2. **Sled Logistics Team** — support/mobility; reinforces the Arctic logistics fantasy without adding deep supply rules yet.
3. **Hunter-Scouts** — recon/skirmisher; local knowledge and target selection.

QXZ Meridian:

1. **Meridian Security** — disciplined infantry / baseline attacker.
2. **Strato Sensor Swarm** — ranged/recon drone; primary Sensor Lock / Marked expression.
3. **Climate Bulwark** — heavy defender; slow, tough, protects infrastructure.

Neutral / shared:

- **Survey Drones** and/or **Site Guards** as simple guarded-site defenders.

## Scope

### In scope

- MVP unit definition schema and data validation.
- Three unit definitions for Home Rule Coalition and three for QXZ Meridian.
- One or two neutral guard definitions.
- Tactical role fields sufficient for melee, ranged, support/recon, and heavy defender behavior.
- One readable status/effect: Sensor Lock / Marked, initially expressed through QXZ sensor units.
- Fixed-offer recruitment from starting hubs plus one neutral recruitment site.
- Strategic army summary showing recruited stacks and faction identity.
- Strategic-to-tactical setup using recruited composition.
- One composition-consequence scenario/site demonstrating that army mix matters.
- Evidence and playtest closeout.

### Out of scope

- Full 6-7 line HoMM roster.
- Upgraded unit variants.
- Full town/dwelling construction tree.
- Full economy, weekly market, or deep resource simulation.
- Full Intel upgrade economy.
- Full Champion progression/assets/operations expansion.
- Strategic AI.
- Full tactical cover/LOS/morale/damage-type taxonomies.
- Final unit art, portraits, animation, VFX, or audio.
- Renaming real Greenlandic identity into faction IP. `Kalaallit` must not be used as a playable faction brand.

### Deferred

- Home Rule final faction naming beyond the approved provisional production name.
- Full faction pages for every Greenland faction.
- Unit upgrades and elite controversial units.
- Intel-powered unit/site upgrades.
- Champion Assets/Operations follow-up epic.

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story | Status | Type | Depends On | Evidence |
| --- | --- | --- | --- | --- |
| [STORY-ARMY-001 MVP Faction Unit Definitions and Roster Seed](../stories/story-army-001-mvp-faction-unit-definitions-and-roster-seed.md) | DONE / merged | Data + Tactical Setup | EPIC-008 approved | Unity PR #60, exact-head CI, post-merge CI, unit-definition tests/evidence |
| [STORY-ARMY-002 Tactical Role Behaviors and Sensor Lock](../stories/story-army-002-tactical-role-behaviors-and-sensor-lock.md) | DONE / merged | Tactical Rules + UI | ARMY-001 DONE | Unity PR #61, exact-head CI, post-merge CI, Sensor Lock/role behavior tests/evidence |
| [STORY-ARMY-003 Fixed Recruitment Offers and Army Summary](../stories/story-army-003-fixed-recruitment-offers-and-army-summary.md) | DONE / merged | Strategic Rules + UI | ARMY-001/002 DONE | Unity PR #64, exact-head CI, post-merge CI, recruit → army update → BattleSetup evidence |
| [STORY-ARMY-004 Composition Consequence Scenario](../stories/story-army-004-composition-consequence-scenario.md) | DONE / merged | Vertical Slice | ARMY-001/002/003 DONE | Unity PR #67, exact-head CI, post-merge CI, before/after recruitment battle evidence, losses/rewards summary |
| [STORY-QA-009 EPIC-008 Playtest and Closeout Review](../stories/story-qa-009-epic-008-playtest-and-closeout-review.md) | DONE / merged; superseded by human playtest rejection | QA + Playability Review | implementation slices DONE | Unity PR #70, exact-head CI, post-merge CI, `CLOSE EPIC` recommendation later rejected by human playtest |
| [STORY-ARMY-005 Army, Recruitment, and Map Readability Repair](../stories/story-army-005-army-recruitment-and-map-readability-repair.md) | DONE / merged | UI + Playability Repair | QA-009 DONE + human playtest rejection | Unity PR #72, exact-head CI, post-merge CI, PNG evidence; pointer cleanup PR #73 |
| [STORY-QA-010 EPIC-008 Repair Playtest and Closeout Review](../stories/story-qa-010-epic-008-repair-playtest-and-closeout-review.md) | DONE / closeout rejected | QA + Human Playtest | ARMY-005 DONE | Human notes: pan/zoom reset, misleading recruitment availability, tactical drones unusable/no stack info |
| [STORY-ARMY-006 Map Camera, Recruitment, and Tactical Stack Interaction Repair](../stories/story-army-006-map-camera-recruitment-and-tactical-stack-interaction-repair.md) | READY / approved | UI + Playability Repair | QA-010 DONE / rejected | Current approved repair packet |

Allowed story statuses: Draft, NEEDS WORK, READY-candidate, READY, IN PROGRESS, REVIEW, DONE, BLOCKED.

## Dependencies

- Upstream epics:
  - EPIC-006 tactical readability/defender agency is complete enough to support role differentiation.
  - EPIC-007 strategic readability/bases/spatial presentation is closed.
- Required GDDs:
  - Faction unit rosters, tactical combat, strategic map.
- Required world canon posture:
  - Home Rule Coalition is soft-canon / game-bridge, not hard canon.
  - QXZ Meridian is reviewed soft-canon in world vault and approved enough for game-facing use.
- Required testing/evidence strategy:
  - Strict layered tests, PlayMode/smoke evidence, PNG evidence where needed, CI.
- Required CI/build automation:
  - Existing Unity Foundation CI.

## Risks

| Risk | Type | Impact | Mitigation / Owner |
| --- | --- | --- | --- |
| Unit definitions become a full roster/balance project | Scope | Epic stalls | Lock to 3 lines per faction, no upgrades / shared |
| Home Rule name is mistaken for hard canon | Lore | Premature canon lock | Mark soft-canon/provisional and avoid Kalaallit as faction brand / shared |
| Sensor Lock becomes hidden or too broad | UX / Rules | Confusing tactical status | Keep one readable effect, explicit event-feed/status text / implementation agent |
| Recruitment expands into town building | Scope | Unbounded systems | Fixed offers only, no construction tree / shared |
| Composition difference is cosmetic | Design | Epic fails player-value goal | Require composition-consequence scenario before closeout / shared |

## Epic readiness gate

- [x] Capability goal is clear.
- [x] Relevant GDD sections exist.
- [x] Relevant technical decisions exist.
- [x] Required test/evidence layers are known.
- [x] Required CI/build checks are known.
- [x] Required agent instruction scopes / AGENTS.md updates are known.
- [x] Scope and out-of-scope are explicit.
- [x] Child stories are identified.
- [x] Dependencies are known.
- [x] Major risks are documented.
- [x] At least one child story passes the Story Readiness Standard. `STORY-ARMY-001` is READY / approved.

## Human playtest rejection — 2026-06-25

Human playtest rejected the previous `CLOSE EPIC` recommendation. Blocking complaints preserved as implementation authority for `STORY-ARMY-005`:

- UI is still hard to read and cluttered.
- Dark top-screen hue hurts objective readability.
- Map cannot be moved/panned, making focus annoying.
- Player cannot see or understand their army, units, stacks, roles, or composition.
- Recruitment/dwellings only say “recruited” and do not explain unit type/count/cost/future dwelling model.
- Tactical roles and stack differences are invisible.

EPIC-008 cannot close until the QA-010 blockers are repaired or explicitly accepted by the human. Current blockers:

- pan/zoom resets after UI button clicks;
- recruitment availability misleads after drone count increases only once;
- tactical drones cannot be selected, moved, or utilized;
- stack info is not shown on tactical click.

## Epic DONE gate

- [ ] Required child stories are DONE or explicitly deferred by human closeout.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, validators, PlayMode/smoke evidence, and manual/PNG evidence are complete or accepted as documented exceptions.
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

## Verdict

CLOSEOUT REJECTED AGAIN. `STORY-QA-010` is DONE with a `REJECT CLOSEOUT` verdict. `STORY-ARMY-006` is READY / approved as the current Unity implementation repair packet.
