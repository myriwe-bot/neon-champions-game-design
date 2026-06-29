---
title: EPIC-VSLICE-MVP-010 Terrain, Tactical Battlefields, and Map-Space Readability
type: epic
status: approved / in-progress
phase: production
owner: shared
created: 2026-06-27
updated: 2026-06-29
source_lore: [greenland, white-sky, digital-net]
related:
  [
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    design/gdd/tactical-combat/statuses-terrain-and-objectives,
    production/planning/next-implementation-direction-brief-2026-06-27,
    production/stories/story-terrain-001-strategic-terrain-tags-and-tactical-layout-family-contract,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# Epic: EPIC-VSLICE-MVP-010 Terrain, Tactical Battlefields, and Map-Space Readability

## Status

APPROVED / IMPLEMENTATION COMPLETE; AWAITING QA CLOSEOUT APPROVAL. `STORY-TERRAIN-001` through `STORY-TERRAIN-005` are DONE / merged. No current READY / approved Unity implementation packet is active. Next recommended packet is `STORY-QA-013 EPIC-010 Playtest and Closeout Review` as READY-candidate / approval pending.

## Priority tier

Vertical Slice / MVP.

## Phase

Production.

## Owner

Shared.

## Human direction snapshot

Accepted choices:

1. Direction: terrain, tactical battlefields, and map-space readability.
2. Include strategic-map terrain identity because terrain is already being introduced, but keep strategic terrain mostly presentation/data for this epic.
3. Tactical terrain gets the first real gameplay mechanics: authored layout families, deployment zones, blockers, simple cover/defensive cells, and readability.
4. Strategic terrain movement costs, supply/logistics, weather, fog/stealth, strategic AI terrain valuation, and topology rewrites are explicitly out of scope.
5. First story should create the shared data/schema bridge: strategic terrain tags and tactical layout family contract.

## Related systems

- Strategic map topology and presentation.
- Scenario-authored map/site/region data.
- Tactical combat board layout and deployment.
- Tactical terrain cells, blockers, cover/defensive cells, and objective-adjacent cells.
- Strategic-to-tactical battle setup / context handoff.
- UX/readability and evidence capture.

## Capability goal

Make terrain a shared language across strategic and tactical play: the strategic map communicates region/site terrain identity and battle context, while tactical battles become readable authored spaces with deployment zones and simple terrain features that affect positioning.

## Player / design value

The player should feel that a fight at a data cache, base outskirts, open route, or central infrastructure hub happens in a different kind of place. Strategic terrain should help the player anticipate battle context; tactical terrain should make movement, range, role choice, and positioning matter without adding full XCOM-style simulation.

Relevant pillars:

- [x] Cyberpunk strategy/RPG.
- [x] Infrastructure-first conflict.
- [x] HoMM-like exploration, capture, and tactical escalation.
- [x] Factions as tactical philosophies once roster roles meet terrain.
- [x] Champions as command and force projection, because later Commands/Operations can target terrain/context.
- [ ] Full dirty information/fog layer.

## Source requirements

- GDDs:
  - `design/gdd/strategic-map.md` §§1-10 for MVP direction, graph-backed map rules, site/theme types, and the new terrain/context contract.
  - `design/gdd/tactical-combat.md` §§1-6 for tactical-combat scope, flat hex board, deployment, and the new tactical terrain contract.
  - `design/gdd/tactical-combat/statuses-terrain-and-objectives.md` for existing terrain hazard/objective notes; this epic does not automatically authorize hazards.
- Prior epic state:
  - EPIC-009 is DONE / closed and provides scenario-authored strategic map, bases, sites, routes, and facilities.
  - EPIC-006 tactical readability/defender agency implementation stories are DONE / merged, providing tactical labels, event feed, affordances, AP/Defend, unit data, and neutral guard CombatAI.
- Architecture / process:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

## Scope

### In scope

- Strategic terrain identity/presentation tags for map regions, sites, nodes, and/or routes where current authored map data supports them.
- Tactical layout family selection from strategic battle context.
- Data-driven mapping from strategic terrain/site context to tactical layout family IDs.
- Authored tactical layout definitions with deployment zones.
- Tactical terrain cells such as open, blocked/obstacle, defensive/cover, objective-adjacent, and deployment.
- Movement/attack affordances respecting blockers and deployment zones.
- Clear tactical readability evidence showing terrain, deployment, movement, threat/range, and battle context.
- A closeout playtest/QA story after implementation stories are complete.

### Out of scope

- Strategic terrain movement costs or movement-type rules.
- Strategic supply/logistics.
- Weather, climate hazards, or White Sky environmental simulation.
- Fog of war, stealth/reveal, scouting uncertainty, or dirty-information rules.
- Strategic AI terrain valuation.
- Strategic topology rewrite, tile/hex/freeform strategic movement, or procedural map generation.
- Full XCOM simulation, elevation/high ground, universal overwatch, destructible cover, or complex line-of-sight rewrite.
- Final art, final icons, animation, VFX, audio, or localization pass.

### Deferred

- Terrain-influenced strategic movement and route requirements.
- Supply/logistics and weather.
- Full tactical cover/LoS model.
- Terrain-aware strategic AI.
- Tactical operations/Champion powers that manipulate terrain.
- Map editor UI for terrain/layout authoring.

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story | Status | Type | Depends On | Evidence |
| --- | --- | --- | --- | --- |
| [STORY-TERRAIN-001 Strategic Terrain Tags and Tactical Layout Family Contract](../stories/story-terrain-001-strategic-terrain-tags-and-tactical-layout-family-contract.md) | DONE / merged | Data + Contract + Validation | EPIC-010 approval; EPIC-009 DONE | PR #86; exact-head CI; post-merge CI |
| [STORY-TERRAIN-002 Tactical Layout Definitions and Deployment Zones](../stories/story-terrain-002-tactical-layout-definitions-and-deployment-zones.md) | DONE / merged | Tactical Data + Presentation | TERRAIN-001 DONE | PR #89; exact-head CI; post-merge CI |
| [STORY-TERRAIN-003 Tactical Blockers and Simple Defensive Terrain](../stories/story-terrain-003-tactical-blockers-and-simple-defensive-terrain.md) | DONE / merged | Tactical Rules + UI | TERRAIN-002 DONE | PR #92; exact-head CI; post-merge CI |
| [STORY-TERRAIN-004 Range, Threat, and Terrain Readability Pass](../stories/story-terrain-004-range-threat-and-terrain-readability-pass.md) | DONE / merged | Tactical UI + Playability | TERRAIN-003 DONE | PR #95; exact-head CI; post-merge CI |
| [STORY-TERRAIN-005 Strategic Context to Tactical Battlefield Smoke](../stories/story-terrain-005-strategic-context-to-tactical-battlefield-smoke.md) | DONE / merged | Integration Smoke | TERRAIN-001-004 DONE | PR #99; exact-head CI; post-merge CI |
| [STORY-QA-013 EPIC-010 Playtest and Closeout Review](../stories/story-qa-013-epic-010-playtest-and-closeout-review.md) | READY-candidate / approval pending | QA + Playability Review | EPIC-010 implementation stories DONE | Guarded prompt prepared |

Allowed story statuses: Draft, NEEDS WORK, READY-candidate, READY, IN PROGRESS, REVIEW, DONE, BLOCKED.

## Dependencies

- Upstream epics:
  - EPIC-009 is DONE / closed.
  - EPIC-006 tactical battle readability implementation stories are DONE / merged.
- Required GDDs:
  - Strategic Map GDD with terrain/context contract.
  - Tactical Combat GDD with tactical terrain/battlefield contract.
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
  - None for epic approval. Exact terrain tags, layout-family IDs, and tactical layout content are story-scoped unless a story cannot pass ambiguity check.

## Risks

| Risk | Type | Impact | Mitigation / Owner |
| --- | --- | --- | --- |
| Terrain epic turns into strategic movement rewrite | Scope / Technical | Destabilizes newly closed EPIC-009 loop | Explicitly exclude strategic terrain movement costs and topology changes / shared |
| Tactical terrain imports full XCOM cover/LoS complexity | Scope / UX | Slows frequent HoMM-like battles | Start with blockers, deployment, simple defensive cells, and readability only / shared |
| Strategic tags are too cosmetic to matter | Design | Player cannot connect map context to battle | First story requires tactical layout family bridge, not presentation-only tags / shared |
| Layout family mapping hardcodes one scenario | Technical | Future editor/content work blocked | Data-driven IDs and validation; no hardcoded map-to-battle switch logic / implementation agent |
| Terrain terms become canon too early | Lore | Overcommits geography/fiction | Use scenario-authored tags/display keys; prototype labels remain provisional / shared |

## Epic readiness gate

- [x] Capability goal is clear.
- [x] Relevant GDD sections exist or are updated by this preparation packet.
- [x] Relevant technical decisions exist.
- [x] Required test/evidence layers are known.
- [x] Required CI/build checks are known.
- [x] Required agent instruction scopes / AGENTS.md updates are known.
- [x] Scope and out-of-scope are explicit.
- [x] Child stories are identified.
- [x] Dependencies are known.
- [x] Major risks are documented.
- [x] At least one child story passes the Story Readiness Standard: `STORY-TERRAIN-001` is READY / approved.

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

APPROVED / IMPLEMENTATION COMPLETE; AWAITING QA CLOSEOUT APPROVAL. `STORY-TERRAIN-001` through `STORY-TERRAIN-005` are DONE / merged. Next recommended packet is `STORY-QA-013 EPIC-010 Playtest and Closeout Review` as READY-candidate / approval pending; no new Unity implementation is authorized until human approval promotes it to READY.
