---
title: STORY-ARMY-004 Composition Consequence Scenario
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-06-19
updated: 2026-06-19
source_lore: [greenland, qxz-meridian, white-sky]
related:
  [
    production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity,
    production/planning/epic-008-faction-armies-recruitment-and-role-identity-plan,
    production/stories/story-army-001-mvp-faction-unit-definitions-and-roster-seed,
    production/stories/story-army-002-tactical-role-behaviors-and-sensor-lock,
    production/stories/story-army-003-fixed-recruitment-offers-and-army-summary,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    design/gdd/faction-unit-rosters,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: pending
---

# STORY-ARMY-004 Composition Consequence Scenario

## Status

READY-candidate / approval pending. Prepared after `STORY-ARMY-003` merged in Unity PR #64. This is the next EPIC-008 implementation candidate, but it is **not runnable** until human approval promotes it to `status: ready`, `approval: approved`, and Ambiguity Check PASS.

## Story type

Vertical Slice + Tactical/Strategic Integration + Evidence.

## Parent epic

- [EPIC-VSLICE-MVP-008 Faction Armies, Recruitment, and Tactical Role Identity](../epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md)

## User/player/system value

As a player, I want recruited army composition to visibly change a tactical fight and the post-battle strategic result, so recruitment feels like a meaningful strategic choice rather than a cosmetic army list update.

## Source requirements

Exact source references:

- `production/stories/story-army-001-mvp-faction-unit-definitions-and-roster-seed.md` for approved unit IDs/names, default counts, roles, and faction buckets.
- `production/stories/story-army-002-tactical-role-behaviors-and-sensor-lock.md` for role/Sensor Lock behavior that must not regress.
- `production/stories/story-army-003-fixed-recruitment-offers-and-army-summary.md` for fixed offer, consumption, army summary, and recruited-composition handoff behavior.
- `production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md` for composition-consequence scope.
- `production/planning/epic-008-faction-armies-recruitment-and-role-identity-plan.md` Slice D.
- `design/gdd/strategic-map.md` §§2-8 and §§10-13 for strategic loop, site interaction, Champion movement, recruitment, tactical handoff, rewards, and return summary.
- `design/gdd/tactical-combat.md` §§3-6.7 for stack combat, AP, role readability, loss application, and tactical labels.
- `design/gdd/faction-unit-rosters.md` for MVP faction roster names and provisional naming guardrails.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.

## In scope

Concrete implementation target:

- Add or adapt one story-scoped guarded site / tactical encounter in the existing smoke scenario so it demonstrates a meaningful difference between starting composition and recruited/reinforced composition.
- Preserve the ARMY-003 path: recruit fixed offer, inspect army summary, move/engage a guarded site, launch tactical setup with current recruited composition.
- Add a before/after comparison surface in tests/evidence showing that tactical setup/labels differ when the player recruits first vs when they enters the fight with starting composition only.
- Ensure post-battle summary records stack losses, reward/site outcome, and return-to-strategic state for the composition scenario.
- Keep the demonstration narrow and deterministic enough for automated EditMode/PlayMode/smoke coverage.
- Add focused tests plus PNG evidence under `production/evidence/STORY-ARMY-004/`.

## Out of scope

Not authorized by this story:

- No full balance pass, difficulty model, combat simulator, or scenario editor.
- No new unit definitions, new faction roster rows, upgraded variants, or town/economy system.
- No new tactical role behavior beyond preserving ARMY-001/002 roles and ARMY-003 recruitment handoff.
- No strategic AI, campaign progression, death/recovery/revival, or full casualty persistence redesign beyond existing battle result application.
- No final art/icons/VFX/audio/animation.
- No hard-canon rename of Home Rule Coalition.

## Allowed stubs, mocks, placeholders, or temporary data

- Scenario tuning may use story-scoped prototype site/guard counts if IDs are stable and documented.
- Evidence may compare deterministic test paths rather than full manual free-play balance.
- UI may use existing text-only HUD/snapshot/event-feed surfaces.
- If exact win/loss tuning would require a broader balance pass, prefer a narrow deterministic assertion that recruited composition changes tactical setup, loss summary, or reward path rather than widening scope.

## Dependencies

- `STORY-ARMY-001` DONE / merged.
- `STORY-ARMY-002` DONE / merged.
- `STORY-ARMY-003` DONE / merged.
- Existing recruitment fixed offers, army summary, tactical setup, battle result application, guarded-site interaction, PlayMode evidence capture, and Unity Foundation CI.

## Acceptance criteria

- [ ] A deterministic scenario path exists for fighting with starting composition only.
- [ ] A deterministic scenario path exists for recruiting first, then fighting with changed composition.
- [ ] Tactical setup/labels visibly differ between the starting-only and recruited-composition paths.
- [ ] Post-battle summary records losses and site/reward outcome for the composition scenario.
- [ ] Return-to-strategic state after the battle remains visible and does not regress ARMY-003 recruitment/summary behavior.
- [ ] Existing movement, recruitment, offer consumption, Sensor Lock, tactical role labels, AP, retaliation, CombatAI, and battle handoff behavior do not regress.
- [ ] Evidence documents the comparison, tactical setup/labels, post-battle summary, and deferred full balance/scenario-editor depth.

## Verification requirements

- Unit/EditMode tests: required for deterministic starting-only vs recruited-composition setup, post-battle summary/loss outcome, and no-regression of ARMY-003 offer state.
- PlayMode/smoke tests: required for visible recruit -> fight -> result/return path where practical.
- Screenshot/video evidence: required PNG evidence under `production/evidence/STORY-ARMY-004/` showing starting-only setup, recruited setup, and post-battle/return summary.
- Performance budget or N/A: N/A.
- CI evidence: Unity Foundation CI exact-head before merge.
- TDD evidence required? Yes for deterministic composition comparison and result/return state.

## Ambiguity Check

Status: FAIL / approval pending.

Open approval questions before READY:

1. What should ARMY-004 prove first?
   - Recommended: a narrow Home Rule path where `settlement_watch` recruitment changes the guarded-site tactical setup and post-battle loss/reward summary.
2. Should the comparison require different battle outcomes, or only different setup/loss pressure?
   - Recommended: require visible setup/label/loss-summary difference, not guaranteed victory/loss tuning.
3. Which encounter should be used?
   - Recommended: adapt the existing guarded-site path if small; otherwise create one story-scoped guarded composition-demo site.
4. Should QXZ get a mirrored composition proof now?
   - Recommended: defer mirrored QXZ proof to QA/closeout unless cheap; keep ARMY-004 focused on one deterministic path.

Human-approved exceptions:

- None yet.

## Branch / PR requirements

- Branch name after approval: `story/STORY-ARMY-004-composition-consequence-scenario`
- PR title after approval: `STORY-ARMY-004 Composition consequence scenario`
- Required linked story ID: `STORY-ARMY-004`.
- Required evidence summary: tests run, PNG evidence path, CI run URL.
- Required omissions section: explicitly list known omissions/stubs/placeholders/deferred work or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked or explicitly N/A.
- [x] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [x] Relevant root/scoped AGENTS.md instructions are identified.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed.
- [ ] Ambiguity Check status is PASS.
- [ ] Human approval recorded.

## DONE gate

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required verification evidence exists.
- [ ] Required automated tests, validators, and PlayMode/smoke evidence pass, or human-approved exceptions are documented.
- [ ] No unauthorized design or architecture decisions were introduced.
- [ ] Omissions/stubs/mocks/deferred work are explicitly documented.
- [ ] PR/code review is complete.
- [ ] CI passes or human-approved exceptions are documented.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY-candidate / approval pending. Do not run Codex until the Ambiguity Check is approved and the story is promoted to READY.
