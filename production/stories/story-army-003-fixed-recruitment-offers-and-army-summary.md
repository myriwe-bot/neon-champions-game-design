---
title: STORY-ARMY-003 Fixed Recruitment Offers and Army Summary
type: story
status: ready
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
    design/gdd/faction-unit-rosters,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-ARMY-003 Fixed Recruitment Offers and Army Summary

## Status

READY / approved. Human approval recorded 2026-06-19 from chat: `Approved`, approving the recommended defaults listed in the candidate Ambiguity Check. Prepared after `STORY-ARMY-002` merged in Unity PR #61.

## Story type

Strategic Rules + UI + Tactical Setup Integration.

## Parent epic

- [EPIC-VSLICE-MVP-008 Faction Armies, Recruitment, and Tactical Role Identity](../epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md)

## User/player/system value

As a player, I want starting hubs and one neutral recruitment site to add fixed unit stacks to my army and show my current composition, so recruitment starts affecting tactical battles instead of unit identity living only inside test setups.

## Source requirements

Exact source references:

- `production/stories/story-army-001-mvp-faction-unit-definitions-and-roster-seed.md` for approved unit IDs/names and faction buckets.
- `production/stories/story-army-002-tactical-role-behaviors-and-sensor-lock.md` for current role/Sensor Lock behavior that must not regress.
- `production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md` for fixed-offer recruitment scope.
- `production/planning/epic-008-faction-armies-recruitment-and-role-identity-plan.md` Slice C.
- `design/gdd/strategic-map.md` §§2-8 and §§10-13 for local-hotseat strategic map, bases, recruitment/reinforcement, army summary, site interaction, Champion movement, and tactical handoff.
- `design/gdd/faction-unit-rosters.md` for Home Rule / QXZ MVP roster names and provisional naming guardrails.
- `design/gdd/tactical-combat.md` §§3-6.7 for stack-first battle setup and readable tactical roles.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.

## In scope

Concrete implementation target:

- Add fixed recruitment/reinforcement offers at each starting hub:
  - Home Rule starting hub offers `settlement_watch` / Settlement Watch using the unit definition catalog default count.
  - QXZ starting hub offers `meridian_security` / Meridian Security using the unit definition catalog default count.
- Add one neutral recruitment site offering `survey_drones` / Survey Drones if it can be represented on the existing strategic map without expanding topology beyond a small approved site/node addition; otherwise stop and report the scoped blocker rather than substituting an unapproved offer.
- Add an army summary surface on the strategic HUD/snapshot that shows current stack composition by unit display name, count, and faction/owner.
- Applying a valid fixed offer updates the acting faction/Champion army state and is visible before tactical handoff.
- Tactical BattleSetup generation uses the recruited/current army composition rather than always falling back to a single placeholder/default stack where the current architecture supports it.
- Add concrete denial/diagnostic feedback for invalid recruitment attempts: no selected Champion/faction, wrong faction/site, already claimed/consumed fixed offer, invalid unit definition, or unsupported offer target.
- Add focused EditMode and PlayMode/smoke tests plus evidence under `production/evidence/STORY-ARMY-003/`.

## Out of scope

Not authorized by this story:

- No town building tree, dwelling construction, weekly growth, economy loop, market, or resource costs.
- No upgraded variants, full roster expansion, balancing pass, or unit production scheduling.
- No strategic AI recruitment.
- No final art/icons/VFX/audio/animation.
- No new tactical role behavior beyond preserving ARMY-002 behavior.
- No full post-battle casualty persistence redesign beyond using existing current army state where already supported.
- No hard-canon rename of Home Rule Coalition.

## Allowed stubs, mocks, placeholders, or temporary data

- Fixed offers may be hard-authored prototype data if IDs are stable, validated, and story-scoped.
- Neutral recruitment uses `survey_drones` if the existing map/site path supports it without broad topology work; do not substitute `site_guards` without a story update.
- UI may use text-only labels/summaries on existing HUD/snapshot surfaces.
- Offer consumption is one-time for MVP; recurring/weekly recruitment is explicitly deferred.
- Fixed offer stack counts use current MVP default counts from the unit definition catalog unless a smaller proof count is required for readability and is explicitly documented in evidence.

## Dependencies

- `STORY-ARMY-001` DONE / merged.
- `STORY-ARMY-002` DONE / merged.
- Existing strategic map, starting hubs, site interaction, Champion movement, tactical handoff, tactical setup, unit definitions, and Unity Foundation CI.

## Acceptance criteria

- [ ] Starting hub fixed offers are visible and faction-scoped.
- [ ] A valid offer adds the approved unit stack/count to the acting faction/Champion army state.
- [ ] Army summary shows unit display names and counts after recruitment/reinforcement.
- [ ] A recruited/current army composition reaches tactical setup and is visible in tactical labels/evidence.
- [ ] Invalid recruitment attempts fail safely with diagnostics and no partial mutation.
- [ ] One-time consumed offer state prevents duplicate free claims unless the story explicitly documents a narrower accepted model.
- [ ] Existing movement, site interaction, Sensor Lock, tactical role labels, AP, retaliation, CombatAI, and battle handoff behavior do not regress.
- [ ] Evidence documents fixed offers, army summary, tactical handoff, and deferred recruitment economy depth.

## Verification requirements

- Unit/EditMode tests: required for offer validation, valid claim mutation, consumed-state duplicate blocking, army summary state, and BattleSetup composition.
- PlayMode/smoke tests: required for visible offer/summary path and tactical handoff with recruited/current composition where practical.
- Integration/data validation tests: required for unit IDs and fixed offer data.
- Screenshot/video evidence: required PNG evidence under `production/evidence/STORY-ARMY-003/` showing offer visibility, claimed army summary, and tactical handoff/composition.
- Performance budget or N/A: N/A.
- CI evidence: Unity Foundation CI exact-head before merge.
- TDD evidence required? Yes for strategic recruitment state and validation.

## Ambiguity Check

Status: PASS.

Human-approved answers recorded 2026-06-19 from chat: `Approved`:

1. Starting-hub fixed offers:
   - Home Rule hub -> `settlement_watch` / Settlement Watch.
   - QXZ hub -> `meridian_security` / Meridian Security.
2. Neutral recruitment site:
   - Include one neutral `survey_drones` / Survey Drones offer only if the existing map/site path is small; otherwise stop and report the scoped blocker rather than substituting `site_guards`.
3. Claim model:
   - One-time consumed state for each fixed offer. No economy/resource cost in this story.
4. Stack counts:
   - Use current MVP default counts from the unit definition catalog unless implementation must choose smaller proof counts for readability and documents that in evidence.

Human-approved exceptions:

- `design/gdd/faction-unit-rosters.md` remains broader draft/pending, but the exact Home Rule/QXZ/Survey Drones MVP unit IDs and names already approved by ARMY-001 plus the ARMY-003 fixed-offer defaults above are approved as source authority for this story only.

## Branch / PR requirements

- Branch name after approval: `story/STORY-ARMY-003-fixed-recruitment-offers-army-summary`
- PR title after approval: `STORY-ARMY-003 Fixed recruitment offers and army summary`
- Required linked story ID: `STORY-ARMY-003`.
- Required linked GDD/ADR/control docs:
  - `design/gdd/strategic-map.md`.
  - `design/gdd/faction-unit-rosters.md`.
  - `design/gdd/tactical-combat.md`.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: read Unity root `AGENTS.md` plus scoped AGENTS files for touched Runtime/Domain/Application/Presentation/Tests/Evidence directories.
- Required evidence summary: tests run, PlayMode/PNG evidence path, CI URL.
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
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY / approved for Unity implementation. Implement exactly this story scope; do not start ARMY-004 composition-consequence work until a later story is promoted to READY.
