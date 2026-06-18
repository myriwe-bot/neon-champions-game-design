---
title: EPIC-VSLICE-MVP-007 Strategic Map Readability, Bases, and Spatial Presentation
type: epic
status: approved
phase: production
owner: shared
created: 2026-06-15
updated: 2026-06-18
source_lore: [greenland, blue-monday, white-sky, digital-net]
related:
  [
    design/gdd/strategic-map,
    design/research/homm-like-strategic-map-topology-reference,
    production/planning/prototype-readability-and-map-next-steps-2026-06-15,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# Epic: EPIC-VSLICE-MVP-007 Strategic Map Readability, Bases, and Spatial Presentation

## Status

DONE / CLOSED FOR IMPLEMENTATION. Human approval recorded 2026-06-15 for the epic. `STORY-STRAT-READ-002`, `STORY-STRAT-BASE-001`, `STORY-STRAT-MAP-REGION-001`, and `STORY-QA-008` merged 2026-06-18. The closeout review accepted EPIC-007 from the QA pass and recommends pausing for human playtest or next-epic direction before starting another mechanics train.

This epic is not direct implementation authority. Agents and Codex may only implement READY child stories.

## Priority tier

Vertical Slice / MVP.

## Phase

Production.

## Owner

Shared.

## Related systems

- Strategic Map.
- Bases / starting hubs.
- Recruitment / reinforcement.
- Site control and ownership.
- Strategic UI/HUD.
- Strategic-to-tactical battle setup/result flow.
- Map presentation.

## Capability goal

Make the strategic layer feel more like a readable HoMM-like map and less like a prototype node diagram, while preserving the approved graph rules until a region/site or tile/hex migration is justified by playtest.

## Player / design value

The player should understand reachable sites, path costs, bases, guarded sites, ownership, interaction stakes, and battle return consequences before Neon Champions invests in a richer region/tile map.

Relevant pillars:

- [x] Cyberpunk strategy/RPG.
- [x] Infrastructure-first conflict.
- [x] HoMM-like exploration, capture, and tactical escalation.
- [x] Champions as legitimacy and force projection.
- [x] Intel as secrets turned into power, where data/cache sites are visible.
- [ ] Full dirty information/fog layer.

## Source requirements

- GDDs:
  - `design/gdd/strategic-map.md` §§1-8 for MVP direction, first scenario, core loop, data/state, and UX readability requirements.
  - `design/gdd/strategic-map.md` §9 for approved node-route topology and future tile/grid/region compatibility.
  - `design/gdd/strategic-map.md` §§10-13 for site states, resources/recruitment, Champion movement, turn/scenario/victory structure.
- References:
  - `design/research/homm-like-strategic-map-topology-reference.md` for HoMM3/Olden Era/Songs/King's Bounty map lessons.
  - `production/planning/prototype-readability-and-map-next-steps-2026-06-15.md` for approved ordering.
- ADRs / architecture docs / control-manifest sections:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

## Scope

### In scope

- Strategic map readability pass after tactical readability baseline:
  - reachable sites/routes;
  - path cost preview;
  - site category/ownership/guarded/objective/cache markers;
  - interaction preview;
  - clearer post-battle return summaries.
- Minimal home-base reinforcement/recruitment affordance.
- Region/site presentation prototype that keeps graph rules internally while presenting regions, roads/corridors, guarded zones, and ownership more spatially.

### Out of scope

- Full HoMM-style town building tree.
- Full square/hex strategic tile movement in the first pass.
- Procedural map generation.
- Map editor.
- Full fog, weather, logistics, supply, or strategic AI.
- Full economy or market simulation.
- Final map art, final icons, VFX, audio, or animation.

### Deferred

- True square/isometric tile map or hex strategic map.
- Full base construction/garrison/town management.
- Strategic AI opponent.
- Advanced route blocking/weather/supply/faction movement modifiers.

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story | Status | Type | Depends On | Evidence |
| --- | --- | --- | --- | --- |
| [STORY-STRAT-READ-002 Strategic Map Readability Pass](../stories/story-strat-read-002-strategic-map-readability-pass.md) | DONE / merged | Strategic UI + Playability Repair | Tactical readability baseline from EPIC-006 through STORY-TAC-AI-001 DONE | PR #55, post-merge CI, reachability/path/site/interaction/return-summary evidence |
| [STORY-STRAT-BASE-001 Starting Hub Reinforcement Preview](../stories/story-strat-base-001-starting-hub-reinforcement-preview.md) | DONE / merged | Strategic Rules + UI | STRAT-READ-002 DONE | PR #56, post-merge CI, base/reinforcement tests and evidence |
| [STORY-STRAT-MAP-REGION-001 Region/Site Presentation Prototype](../stories/story-strat-map-region-001-region-site-presentation-prototype.md) | DONE / merged | Strategic Presentation + Data | STRAT-READ-002 and STRAT-BASE-001 DONE | PR #57, post-merge CI, region/site map presentation evidence, no topology rewrite |
| [STORY-QA-008 Strategic Map Region Playtest and Closeout Review](../stories/story-qa-008-strategic-map-region-playtest-and-closeout-review.md) | DONE / merged | QA + Playability Review | EPIC-007 child stories DONE | PR #58, post-merge CI, closeout review/evidence; no new mechanics |

Allowed story statuses: Draft, NEEDS WORK, READY-candidate, READY, IN PROGRESS, REVIEW, DONE, BLOCKED.

## Dependencies

- Upstream epics:
  - `EPIC-VSLICE-MVP-006` should deliver enough tactical readability that strategic decisions can be judged.
- Required GDDs:
  - Strategic map GDD cited above.
- Required technical decisions:
  - Existing Unity technical scheme and control manifest.
- Required testing/evidence strategy:
  - Strict layered tests, PlayMode smoke, PNG/manual evidence, CI.
- Required CI/build automation:
  - Existing Unity Foundation CI.
- Required agent instruction scopes / AGENTS.md updates:
  - Unity root and scoped AGENTS.md at implementation time.
- Required data/assets:
  - Prototype text/markers are allowed; final map art is not required.

## Risks

| Risk | Type | Impact | Mitigation / Owner |
| --- | --- | --- | --- |
| Jumping to full tiles too early | Scope / Technical | Large rewrite before need is proven | Start with graph-backed region/site presentation / shared |
| Bases expand into town-building tree | Scope | Unbounded design and implementation | First base story is one fixed reinforcement/recruitment affordance / shared |
| Strategic readability hides tactical confusion | UX | Player still cannot judge the loop | Start this epic after tactical readability baseline / shared |
| Region/site presentation conflicts with approved graph model | Technical | Rework of strategic domain | Keep graph as rules substrate; add presentation/data fields only / implementation agent |

## Epic readiness gate

- [x] Capability goal is clear.
- [x] Relevant GDD sections exist.
- [x] Relevant technical decisions exist.
- [x] Required test/evidence layers are known.
- [x] Required CI/build checks are known.
- [x] Required agent instruction scopes / AGENTS.md updates are known.
- [x] Scope and out-of-scope are explicit.
- [x] Child stories are identified as draft targets.
- [x] Dependencies are known.
- [x] Major risks are documented.
- [x] At least one child story is READY. `STORY-STRAT-READ-002` is READY / approved after EPIC-006 baseline landed.

## Epic DONE gate

- [x] Required child stories are DONE or explicitly deferred by human closeout.
- [x] Required verification evidence exists.
- [x] Required automated tests, validators, PlayMode/smoke evidence, and manual/PNG evidence are complete or accepted as documented exceptions.
- [x] Unresolved omissions are documented.
- [x] Docs have been updated in the correct source-of-truth layer.
- [x] Playtest/QA evidence exists if required.
- [x] No open blocker remains hidden.
- [x] Human review accepts the epic as complete.

## Anti-pattern check

Invalid epic behavior:

- [ ] This epic authorizes production implementation directly.
- [ ] This epic replaces READY stories.
- [ ] This epic hides ambiguous design decisions.
- [ ] This epic bundles unrelated work for convenience.
- [ ] This epic asks agents to figure out missing details.

## Verdict

DONE / CLOSED. EPIC-007 implementation children and closeout review are merged through Unity PR #58, with Unity README pointer cleanup merged in PR #59. No next Unity implementation story is READY; next direction remains human-owned.
