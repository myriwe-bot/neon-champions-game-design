---
title: STORY-ARMY-002 Tactical Role Behaviors and Sensor Lock
type: story
status: done
phase: production
owner: shared
created: 2026-06-18
updated: 2026-06-19
source_lore: [greenland, qxz-meridian, white-sky]
related:
  [
    production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity,
    production/planning/epic-008-faction-armies-recruitment-and-role-identity-plan,
    production/stories/story-army-001-mvp-faction-unit-definitions-and-roster-seed,
    design/gdd/faction-unit-rosters,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-ARMY-002 Tactical Role Behaviors and Sensor Lock

## Status

DONE / merged. Human approval recorded 2026-06-18 from chat: `Approved`, in response to approval question for `STORY-ARMY-002 Tactical Role Behaviors and Sensor Lock` with the recommended default Sensor Lock effect. Unity PR #61 merged 2026-06-19.

## Story type

Tactical Rules + UI / Playability Differentiation.

## Parent epic

- [EPIC-VSLICE-MVP-008 Faction Armies, Recruitment, and Tactical Role Identity](../epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md)

## User/player/system value

As a player, I want the newly defined early units to behave differently in battle, so that army composition becomes readable and tactically meaningful before recruitment expands the strategic loop.

## Source requirements

Exact source references:

- `production/stories/story-army-001-mvp-faction-unit-definitions-and-roster-seed.md` for approved unit IDs, display names, factions, and placeholder stats.
- `production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md` for the accepted direction: roles plus one readable status/effect, QXZ-first Sensor Lock / Marked.
- `design/gdd/tactical-combat.md` §§3-6.7 for stack-first combat, actions, retaliation hooks, range, and visible statuses.
- `design/gdd/faction-unit-rosters.md` for the first 3-line Home Rule / QXZ roster fantasy; use only the already-approved seed scope.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.

## In scope

Concrete implementation tasks:

- Make the ARMY-001 unit definitions produce visible tactical role differences without adding new faction rosters or recruitment.
- Preserve or refine the current data fields for:
  - melee / retaliator;
  - ranged / recon;
  - support / mobility;
  - heavy defender.
- Implement one readable status/effect: **Sensor Lock / Marked**.
  - Primary owner: QXZ `strato_sensor_swarm` / Strato Sensor Swarm.
  - Effect should be small, visible, and easy to explain.
  - Human-approved MVP effect: Strato Sensor Swarm applies a separate 1 AP Sensor Lock support action; the next successful attack against the marked target deals +1 stack-count damage and consumes the mark.
- Add event-feed/status text that explains:
  - who applied Sensor Lock / Marked;
  - who is marked;
  - what changed mechanically;
  - when the status expired or was consumed, if applicable.
- Ensure melee/retaliator, ranged/recon, and heavy defender roles remain visible in labels/snapshots/evidence.
- Add focused tests for role behavior and Sensor Lock edge cases.
- Add PlayMode/PNG evidence under `production/evidence/STORY-ARMY-002/`.

## Out of scope

Not authorized by this story:

- No recruitment UI/action or strategic recruitment changes. That belongs to ARMY-003.
- No full town/dwelling tree.
- No upgraded variants or new unit lines.
- No full balance pass.
- No full cover, LOS, morale, damage-type taxonomy, armor/shield system, or AP redesign.
- No Champion Assets/Operations expansion.
- No strategic AI.
- No final art/icons/VFX/audio/animation.
- No hard-canon rename of Home Rule Coalition.

## Allowed stubs, mocks, placeholders, or temporary data

- Sensor Lock / Marked can use prototype text labels and existing event-feed/status surfaces.
- The exact numerical bonus/effect may be a small prototype value if it is explicit, tested, documented, and easy to change later.
- Sled Logistics Team may remain a support/mobility placeholder if implementing a distinct tactical ability would exceed scope; it should still display as a distinct support/mobility role.
- Home Rule counterplay to Sensor Lock may remain deferred unless it is very small and does not broaden scope.

## Dependencies

- `STORY-ARMY-001` DONE / merged.
- Existing tactical board, action, event-feed, labels, AP, retaliation, and CombatAI baseline.
- Existing Unity Foundation CI.

## Acceptance criteria

- [ ] Strato Sensor Swarm can apply a visible Sensor Lock / Marked status/effect to a legal enemy target.
- [ ] Sensor Lock / Marked has an explicit, tested mechanical effect and does not remain a cosmetic flag.
- [ ] Event feed/status text identifies the applier, target, and effect in player-readable terms.
- [ ] Invalid Sensor Lock / Marked attempts fail safely with concrete diagnostics and no partial mutation.
- [ ] The effect cannot target defeated, same-side, missing, or out-of-range targets unless the story explicitly documents a narrower allowed target model.
- [ ] Melee/retaliator, ranged/recon, support/mobility, and heavy defender role labels remain visible in tactical snapshots/evidence.
- [ ] Existing movement, attack, retaliation, AP, CombatAI, battle handoff, and ARMY-001 unit definition behavior do not regress.
- [ ] Evidence documents the prototype Sensor Lock / Marked value/effect and deferred role depth.

## Verification requirements

- Unit tests: Required for Sensor Lock / Marked validation, application, effect, expiration/consumption if any, and invalid target cases.
- Unity edit-mode tests: Required for tactical board/action behavior and snapshot/event text where practical.
- Unity play-mode tests: Required if current PlayMode smoke can verify visible status/evidence.
- Integration/data validation tests: Existing validators remain green.
- Screenshot/video evidence: Required PNG evidence under `production/evidence/STORY-ARMY-002/` showing Sensor Lock / Marked applied and visible role labels.
- Performance budget or N/A: N/A.
- CI evidence: Unity Foundation CI exact-head before merge.
- TDD evidence required? Yes for production tactical logic.
- Automation deferred? No broad exception approved; document any UI-only manual evidence.

## Ambiguity Check

Status: PASS.

Human-approved answers recorded 2026-06-18:

1. Sensor Lock / Marked effect:
   - Strato Sensor Swarm applies a 1 AP Sensor Lock support action.
   - The next successful attack against the marked target deals +1 stack-count damage.
   - The mark is consumed after that bonus attack.
2. Sensor Lock action cost/type:
   - Separate 1 AP support action, not a replacement for the normal attack.
3. Authorized applier:
   - Only QXZ `strato_sensor_swarm` / Strato Sensor Swarm applies Sensor Lock in this story.
4. Deferred scope:
   - Home Rule counterplay is deferred.
   - Sled Logistics Team remains a visible support/mobility role only; no special mobility ability yet.

Human-approved exceptions:

- None.

## Branch / PR requirements

- Branch name after approval: `story/STORY-ARMY-002-tactical-role-behaviors-sensor-lock`
- PR title after approval: `STORY-ARMY-002 Tactical role behaviors and Sensor Lock`
- Required linked story ID: `STORY-ARMY-002`.
- Required linked GDD/ADR/control docs:
  - `design/gdd/faction-unit-rosters.md`.
  - `design/gdd/tactical-combat.md`.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: read Unity root `AGENTS.md` plus scoped AGENTS files for all touched Runtime/Domain/Application/Presentation/Tests/Evidence directories.
- Required evidence summary: tests run, PlayMode/PNG evidence path, CI URL.
- Required omissions section: explicitly list known omissions/stubs/placeholders/deferred work or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked or explicitly N/A.
- [x] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] UX/reference sources are linked.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied or marked non-blocking.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval recorded.

## DONE gate

- [x] Implementation matches approved story scope.
- [x] Acceptance criteria pass.
- [x] Required verification evidence exists.
- [x] Required automated tests, validators, and PlayMode/smoke evidence pass, or human-approved exceptions are documented.
- [x] No unauthorized design or architecture decisions were introduced.
- [x] Omissions/stubs/mocks/deferred work are explicitly documented.
- [x] PR/code review is complete.
- [x] CI passes or human-approved exceptions are documented.
- [x] Required docs were updated in the correct source-of-truth layer.

Merge evidence:

- Unity PR #61: https://github.com/myriwe-bot/neon-champions-unity/pull/61
- Merge commit: `847e1700535855571acbf8f289e14a4b46d05293`
- Post-merge Unity Foundation CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27821650148

## Verdict

DONE / merged. Prepare `STORY-ARMY-003` only as approval-pending until human approval resolves its Ambiguity Check.
