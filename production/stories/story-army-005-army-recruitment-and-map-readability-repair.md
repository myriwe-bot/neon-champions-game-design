---
title: STORY-ARMY-005 Army, Recruitment, and Map Readability Repair
type: story
status: ready
phase: production
owner: shared
created: 2026-06-25
updated: 2026-06-25
source_lore: [greenland, qxz-meridian, white-sky]
related:
  [
    production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity,
    production/planning/epic-008-faction-armies-recruitment-and-role-identity-plan,
    production/planning/strategic-map-realism-brief-2026-06-25,
    production/stories/story-army-001-mvp-faction-unit-definitions-and-roster-seed,
    production/stories/story-army-002-tactical-role-behaviors-and-sensor-lock,
    production/stories/story-army-003-fixed-recruitment-offers-and-army-summary,
    production/stories/story-army-004-composition-consequence-scenario,
    production/stories/story-qa-009-epic-008-playtest-and-closeout-review,
    design/gdd/strategic-map,
    design/gdd/tactical-combat,
    design/gdd/faction-unit-rosters,
    design/research/homm-like-tactical-battle-ui-reference,
    design/research/homm-like-strategic-map-topology-reference,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-ARMY-005 Army, Recruitment, and Map Readability Repair

## Status

READY / approved. Human approval recorded 2026-06-25: approve `STORY-ARMY-005` with a strategic-map selected-Champion hero bar, fixed Tier-1-style recruitment clarity, tactical stack labels/details, map panning, and a realistic-map brief in parallel. This story is a repair after human playtest rejected EPIC-008 closeout.

## Story type

UI / Playability Repair / Strategic + Tactical Readability.

## Parent epic

- [EPIC-VSLICE-MVP-008 Faction Armies, Recruitment, and Tactical Role Identity](../epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md)

## User/player/system value

As a player, I need to see my selected Champion, army stacks, recruitment result, tactical stack identities, and navigable map focus clearly enough to judge whether recruitment and army composition matter.

## Closeout rejection source

Human playtest rejected EPIC-008 closeout with these concrete blockers, which are implementation authority for this repair:

- “The UI is still hard to read.”
- “A darker hue permeates the top part of the screen, including where objectives are.”
- “The map cannot be moved, which makes it annoying to focus on a specific area. It should be scrollable in the near future.”
- “Actually, we should move to a more realistic map and work on that quite soon.”
- “I do not understand where I can see my army, what it does, what units do and what units I have. The UI is very very cluttered.”
- “I do not understand what types of units I can recruit.”
- “The dwelling does not give any information in addition to ‘recruited’ status.”
- “I have no idea how to see different types of stacks and units. I do not understand what tactical roles would do. I do not understand that they even exist.”
- “I would not know how to create a composition or how to view it, so no. It is completely unreadable right now.”
- “Everything to do with army. Also, what abilities the hero has etc.”

## Source requirements

Exact source references:

- `production/stories/story-qa-009-epic-008-playtest-and-closeout-review.md` for the closeout-review contract and prior `CLOSE EPIC` recommendation that is now superseded by human playtest rejection.
- `production/epics/epic-vslice-mvp-008-faction-armies-recruitment-and-tactical-role-identity.md` for faction armies, recruitment, tactical role identity, and EPIC-008 DONE gate.
- `production/planning/epic-008-faction-armies-recruitment-and-role-identity-plan.md` for the EPIC-008 repair train update.
- `production/stories/story-army-001-mvp-faction-unit-definitions-and-roster-seed.md` for approved unit IDs/names/count defaults and faction buckets.
- `production/stories/story-army-002-tactical-role-behaviors-and-sensor-lock.md` for role/Sensor Lock behavior that must become more readable and must not regress.
- `production/stories/story-army-003-fixed-recruitment-offers-and-army-summary.md` for fixed offer, offer consumption, army summary, and recruited-composition handoff behavior.
- `production/stories/story-army-004-composition-consequence-scenario.md` for composition-consequence proof that is not judgeable until this readability repair lands.
- `design/gdd/strategic-map.md` §§2-8 and §§10-13 for selected Champion, site interaction, recruitment, movement, tactical handoff, and strategic UI expectations.
- `design/gdd/tactical-combat.md` §§3-6.7 for stack combat, labels, role readability, actions, statuses, and tactical HUD expectations.
- `design/gdd/faction-unit-rosters.md` for MVP faction unit names, roles, and naming guardrails.
- `design/research/homm-like-tactical-battle-ui-reference.md` for stack-count/label/action readability reference.
- `design/research/homm-like-strategic-map-topology-reference.md` for HoMM-like map/dwelling reference; reference only, not authority for broad topology replacement.
- `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
- `docs/architecture/testing-strategy.md`.
- `docs/architecture/ci-build-automation.md`.

## In scope

Concrete implementation target:

- Add or repair a selected-Champion strategic-map bottom **hero bar** that persists while that Champion is selected.
- Hero bar must show, using available data and placeholders where needed:
  - Champion/hero name;
  - class/archetype if available, otherwise clear placeholder like `Class: prototype` rather than blank ambiguity;
  - level if available, otherwise clear placeholder like `Level: prototype` if no level system exists;
  - army stack slots for the currently selected Champion only;
  - each stack's unit name, count, and compact role hint.
- Stack slots must be clickable/selectable if small and safe. If rearranging stacks is not small/safe, show a clearly non-fake deferred affordance or omit drag/reorder rather than pretending it works.
- Repair recruitment-site preview/result copy so the player can understand what joins:
  - prototype uses HoMM3 Tier-1-style fixed recruitment clarity, e.g. “20 Settlement Watch join your army.”
  - text must show exact unit name and count before or at recruitment and exact army change after recruitment.
  - do not hard-code fixed joiners as the only future dwelling type.
- Preserve future dwelling extensibility in code/data shape where practical:
  - future fixed joiners;
  - purchasable units;
  - variable quantities;
  - costs/resources;
  - upgraded or conditional offers.
- Add tactical compact labels always visible enough to distinguish different stacks:
  - unit/stack name or readable short name;
  - count;
  - compact role hint/icon/text.
- Add selected-stack detail surface where practical:
  - role;
  - basic action purpose;
  - relevant status such as Sensor Lock / Marked if present.
- Add strategic map panning/scrolling sufficient to focus on a specific area.
- Add basic camera bounds or equivalent guardrails so panning does not break scene framing.
- Fix the dark top-screen hue/objective contrast issue if small and directly tied to this readability pass.
- Add focused tests and PlayMode/PNG evidence under `production/evidence/STORY-ARMY-005/`.

## Out of scope

Not authorized by this story:

- No full realistic map replacement, terrain/geography rewrite, tile/hex topology, procedural map, map editor, or final map art.
- No full dwelling economy, weekly growth/stock refresh, construction tree, town screen, market, resource economy, or choose-quantity purchase flow.
- No full stack management system; stack rearrangement is optional only if small/safe and must not expand scope.
- No deep hero leveling/class/progression system; display existing/prototype values only.
- No new unit roster rows, balance pass, upgraded unit variants, new tactical mechanics, tactical AI expansion, or new Sensor Lock rules.
- No final art/icons/VFX/audio/animation/localization pass.
- No hard-canon rename of Home Rule Coalition.

## Allowed stubs, mocks, placeholders, or temporary data

- Prototype hero class/level display may use explicit placeholder values if no real system exists yet.
- Placeholder icons/role text are allowed if readable and deterministic.
- A non-functional stack reorder affordance is not allowed. If reordering is not implemented, communicate that it is deferred or simply make slots selectable only.
- Fixed Tier-1-style recruitment copy is allowed for this prototype, but code/data should avoid making it the only possible future dwelling mode when cheap to preserve flexibility.

## Dependencies

- `STORY-ARMY-001` DONE / merged.
- `STORY-ARMY-002` DONE / merged.
- `STORY-ARMY-003` DONE / merged.
- `STORY-ARMY-004` DONE / merged.
- `STORY-QA-009` DONE / merged, then superseded by human playtest rejection.
- Existing strategic map, Champion selection, recruitment site, army summary, tactical stack setup/labels, and Unity Foundation CI.

## Acceptance criteria

- [ ] Given a Champion is selected on the strategic map, a bottom hero bar remains visible for that selected Champion and shows name, class/archetype or explicit placeholder, level or explicit placeholder, and current army stack slots.
- [ ] Given the selected Champion has army stacks, each stack slot communicates unit name, count, and compact role hint.
- [ ] Given a recruitment site/dwelling can be used, the UI communicates the exact fixed prototype joiner before or at recruitment, including unit name and count.
- [ ] Given recruitment succeeds, the feedback states the exact stack/unit added or changed rather than only saying “recruited”.
- [ ] Given the player returns to army view after recruiting, the hero bar/army slots visibly reflect the changed composition.
- [ ] Given tactical combat starts with multiple stack types, compact labels make different stack/unit types distinguishable without selection.
- [ ] Given a tactical stack is selected, a detail surface explains its role/basic action purpose and relevant status if present.
- [ ] Given the strategic map is larger than the viewport/focus area, the player can pan/scroll/move focus enough to inspect a specific area without losing core HUD context.
- [ ] Given the top objective area is visible, the dark hue/contrast issue no longer prevents reading the objective.
- [ ] Existing recruitment, army composition handoff, tactical role/Sensor Lock behavior, battle handoff/return, objective state, and existing PlayMode smoke paths do not intentionally regress.
- [ ] Evidence explicitly addresses the human complaints about army visibility, recruitment clarity, tactical-role visibility, map panning, and top-objective readability.

## Verification requirements

- Unit/EditMode tests: required for any new formatting/projection helpers, recruitment preview/result strings, army snapshot/slot projection, and no-regression of recruitment handoff where practical.
- PlayMode/smoke tests: required for selected-Champion hero bar, recruitment preview/result, tactical labels/detail surface where practical, and map panning/focus behavior.
- Screenshot/video evidence: required PNG evidence under `production/evidence/STORY-ARMY-005/` showing hero bar, recruitment preview/result, changed army, tactical labels/details, panning/focus, and improved objective contrast.
- Performance budget or N/A: N/A; UI projection and panning must remain deterministic and cheap.
- CI evidence: Unity Foundation CI exact-head before merge.
- TDD evidence required? Yes for new projection/formatting/domain-adjacent behavior where practical.

## Ambiguity Check

Status: PASS.

Human-approved answers recorded 2026-06-25:

1. Recruitment clarity uses HoMM3 Tier-1-style fixed recruitment for this prototype slice, but future dwelling types must allow fixed joiners, purchasable units, variable quantities, costs/resources, and upgraded or conditional offers.
2. Strategic army display uses a bottom selected-Champion hero bar with persistent-in-strategic-view visibility while that Champion is selected; it shows hero name, class/archetype, level, and stack slots. Stack slots should be clickable and eventually rearrangeable; rearrangement is optional only if small/safe in this repair story.
3. Tactical stack readability uses compact labels always and detailed info on select.
4. Map panning is included in this repair story.
5. A realistic-map design brief starts in parallel, but realistic map implementation is not authorized by this story.

Approved assumptions:

- This is a readability/playability repair, not a new feature epic.
- Placeholder hero class/level values are acceptable if explicit and not presented as final systems.
- Exact wording may be implementation-owned if it satisfies the acceptance criteria and preserves the approved meaning.

Human-approved exceptions:

- `design/gdd/faction-unit-rosters.md` is still draft/pending overall, but its existing MVP unit names, faction buckets, and role hints already used by ARMY-001..004 are approved only as bounded source context for this readability repair. This does not approve broader roster canon, balance, upgrades, or additional faction content.
- Map panning is allowed inside this army/recruitment readability repair because the human identified inability to focus the current map as part of the failed playtest readability gate.
- Top objective contrast may be fixed if small and directly tied to readability.

If status is FAIL, this story is not READY.

## Branch / PR requirements

- Branch name: `story/STORY-ARMY-005-army-recruitment-map-readability-repair`.
- PR title: `STORY-ARMY-005 Army recruitment and map readability repair`.
- Required linked story ID: `STORY-ARMY-005`.
- Required linked GDD/ADR/control docs:
  - `design/gdd/strategic-map.md`.
  - `design/gdd/tactical-combat.md`.
  - `design/gdd/faction-unit-rosters.md`.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- Required root/scoped AGENTS.md instructions: read Unity root `AGENTS.md` plus scoped AGENTS files for every touched Runtime/Application/Presentation/Tests/Evidence directory.
- Required evidence summary: tests run, PlayMode/PNG evidence path, CI run URL.
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
- [ ] Required automated tests, validators, PlayMode/smoke evidence pass, or human-approved exceptions are documented.
- [ ] No unauthorized design or architecture decisions were introduced.
- [ ] Omissions/stubs/mocks/deferred work are explicitly documented.
- [ ] PR/code review is complete.
- [ ] CI passes or human-approved exceptions are documented.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY for Unity implementation. This is the only current approved Unity implementation packet. The parallel realistic-map brief is design-only and does not authorize map replacement implementation.
