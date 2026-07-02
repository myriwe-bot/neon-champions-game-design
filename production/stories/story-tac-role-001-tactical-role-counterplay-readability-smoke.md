---
title: STORY-TAC-ROLE-001 Tactical Role Counterplay Readability Smoke
type: story
status: ready
phase: production
owner: shared
created: 2026-07-02
updated: 2026-07-02
source_lore: []
related:
  [
    production/epics/epic-vslice-mvp-014-tactical-role-counterplay-and-combat-decision-readability,
    production/planning/next-implementation-direction-brief-2026-07-02,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-TAC-ROLE-001 Tactical Role Counterplay Readability Smoke

## Status

READY / approved. Human approval recorded 2026-07-02: "approved". This is the current narrow implementation packet for EPIC-014 after EPIC-013 closed.

## Story type

Tactical UX + tactical rules/readability smoke with PlayMode evidence.

## Parent / context

Parent: `EPIC-VSLICE-MVP-014 Tactical Role Counterplay and Combat Decision Readability`.

The strategic pressure loop is now readable enough to expose tactical battles as the next weak endpoint. This story should not redesign tactical combat. It should make exactly one existing-or-nearby tactical decision pattern understandable and visibly consequential.

## Player/design value

As a player, I need one tactical choice to clearly show what role/counterplay decision is available, why it matters, and what happened, so tactical combat starts feeling like a readable battle system rather than generic stack clicking.

## Source authority

Required sources:

- `production/planning/next-implementation-direction-brief-2026-07-02.md` — approved direction and first-slice boundary.
- `production/epics/epic-vslice-mvp-014-tactical-role-counterplay-and-combat-decision-readability.md` — parent scope and exclusions.
- `design/gdd/tactical-combat.md` §§3-6 — MVP tactical principles, flat hex grid, stack entities, AP/action loop, movement/attack, retaliation, range, and readable statuses.
- `design/gdd/tactical-combat.md` §§6.2A, 6.3, 6.4, 6.5, and 6.6 — tactical battlefield readability, AP/actions, retaliation, attack/damage/defense, and information/range/cover boundaries.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.

## In scope

- Add or clarify exactly one tactical role/counterplay decision pattern using existing systems where practical. Acceptable implementation choices include one of:
  - a marked/sensor-locked target choice;
  - a ranged-threat or out-of-range choice made clearer and consequential;
  - a Defend tradeoff made clearer in relation to incoming/retaliation risk;
  - a simple focus-fire/assault/support counter cue using existing stack and event-feed state.
- Prefer the smallest implementation that gives a real player-facing decision and result. Codex may choose the lowest-risk pattern after inspecting current Unity code, but must document the chosen pattern in PR evidence.
- Surface the decision through existing tactical presentation snapshot, HUD/status, event feed, labels, or evidence text so the player can read:
  - before-choice tactical context;
  - the available choice and why it matters;
  - action result / consequence;
  - any denial or no-op state without partial mutation.
- Add focused tests for the chosen decision pattern and no-partial-mutation/denial behavior where applicable.
- Add PlayMode smoke/evidence under Unity `production/evidence/STORY-TAC-ROLE-001/` showing before-choice, choice-available, action-result, and surrounding-loop-unbroken states.

## Out of scope

- No broad tactical AI, initiative rewrite, LOS rewrite, cover system, universal overwatch, ability trees, faction-wide roster redesign, new tactical unit families, or balance pass.
- No new strategic economy, campaign/meta systems, victory rules, map topology/content, or new tactical layout families.
- No dirty-information/PR/counter-intel systems.
- No Champion spellbook/loadout/progression expansion.
- No final art/audio/VFX/icons/localization/accessibility framework.
- No implementation from draft/lore-only sources or chat memory.

## Allowed stubs, mocks, placeholders, or temporary data

- Prototype labels, simple markers, event-feed text, and small code-side constants are allowed if they are clearly temporary and listed in PR omissions.
- The chosen counterplay pattern may be a minimal prototype mechanic if it is state-backed, tested, and visibly explained.
- No final balance or canon naming is required.

## Dependencies

- EPIC-013 DONE / closed.
- Existing tactical battle setup, AP/Defend, retaliation, range/threat readability, terrain readability, unit/stack presentation, and PlayMode evidence infrastructure.
- Unity current-task README pointer must name this story before Codex implementation.

## Acceptance criteria

- [ ] A single chosen tactical role/counterplay decision pattern is named in code/evidence and remains inside this story's scope.
- [ ] Before the choice, the tactical UI/snapshot/evidence shows enough context for the player to understand the available decision.
- [ ] The choice itself is visible in player-facing text/labels/event feed and explains why it matters.
- [ ] Applying the choice produces a visible state-backed result or consequence; it is not screenshot-only text.
- [ ] Invalid/unavailable/repeat/no-op use, if applicable to the chosen pattern, gives clear feedback and does not partially mutate tactical state.
- [ ] Existing movement, attack, AP/Defend, retaliation, range/threat, tactical handoff, and surrounding loop smokes are not intentionally regressed.
- [ ] Evidence under Unity `production/evidence/STORY-TAC-ROLE-001/` includes before-choice, choice-available, action-result, surrounding-loop-unbroken screenshots/notes, and omissions/deferred-work notes.
- [ ] Exact-head Unity Foundation CI passes before merge.

## Verification requirements

Required unless a blocker is documented in PR evidence:

- `git diff --check`.
- Focused EditMode tests for the chosen decision pattern, state-backed result/consequence, and denial/no-partial-mutation where applicable.
- PlayMode smoke or generated PNG/text evidence for before-choice, choice-available, action-result, and surrounding-loop-unbroken states.
- Placeholder validator.
- Standalone Windows64 build if the Unity CI workflow runs it.
- Exact-head Unity Foundation CI before merge, and post-merge main CI after merge.

## Ambiguity Check

Status: PASS.

Human-approved answers recorded 2026-07-02:

1. Terse approval `approved` approves the recommended Tactical role counterplay and combat decision readability direction from `production/planning/next-implementation-direction-brief-2026-07-02.md`.
2. The first implementation packet is `STORY-TAC-ROLE-001 Tactical Role Counterplay Readability Smoke`.
3. Codex may select the lowest-risk one-pattern implementation from existing tactical surfaces after reading current code, but must keep it to exactly one tactical decision pattern and document that choice.
4. Prototype labels/markers are allowed if state-backed, tested, player-facing, and listed as temporary.
5. Broader tactical AI, full cover/LOS/overwatch, balance, new unit families, strategic economy, campaign/meta, dirty-information, and Champion progression remain out of scope.

## Branch / PR requirements

- Branch name: `story/STORY-TAC-ROLE-001-tactical-role-counterplay-readability-smoke`.
- PR title: `STORY-TAC-ROLE-001 tactical role counterplay readability smoke`.
- Required linked story ID: `STORY-TAC-ROLE-001`.
- Required evidence path: `production/evidence/STORY-TAC-ROLE-001/`.
- Required evidence summary: chosen pattern, tests run, evidence path, exact-head CI URL placeholder until PR CI runs, and omissions/deferred work.
- Required omissions section: explicitly list known omissions/stubs/placeholders/deferred work or state `No known omissions`.
- Codex must commit and push the implementation branch to remote, or clearly explain why it stopped without pushing.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source sections are linked.
- [x] Exact ADR/architecture/control-manifest source is linked.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied or guarded.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined.
- [x] Ambiguity Check status is PASS.
- [x] Human approval recorded.

## DONE gate

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, validators, and PlayMode/smoke evidence pass, or human-approved exceptions are documented.
- [ ] No unauthorized design or architecture decisions were introduced.
- [ ] Omissions/stubs/mocks/deferred work are explicitly documented.
- [ ] PR/code review is complete.
- [ ] CI passes or human-approved exceptions are documented.
