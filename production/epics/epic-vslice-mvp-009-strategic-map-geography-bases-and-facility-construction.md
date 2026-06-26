---
title: EPIC-VSLICE-MVP-009 Strategic Map Geography, Bases, and Facility Construction
type: epic
status: approved
phase: production
owner: shared
created: 2026-06-26
updated: 2026-06-26
source_lore: [greenland, blue-monday, white-sky, digital-net]
related:
  [
    design/gdd/strategic-map,
    design/gdd/faction-unit-rosters,
    design/research/homm-like-strategic-map-topology-reference,
    design/research/homm-town-building-reference,
    production/planning/strategic-map-realism-brief-2026-06-25,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# Epic: EPIC-VSLICE-MVP-009 Strategic Map Geography, Bases, and Facility Construction

## Status

APPROVED / PLANNED. Human direction recorded 2026-06-26: proceed from EPIC-008 closeout into strategic-map geography/readability plus bases and simple resource-costed facility construction. This epic is a capability container only. Agents and Codex may not implement the epic directly; only READY child stories authorize implementation.

First child story DONE / merged: `STORY-MAP-REAL-001 Scenario-Authored Strategic Map Shell`. Next child story READY / approved: `STORY-BASE-001 Base Definition and Facility Construction Core`.

## Priority tier

Vertical Slice / MVP.

## Phase

Production.

## Owner

Shared.

## Human direction snapshot

Accepted choices:

1. Direction: strategic map geography/readability plus bases and simple buildings/facilities.
2. Rules posture: preserve current node-route graph rules; improve presentation and scenario-authored map data.
3. Geography/naming posture: agnostic/editor-friendly. Base, town, site, node, and map labels are scenario-authored data/localization keys, not hardcoded canon.
4. Story size: medium-batched.
5. Base facility model: simple build/upgrade during scenario with resource costs.
6. Facility construction timing: one build per base per turn.
7. Base capture: starting bases are not capturable in this epic.
8. Future map editor posture: data fields plus validation now; no editor UI.
9. Income chain size: three levels total — basic, mid, high.
10. Recruitment/dwelling scope: one to two specific dwelling/facility offers per faction.

## Related systems

- Strategic map topology and presentation.
- Scenario-authored map/base/site data.
- Bases / starting hubs.
- Base facilities and simple construction.
- Resource income and spending.
- Recruitment/dwelling offers.
- Strategic UI/HUD.
- Strategic-to-tactical battle setup/result flow.

## Capability goal

Make the strategic layer feel like a scenario-authored operational map with meaningful bases, routes, sites, and simple base-building choices, while preserving the current graph-based movement rules and avoiding a full town/economy rewrite.

## Player / design value

The player should understand bases as owned operational anchors, spend resources on small facility choices, see those choices affect income/recruitment pressure, and still play the existing recruit -> move -> fight -> objective loop on a clearer authored map.

Relevant pillars:

- [x] Cyberpunk strategy/RPG.
- [x] Infrastructure-first conflict.
- [x] HoMM-like exploration, capture, town/base growth, and tactical escalation.
- [x] Champions as legitimacy and force projection.
- [x] Intel as secrets turned into power, where future Sensor/Intel facilities can hook in.
- [ ] Full dirty information/fog layer.

## Source requirements

- GDDs:
  - `design/gdd/strategic-map.md` §§1-11 for MVP direction, scenario shape, topology, sites, resources, recruitment, and graph-backed map rules.
  - `design/gdd/strategic-map.md` §12 for base facilities and simple construction.
  - `design/gdd/strategic-map.md` §§13-16 for Champion movement, turn/scenario/victory, DTO boundaries, and acceptance criteria.
  - `design/gdd/faction-unit-rosters.md` for current Home Rule Coalition / QXZ unit definitions usable by recruitment offers.
- Research:
  - `design/research/homm-like-strategic-map-topology-reference.md` for HoMM-like map/site/topology lessons.
  - `design/research/homm-town-building-reference.md` for Heroes 3 and Olden Era town/building/dwelling reference.
- Planning:
  - `production/planning/strategic-map-realism-brief-2026-06-25.md` for recorded EPIC-009 planning decisions.
- Architecture / process:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

## Scope

### In scope

- Scenario-authored strategic map shell over current node-route graph rules.
- Data-driven map/base/site/node display names and localization/display keys.
- Presentation positions/layout fields for nodes, bases, sites, routes, and map regions/background.
- Validation for scenario-authored map/base/site data.
- Simple base definitions attached to strategic nodes.
- Base facility definitions with resource costs, prerequisites, effects, and serialized runtime state.
- One build per base per turn.
- Three-level administration/income chain.
- One to two faction-specific recruitment/dwelling offers per faction.
- Clear map/base/site/route readability pass.
- Base-building scenario smoke proving build -> income/recruitment -> movement -> battle -> objective pressure.
- QA/playtest closeout.

### Out of scope

- Full hex/tile/freeform movement rewrite.
- Actual map editor UI.
- Procedural map generation.
- Full Heroes-style town tree.
- Full seven-tier dwelling model.
- Upgraded unit dwellings.
- Marketplace/resource trading.
- Starting-base capture/siege.
- Full garrison management.
- Strategic AI construction planning.
- Full fog, weather, logistics, supply, or dirty-information layer.
- Final map art, final icons, VFX, audio, or animation.

### Deferred

- Capturable bases and siege rules.
- Full town/base building tree.
- Multiple-base economies beyond the first scenario need.
- External dwellings with accumulated growth.
- Full map editor UX.
- Strategic AI.
- Intel/Operations facility expansion beyond tiny hooks.

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story | Status | Type | Depends On | Evidence |
| --- | --- | --- | --- | --- |
| [STORY-MAP-REAL-001 Scenario-Authored Strategic Map Shell](../stories/story-map-real-001-scenario-authored-strategic-map-shell.md) | DONE / merged PR #79 | Data + Presentation + Validation | EPIC-009 approved | Complete: validators/tests, PlayMode evidence, PNG evidence, post-merge CI |
| [STORY-BASE-001 Base Definition and Facility Construction Core](../stories/story-base-001-base-definition-and-facility-construction-core.md) | READY / approved | Strategic Rules + UI | MAP-REAL-001 DONE | Required: facility validation, build-command tests, base panel evidence |
| STORY-BASE-002 Administration Income Chain and Recruitment Dwellings | Draft target | Economy + Recruitment | BASE-001 DONE | Required: income/recruitment tests and scenario evidence |
| STORY-MAP-SITE-001 Site, Route, Base, and Objective Readability Pass | Draft target | Strategic UI + Playability | MAP-REAL-001 and BASE-001/002 as needed | Required: map readability evidence |
| STORY-BASE-LOOP-001 Base-Building Scenario Smoke | Draft target | Vertical Slice Smoke | Prior EPIC-009 implementation stories DONE | Required: connected loop evidence |
| STORY-QA-012 EPIC-009 Playtest and Closeout Review | Draft target | QA + Playability Review | EPIC-009 implementation stories DONE | Required: QA/playtest verdict |

Allowed story statuses: Draft, NEEDS WORK, READY-candidate, READY, IN PROGRESS, REVIEW, DONE, BLOCKED.

## Dependencies

- Upstream epics:
  - EPIC-008 is DONE / closed.
  - EPIC-007 strategic map readability/bases/spatial presentation is DONE / closed and provides the predecessor map-presentation baseline.
- Required GDDs:
  - Strategic Map GDD, especially §12 for base facilities.
- Required technical decisions:
  - Existing Unity technical scheme and control manifest.
- Required testing/evidence strategy:
  - Strict layered tests, validators, PlayMode/smoke evidence, PNG/manual evidence where needed, CI.
- Required CI/build automation:
  - Existing Unity Foundation CI.
- Required agent instruction scopes / AGENTS.md updates:
  - Unity root and scoped AGENTS.md at implementation time.
- Required data/assets:
  - Prototype text/markers/icons are allowed; final art is not required.
- Blocking open questions:
  - None for epic approval. Exact facility names, costs, and offer values are story-scoped unless a story cannot pass ambiguity check.

## Risks

| Risk | Type | Impact | Mitigation / Owner |
| --- | --- | --- | --- |
| Base facilities become a full HoMM town tree | Scope | Epic stalls | Lock to 3-level income chain, 1-2 recruitment offers per faction, no upgraded dwellings / shared |
| Map shell hardcodes current prototype names | Technical / Content | Future editor and scenario authoring blocked | First story requires data/localization keys and validation / implementation agent |
| Building mechanics land before map/base data is clean | Technical | Hardcoded one-off base system | Start with MAP-REAL-001 data shell before BASE-001 / shared |
| Economy values dominate design before fun is proven | Balance | False precision and rework | Use prototype values; require tests/evidence, not final balance / shared |
| Geography becomes hard-canon too early | Lore | Overcommits map names/places | Scenario-authored labels; agnostic map authoring; no hardcoded town names / shared |

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
- [x] At least one child story has merged. `STORY-MAP-REAL-001` is DONE / merged; `STORY-BASE-001` is READY / approved.

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

APPROVED / PLANNED. `STORY-MAP-REAL-001` is DONE / merged; `STORY-BASE-001` is READY / approved as the current Unity implementation packet.
