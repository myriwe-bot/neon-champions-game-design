---
title: EPIC-VSLICE-MVP-011 Champion Assets and Operations Depth
type: epic
status: approved
phase: production
owner: shared
created: 2026-06-29
updated: 2026-06-30
source_lore: [champions, digital-net, greenland, white-sky]
related:
  [
    design/gdd/game-pillars,
    design/gdd/strategic-map,
    design/gdd/intel-resource,
    design/gdd/tactical-combat,
    design/gdd/tactical-combat/champion-operations-and-progression,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/planning/next-implementation-direction-brief-2026-06-29,
    production/stories/story-champ-ops-001-champion-asset-slot-and-prototype-operation-on-ramp,
    production/stories/story-champ-ops-002-operation-targeting-and-forecast-readability-pass,
    production/stories/story-champ-ops-003-operation-aftermath-and-closeout-readability-smoke,
  ]
approval: approved
---

# Epic: EPIC-VSLICE-MVP-011 Champion Assets and Operations Depth

## Status

APPROVED / IN PROGRESS. Human approval recorded 2026-06-29: "Approved". This approves the next direction recommended in `production/planning/next-implementation-direction-brief-2026-06-29.md`: Champion Assets / Operations depth. `STORY-CHAMP-OPS-001` and `STORY-CHAMP-OPS-002` are DONE / merged; `STORY-CHAMP-OPS-003` is READY / approved for implementation.

This epic is not direct implementation authority. Agents and Codex may only implement READY child stories.

## Priority tier

Vertical Slice / MVP.

## Phase

Production.

## Owner

Shared.

## Capability goal

Make Champions matter on the strategic layer beyond carrying armies and tactical Command: the active Champion should have a visible Asset/Operation surface, one small non-magical prototype Operation, and a clear connection between existing Intel/Command language and strategic force projection.

## Player / design value

The player should start to read Champions as political/operational actors with access, assets, and prepared leverage, not only as stack containers. This slice should create a tiny but visible HoMM-like artifact/spellbook analogue translated into cyberpunk terms.

Relevant pillars:

- [x] Champions as command, identity, and legitimacy.
- [x] Intel as secrets turned into power.
- [x] Infrastructure-first conflict.
- [x] Cyberpunk strategy/RPG.
- [x] HoMM-like exploration, capture, and tactical escalation.
- [ ] Full dirty-information/fog layer.

## Source requirements

- GDDs / design sources:
  - `production/planning/next-implementation-direction-brief-2026-06-29.md` for approved direction and first-slice boundary.
  - `design/gdd/tactical-combat/champion-operations-and-progression.md` §§29-80 for Marshal/Operator, Command, Operations, and Doctrine framing.
  - `design/gdd/tactical-combat/champion-operations-and-progression.md` §§98-198 for finite Command economy, Operation cadence, and channel vocabulary.
  - `design/gdd/intel-resource.md` for existing Intel resource language and first-spend precedent.
  - `design/gdd/strategic-map.md` for current Champion/map/site/HUD boundaries.
  - `design/gdd/game-pillars.md` for Champion, Intel, infrastructure, and cyberpunk strategy pillars.
- ADRs / architecture docs / control-manifest sections:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

Source authority decision: human-approved narrow implementation-source exception for this epic. The Champion Operations split article has draft/pending front matter, but its cited internal sections may be used for this epic's bounded child stories for Champion assets, Command/Operations vocabulary, and one prototype strategic operation only. This does not approve full Champion progression, skill trees, full operation loadouts, Bio/Echo channels, dirty-information systems, or final balance.

## Scope

### In scope

- Minimal Champion Asset/Operation presentation model for the active Champion.
- One prototype Champion Asset slot or command-layer asset surface.
- One small strategic Operation option tied to existing state, shown in current prototype UI.
- A bounded operation cost using existing approved resource/Command/Intel language; no new resource economy.
- A narrow, reversible visible effect suitable for a first on-ramp, such as scouting/forecasting/marking a nearby guarded site, route, or tactical context for the current turn.
- Tests, PlayMode evidence, and exact-head Unity Foundation CI for each READY child story.

### Out of scope

- Full Champion inventory, equipment UI, skill trees, levels, perks, classes, or progression.
- Full Operations spellbook, loadout/preparation UI, cooldown system, reaction windows, or operation cadence implementation beyond the specific child story.
- New resources, new income rules, Intel subtypes, dirty-information/fog-of-war, misinformation, blackmail, public legitimacy, or feed-state systems.
- New strategic map topology, new sites/routes/objectives, new tactical mechanics, new units, new combat rules, AI, or win/loss rules.
- Final art/audio/VFX/icons/portraits/localization/accessibility framework.
- Bio/Echo special channels or faction-locked operation suites.

### Deferred

- Asset rarity/tier/upgrades and dismantling.
- Multiple assets or asset transfer/loss on Champion defeat.
- Operation loadouts and prepared slots.
- Full Intel/dirty-information operation economy.
- Champion progression/secondary skills.

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story | Status | Type | Depends On | Evidence |
| --- | --- | --- | --- | --- |
| [STORY-CHAMP-OPS-001 Champion Asset Slot and Prototype Operation On-Ramp](../stories/story-champ-ops-001-champion-asset-slot-and-prototype-operation-on-ramp.md) | DONE / merged | Strategic UX + Domain/Presentation + PlayMode Evidence | STORY-UX-002 DONE; EPIC-011 approved | Unity PR #108; exact-head CI and post-merge main CI passed |
| [STORY-CHAMP-OPS-002 Operation Targeting and Forecast Readability Pass](../stories/story-champ-ops-002-operation-targeting-and-forecast-readability-pass.md) | DONE / merged | Strategic UX + Domain/Presentation + PlayMode Evidence | STORY-CHAMP-OPS-001 DONE; EPIC-011 approved | Unity PR #111; exact-head CI and post-merge main CI passed |
| [STORY-CHAMP-OPS-003 Operation Aftermath and Closeout Readability Smoke](../stories/story-champ-ops-003-operation-aftermath-and-closeout-readability-smoke.md) | READY / approved | Strategic UX + Integration Smoke + Closeout Recommendation | STORY-CHAMP-OPS-002 DONE; EPIC-011 approved | After-apply/repeat-denied/surrounding-loop evidence required |

Allowed story statuses: Draft, NEEDS WORK, READY-candidate, READY, IN PROGRESS, REVIEW, DONE, BLOCKED.

## Dependencies

- Upstream epics:
  - `EPIC-VSLICE-MVP-004` DONE / closed for Intel resource on-ramp.
  - `EPIC-VSLICE-MVP-005` COMPLETE / human closeout accepted for first Command/Operations on-ramp.
  - `EPIC-VSLICE-MVP-010` DONE / closed plus `STORY-UX-002` DONE / merged for current readability baseline.
- Required technical decisions:
  - Existing Unity technical scheme and control manifest.
- Required testing/evidence strategy:
  - Strict layered tests, PlayMode smoke, PNG evidence, CI.
- Required data/assets:
  - Prototype IDs and text only; no final content names or art.

## Risks

| Risk | Type | Impact | Mitigation / Owner |
| --- | --- | --- | --- |
| Champion Assets expands into full artifact inventory | Scope | Story becomes unmergeable and design-heavy | CHAMP-OPS-001 permits only one visible prototype asset/operation surface / shared |
| Operations become magic/hacking-only | Design | Narrows cyberpunk faction texture | Use broad Command/Operations language; first operation may be scouting/forecast/marking, not a full Signal system / shared |
| Intel use creates new economy rules | Scope | Conflicts with prior Intel placeholder constraints | Use existing resource display/spend precedent only; no new resource type or recurring income / shared |
| UI becomes unreadable again | UX | Player cannot see what Champion operation does | Require PlayMode HUD evidence and small text surface / reviewer |
| Draft source authority blocks Codex | Process | Implementation agent correctly stops | This epic records a narrow source-authority exception; story repeats it explicitly / shared |

## Epic readiness gate

- [x] Capability goal is clear.
- [x] Relevant GDD/reference sections exist, with a narrow human-approved implementation exception.
- [x] Relevant technical decisions exist or are explicitly N/A.
- [x] Required test/evidence layers are known for expected child story types.
- [x] Required CI/build checks are known.
- [x] Scope and out-of-scope are explicit.
- [x] First child story is identified.
- [x] Dependencies are known.
- [x] Major risks are documented.
- [x] At least one child story can pass the Story Readiness Standard.

## Epic DONE gate

- [ ] Required child stories are DONE or explicitly deferred by human closeout.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, validators, PlayMode/smoke evidence, and manual/PNG evidence are complete or accepted as documented exceptions.
- [ ] Unresolved omissions are documented.
- [ ] Docs have been updated in the correct source-of-truth layer.
- [ ] Playtest/QA evidence exists if required.
- [ ] No open blocker remains hidden.

## Verdict

APPROVED / IN PROGRESS. `STORY-CHAMP-OPS-001` and `STORY-CHAMP-OPS-002` are DONE / merged. `STORY-CHAMP-OPS-003` is READY / approved as the next narrow closeout-readiness implementation packet.
