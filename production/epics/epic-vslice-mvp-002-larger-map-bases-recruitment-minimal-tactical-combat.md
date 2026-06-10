---
title: EPIC-VSLICE-MVP-002 Larger Map, Bases, Recruitment, and Minimal Tactical Combat
type: epic
status: done
phase: production
owner: shared
created: 2026-06-04
updated: 2026-06-10
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

DONE. Direction approved by user on 2026-06-04 as option C, tightly scoped: modest larger map + one simple real tactical battle + one recruitment site. All required child stories are DONE / merged through `STORY-QA-004`.

Closeout accepted by the user on 2026-06-10 after `STORY-QA-004` visual/playability remediation. Unity PR #27 merged as `d7661bf0e1fe7edca0704ac928994489e93ad337`; post-merge Unity `main` CI passed in run https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27278547989.

Remaining limitations are accepted as deferred scope, not blockers: final UI/art/accessibility, strategic AI, full tactical depth, economy depth, save/load, Intel systems, final names/content, and full objective/victory structure.

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

This epic moved Neon Champions from "strategic systems prototype" toward a recognizable HoMM-like MVP slice: bases, map expansion, neutral-site capture, recruitment pressure, real tactical escalation, and a readable-enough prototype UI.

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
  - `design/gdd/faction-unit-rosters.md` for any unit/stack fixtures; child stories used placeholder units/content where final roster content was not approved.
- ADRs / architecture docs / control-manifest sections:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Worldbuilding/lore-facing content:
  - No new final city/base/site names were authorized; placeholder/localization keys remained acceptable.

## Scope

### In scope

- Modest larger strategic map, not a final campaign map.
- Two starting bases/cities as faction anchors.
- One recruitment/reinforcement site with simple fixed offer/stock/cost rules.
- One or more neutral guarded sites that can be captured.
- Integration with the minimal real hex-grid tactical combat foundation from `EPIC-STRAT-MVP-001`.
- Visible capture/recruitment feedback and evidence-ready smoke path.
- Prototype readability/playability remediation sufficient for human closeout.

### Out of scope

- Full town building trees.
- Full economy or market simulation.
- Full tactical combat system, roster balance, ability catalogue, morale, operations, cover, LOS sophistication, animation, audio, final UI, or final art.
- Strategic AI.
- Online/networking.
- Campaign persistence or final save/load.
- Deep Intel/dirty-information systems.
- Final map/scenario editor.
- Full objective/victory structure.

### Deferred

- Multiple city/base types.
- Multiple recruitment sites and faction-specific recruitment economies.
- Central objective victory polish and scenario win/loss structure.
- Enemy-faction site contests and Champion-vs-Champion encounter depth.
- Tactical ability/status/deck/operation depth.
- Tactical casualty persistence beyond current minimal result/capture loop.

## Child stories

Agents and Codex may not implement this epic directly. They may only implement READY child stories.

| Story | Status | Type | Depends On | Evidence |
| --- | --- | --- | --- | --- |
| [STORY-TAC-005 Basic Tactical Player Controls](../stories/story-tac-005-basic-tactical-player-controls.md) | DONE / merged | Tactical UI/Input + Integration + UX/Smoke | STORY-LOOP-002, existing minimal tactical domain | Unity PR #20, command tests, PlayMode smoke, screenshot artifact, CI |
| [STORY-MAP-001 Larger Two-Base Strategic Map Slice](../stories/story-map-001-larger-two-base-strategic-map-slice.md) | DONE / merged | Config/Data + Visual/Feel + Strategic Integration | STORY-TAC-005, strategic-map §§2/3/4/6/8/9 | Unity PR #21, map validation, real base/hub site type, central objective interaction, two-choice PlayMode smoke, screenshot/video, CI |
| [STORY-STRAT-006 Simple Recruitment Site and Fixed Offers](../stories/story-strat-006-simple-recruitment-site-fixed-offer.md) | DONE / merged | Logic + UI/Integration + Config/Data | MAP-001, strategic-map §§4/6/8/10/11/12 | Unity PR #22, normal/upgraded offer validation, cost/stock/apply tests, screenshot evidence, CI |
| [STORY-TAC-006 Multi-Stack Attacker Tactical Setup](../stories/story-tac-006-multi-stack-attacker-tactical-setup.md) | DONE / merged | Logic + Integration + Tactical UI/Smoke | TAC-002, TAC-005, STRAT-006 | Unity PR #23, two-stack attacker placement tests, invalid setup rejection, recruited-army handoff smoke, CI |
| [STORY-LOOP-003 Larger Map Recruitment and Neutral Capture Vertical Slice](../stories/story-loop-003-larger-map-recruitment-and-neutral-capture-vertical-slice.md) | DONE / merged | Playtest + Integration + UX/Smoke | MAP-001, STRAT-006, TAC-006 | Unity PR #24, connected recruitment-to-capture smoke, screenshots, checklist, CI |
| [STORY-QA-003 Loop Slice Visual Readability and Clickable Layout Pass](../stories/story-qa-003-loop-slice-visual-readability-and-clickable-layout-pass.md) | DONE / merged | QA + UI/UX Readability + Visual/Feel | LOOP-003 | Unity PR #25, before/after screenshots, clickable controls/views, layout/readability checklist, CI |
| [STORY-QA-004 Playability Map Scale, Zoom, and UI Clarity Pass](../stories/story-qa-004-playability-map-scale-zoom-and-ui-clarity-pass.md) | DONE / merged | QA + UI/UX Readability + Visual/Feel + Interaction Regression | QA-003 + hotfix PR #26 | Unity PR #27, runtime uGUI layout, PNG evidence, marker separation, focus controls, post-merge CI |

Allowed story statuses: Draft, NEEDS WORK, READY, IN PROGRESS, REVIEW, DONE, BLOCKED.

## Dependencies

- Upstream epics:
  - `EPIC-STRAT-MVP-001` provided the guarded-site capture loop and minimal tactical combat foundation.
- Required GDDs:
  - Strategic Map approved sections.
  - Tactical Combat MVP sections; hex-grid decision recorded.
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

## Risks

| Risk | Type | Impact | Mitigation / Outcome |
| --- | --- | --- | --- |
| Tactical combat scope explodes | Scope | Epic becomes a full tactics game before the strategy loop is testable | Kept tactical work to hex board, stack placement, movement, attack, defeat, result return, and basic controls |
| Larger map becomes content design | Lore-Cultural-IP / Scope | Agents invent final city/site names or faction content | Used placeholders/localization keys; final content deferred |
| Recruitment grows into town-building | Scope | Vertical slice loses focus | Kept recruitment to fixed site/offers |
| UI readability regresses | UX | Demo becomes hard to judge | Added QA-003, hotfix PR #26, and QA-004 uGUI/PNG remediation |
| Hex grid decision conflicts with old docs | Design | Agents treat square/hex as undecided | Tactical GDD and stories cite the hex MVP decision |

## Epic readiness gate

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
- [x] At least one child story passed the Story Readiness Standard.

## Epic DONE gate

- [x] All required child stories are DONE.
- [x] Required verification evidence exists.
- [x] Required automated tests, validators, PlayMode/smoke evidence, and manual evidence are complete or accepted as documented exceptions.
- [x] Unresolved omissions are documented.
- [x] Docs have been updated in the correct source-of-truth layer.
- [x] Playtest/QA evidence exists if required; human visual closeout accepted after QA-004.
- [x] No open blocker remains hidden.
- [x] Human review accepts the epic as complete.

## Anti-pattern check

Invalid epic behavior:

- [ ] This epic authorizes production implementation directly.
- [ ] This epic replaces READY stories.
- [ ] This epic hides ambiguous design decisions.
- [ ] This epic bundles unrelated work for convenience.
- [ ] This epic asks agents to figure out missing details.

If any box above is checked, the epic needs revision.

## Verdict

DONE / closed. User approved closeout on 2026-06-10. This epic proves the prototype vertical slice at current quality: larger map, bases, recruitment, neutral capture, minimal tactical combat, strategic result feedback, and acceptable prototype readability. The next approved planning direction is a new objective/tactical-stakes epic: scenario objective + defender tiers + simple stack HP/strength persistence + staged Champion-vs-Champion combat.
