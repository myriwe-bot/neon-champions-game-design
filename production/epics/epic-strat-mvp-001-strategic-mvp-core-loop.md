---
title: EPIC-STRAT-MVP-001 Strategic MVP Core Loop
type: epic
status: approved
phase: production
owner: shared
created: 2026-06-01
updated: 2026-06-03
source_lore: [greenland, blue-monday, white-sky, digital-net]
related: [design/gdd/strategic-map, docs/architecture/unity-technical-scheme, docs/architecture/control-manifest, docs/architecture/testing-strategy, docs/architecture/ci-build-automation, production/stories/story-strat-001-scenario-map-graph-state, production/stories/story-strat-002-hotseat-turn-ownership, production/stories/story-strat-003-champion-route-movement, production/stories/story-qa-002-strategic-map-readability-actor-clarity-fix-pass, production/stories/story-tac-001-battle-setup-result-dto-contracts, production/sprints/strategic-mvp-story-train-001]
approval: approved
---

# Epic: EPIC-STRAT-MVP-001 Strategic MVP Core Loop

## Status

Story Ready.

This epic is a production planning container. It does not authorize implementation directly. Implementation is authorized only by READY child stories that trace to approved GDD and technical-control docs.

## Priority tier

MVP.

## Phase

Production.

## Owner

Shared.

## Related systems

- Strategic map.
- Scenario runtime state.
- Champion strategic movement.
- Site interaction and ownership/control.
- Strategic resources.
- Tactical battle handoff.
- Turn, objective, and victory state.

## Capability goal

Create the first playable strategic MVP loop foundation: a two-faction local-hotseat scenario on an authored node-route map, with initialized scenario state, Champion positions, site/resource state, turn/objective/victory state, and later stories for movement, site interaction, tactical handoff, and end-turn resolution.

## Player / design value

This epic turns the approved strategic-map GDD into the minimum playable HoMM-like overworld layer for Neon Champions: two opposing Champions competing over infrastructure, resources, guarded sites, and a central objective without requiring strategic AI in the first MVP.

Relevant pillars:
- [x] Cyberpunk strategy/RPG
- [x] Infrastructure-first conflict
- [x] Champions as legitimacy and force projection
- [x] Intel as secrets turned into power
- [x] HoMM-like exploration, capture, and tactical escalation
- [ ] Dirty information
- [ ] Other:

## Source requirements

An epic may group work, but child stories must carry exact source sections before READY.

- GDDs:
  - `design/gdd/strategic-map.md` §§2, 3, 6, 7, 8, 9, 10, 11, 12, 13.
  - Tactical handoff later depends on `design/gdd/strategic-map.md` §14 and relevant tactical-combat GDD sections.
- Design bridges:
  - N/A for current child story. Future lore-facing scenario content must use an approved lore import/design bridge.
- UX specs:
  - N/A for STORY-STRAT-001. Future visual strategic-map stories require explicit UX/readability requirements.
- Data registry docs:
  - No final registry yet. STORY-STRAT-001 may use test-local data and serializable-friendly domain models without deciding the final authoring pipeline.
- ADRs / architecture docs / control-manifest sections:
  - `docs/architecture/unity-technical-scheme.md` — domain logic separate from Unity presentation.
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 9, 10.
  - `docs/architecture/testing-strategy.md` — story-type evidence matrix and TDD requirement.
  - `docs/architecture/ci-build-automation.md` — CI evidence requirements for implementation PRs.
- Worldbuilding links, if lore-facing:
  - Greenland / Blue Monday / White Sky / Digital-Net are thematic source context only. STORY-STRAT-001 is not authorized to add new player-facing lore.
- Reference/legal/cultural constraints, if relevant:
  - Future Greenland map/content stories must check cultural/geographic sensitivity before adding player-facing names or places.

## Scope

### In scope

Capabilities this epic intends to deliver through child stories:

- Scenario/map graph definitions and initialized runtime state.
- Validation of MVP strategic scenario data.
- Champion strategic movement over authored routes.
- Turn order, start/end turn refresh, and objective hold tracking.
- Site state, ownership/control, one-shot/recurring rewards, and basic recruitment/reinforcement points.
- Guarded-site battle request generation and tactical `BattleSetup` handoff.
- Tactical `BattleResult` application back into strategic site, resource, army, Champion defeat, and victory state.
- Minimal local-hotseat flow sufficient for a human to play both sides through the strategic loop.

### Out of scope

Adjacent capabilities explicitly excluded from this epic unless later promoted by a new epic/story:

- Strategic AI.
- Online or simultaneous multiplayer.
- Final visual map presentation, camera polish, or UI art direction beyond scoped child stories.
- Full town trees, deep economy, upkeep, logistics, weather, supply, fatigue, diplomacy, and fog/feed misinformation.
- Multiple Champions per faction.
- More than two factions.
- Campaign persistence or full save/load format.
- Final map/scenario editor or external data pipeline.
- New lore, faction naming, site naming, or player-facing scenario content not already approved.

### Deferred

Known future work not part of the current first loop slice:

- Rich strategic UI/UX and map readability polish.
- Map editor and final content authoring tools.
- Strategic AI and campaign-scale systems.
- Advanced Intel operations and dirty-information mechanics.
- Multi-map campaign persistence and progression.

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story | Status | Type | Depends On | Evidence |
|---|---|---|---|---|
| [[production/stories/story-strat-001-scenario-map-graph-state|STORY-STRAT-001 Scenario Map Graph State]] | READY / implementation verified for merge | Logic + Config/Data | SPIKE-001 foundation, approved strategic-map GDD, approved technical controls | EditMode/domain validation tests, serialization round-trip proxy, TDD/CI evidence |
| [[production/stories/story-strat-002-hotseat-turn-ownership|STORY-STRAT-002 Hotseat Turn Ownership]] | READY-candidate | Logic | STORY-STRAT-001 | Turn validation, start-turn reset, end-turn advancement, round increment tests |
| [[production/stories/story-strat-003-champion-route-movement|STORY-STRAT-003 Champion Route Movement]] | READY-candidate | Logic | STORY-STRAT-001, preferably STORY-STRAT-002 | Movement validation, preview non-mutation, state-transition tests |
| [[production/stories/story-strat-vis-001-minimal-strategic-map-presentation|STORY-STRAT-VIS-001 Minimal Strategic Map Presentation]] | READY-candidate | Visual/Feel + Integration | STORY-STRAT-001, STORY-STRAT-002 recommended | Scene load, node/route/Champion markers, active faction display, screenshot/video |
| [[production/stories/story-strat-input-001-select-champion-and-route-move|STORY-STRAT-INPUT-001 Select Champion and Route Move]] | READY-candidate | Integration + UI/Input | STORY-STRAT-001, STORY-STRAT-002, STORY-STRAT-003, STORY-STRAT-VIS-001 | Select/move/reject PlayMode smoke, visual marker update, screenshot/video |
| [[production/stories/story-strat-ui-001-minimal-hotseat-hud|STORY-STRAT-UI-001 Minimal Hotseat HUD]] | READY-candidate | UI + Integration | STORY-STRAT-001, STORY-STRAT-002, STORY-STRAT-003, STORY-STRAT-VIS-001, STORY-STRAT-INPUT-001 recommended | HUD startup, movement-point display, End Turn update, screenshot/video |
| [[production/stories/story-loop-001-minimal-local-hotseat-strategic-loop-smoke|STORY-LOOP-001 Minimal Local Hotseat Strategic Loop Smoke]] | DONE / merged in Unity PR #9 | Playtest + Integration + UX/Smoke | STORY-STRAT-001/002/003, VIS-001, INPUT-001, UI-001 | End-to-end two-faction movement/end-turn smoke, checklist, screenshot/video, CI |
| [STORY-QA-001 Strategic Smoke Cleanup, Readability, and Bugfix Pass](../stories/story-qa-001-strategic-smoke-cleanup-readability-bugfix-pass.md) | DONE / merged in Unity PR #10 | QA + UI/UX Readability + Bugfix | STORY-LOOP-001 | Readability/layout fixes, map/HUD feedback clarity, screenshots/checklist, CI |
| [STORY-TAC-001 Battle Setup Result DTO Contracts](../stories/story-tac-001-battle-setup-result-dto-contracts.md) | DONE / merged in Unity PR #11 | Logic + Integration contract | STORY-STRAT-001, strategic-map §14 | DTO validation, setup/result matching, snapshot immutability tests |
| [STORY-QA-002 Strategic Map Readability and Actor-Clarity Fix Pass](../stories/story-qa-002-strategic-map-readability-actor-clarity-fix-pass.md) | DONE / merged in Unity PR #12 | QA + UI/UX Readability + Bugfix | STORY-LOOP-001, STORY-QA-001, STORY-TAC-001 | Non-overlap layout checks, actor clarity, map feedback, before/after screenshots, CI |
| STORY-STRAT-004 Site Interaction and Guarded Battle Trigger | Draft placeholder | Logic + Integration | STORY-STRAT-001, STORY-STRAT-002, STORY-STRAT-003, STORY-TAC-001 | Interaction preview/apply and BattleSetup creation tests |
| STORY-STRAT-005 Strategic Battle Result Application | Draft placeholder | Logic + Integration | STORY-TAC-001, STORY-STRAT-004 | BattleResult application, losses, guard clearing, rewards, control, victory tests |

Allowed story statuses: Draft, NEEDS WORK, READY, IN PROGRESS, REVIEW, DONE, BLOCKED.

## Dependencies

- Upstream epics:
  - None.
- Required GDDs:
  - `design/gdd/strategic-map.md` is the main source.
  - Tactical handoff stories will also require relevant tactical-combat GDD sections.
- Required technical decisions:
  - Unity technical scheme.
  - Control manifest.
  - Testing strategy.
  - CI/build automation.
  - SPIKE-001 Unity project and CI foundation available in implementation repo.
- Required testing/evidence strategy:
  - EditMode/domain tests for logic stories.
  - PlayMode/smoke evidence for loop/UX-facing stories.
  - TDD evidence for production gameplay logic.
  - CI evidence for implementation PRs.
- Required CI/build automation:
  - GitHub Actions or documented human-approved exception per implementation PR.
- Required agent instruction scopes / AGENTS.md updates:
  - Unity repo root `AGENTS.md` and scoped AGENTS.md files under touched implementation paths must be read at story execution time.
- Required data/assets:
  - None for STORY-STRAT-001 beyond test-local placeholder data.
  - Future content-facing stories need approved data/content source docs.
- Required tools/packages:
  - Existing Unity test/CI setup from SPIKE-001.
- Blocking open questions:
  - None for STORY-STRAT-001 after parent epic creation and human approval.
  - Future child stories must not assume final data authoring, save/load, visual map, or tactical integration details without exact story scope.

## Risks

| Risk | Type | Impact | Mitigation / Owner |
|---|---|---|---|
| Epic scope expands into "implement strategic map" | Scope | Agents may overbuild beyond first loop | Keep implementation authority in READY child stories only / shared |
| Data models accidentally decide final authoring pipeline | Technical | Premature tooling lock-in | STORY-STRAT-001 permits serializable-friendly domain models and test-local data only / implementer |
| Placeholder IDs become player-facing lore | Lore-Cultural-IP / Content | Unapproved names leak into game | Keep placeholders test-local and non-player-facing / implementer + reviewer |
| Tactical handoff stories outpace tactical implementation | Technical / Dependency | Battle integration blocks loop completion | Use explicit DTO contracts and story-level stubs only when authorized / shared |
| Testing burden weakens under time pressure | Testing | Strategic rules become fragile | Enforce TDD, EditMode tests, CI evidence, and omissions section / reviewer |
| Local-hotseat MVP is mistaken for strategic AI readiness | Design | False expectation of autonomous opponent | State strategic AI out of scope until separate epic/story / shared |

## Epic readiness gate

An epic may enter production only when all items are true:

- [x] Capability goal is clear.
- [x] Relevant GDD sections exist.
- [x] Relevant technical decisions exist or are explicitly N/A.
- [x] Required test/evidence layers are known for expected child story types.
- [x] Required CI/build checks are known for expected child story types, or explicitly N/A with reason.
- [x] Required agent instruction scopes / AGENTS.md updates are known, or explicitly N/A with reason.
- [x] Scope and out-of-scope are explicit.
- [x] Child stories are identified.
- [x] Dependencies are known.
- [x] Major risks are documented.
- [x] At least one child story can pass the Story Readiness Standard.

## Epic DONE gate

An epic may be marked Complete only when all items are true:

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

Story Ready.

STORY-STRAT-001 is READY after human approval and parent epic creation. Remaining work is implementation in the Unity repo through the approved story, with exact source/test paths discovered from that repo's AGENTS.md and assembly layout before coding.
