---
title: STORY-CMD-001 Champion Command Archetype State and Tactical HUD
type: story
status: done
phase: production
owner: shared
created: 2026-06-13
updated: 2026-06-13
source_lore: [champions]
related:
  [
    design/gdd/tactical-combat,
    design/gdd/tactical-combat/champion-operations-and-progression,
    design/gdd/strategic-map,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
    production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp,
  ]
approval: approved
---

# Story: STORY-CMD-001 Champion Command Archetype State and Tactical HUD

## Status

DONE / merged. Unity PR #40 implemented and merged on 2026-06-13 after CI and review passed. Human-approved source-authority exception and profile values are recorded below.

This is the first proposed child story for `EPIC-VSLICE-MVP-005`. It establishes minimal Champion Command state and tactical visibility for both requested archetype poles: Marshal-like and Operator-like Champions. It does **not** yet implement active command spending.

## Story type

Tactical Domain + UI/Integration + PlayMode Smoke.

## Parent epic

- Epic ID/path: `production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp.md`

## User/player/system value

As a player, I want the tactical screen to show that my Champion has a command identity and finite battle-level Command, so that Champions start feeling like commanders with different roles rather than anonymous stack carriers.

## Source requirements

- GDD path + section/rule:
  - `design/gdd/tactical-combat/champion-operations-and-progression.md` §§29-80 for Marshal/Operator poles and Command/Operations/Doctrine definitions.
  - `design/gdd/tactical-combat/champion-operations-and-progression.md` §§98-130 for finite per-battle Command direction.
  - `design/gdd/strategic-map.md` §§6, 7, 14 for Champion strategic state and strategy-to-tactical handoff context.
- ADR / architecture section / control-manifest rule:
  - `docs/architecture/control-manifest.md` §§1, 2, 4, 5, 6, 7, 9, 10.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.
- UX/content/art rule, if applicable:
  - Temporary text labels are allowed; no final icons/art required.
- Parent epic:
  - `production/epics/epic-vslice-mvp-005-champion-command-and-operations-on-ramp.md`.

Source-authority decision: human-approved narrow implementation-source exception. The Champion Operations split article has draft/pending front matter, but this story may use the cited sections for Marshal/Operator poles, Command, Operations, Doctrine, primary stat scopes, and the barebones profile contract only.


## Design decision: Marshal vs Operator governance

This story deliberately does **not** define Command as generic military authority. It follows the active Champion Operations design notes:

- **Command** is the Knowledge analogue. It governs starting Command pool and prepared Operation loadout/flexibility. Operators tend to have more of it.
- **Control** is the Spell Power analogue. It governs Operation strength, duration, radius, reliability, penetration, or similar per Operation. Operators lean into it.
- **Marshals** are governed mainly by Attack, Defense, Logistics, Doctrine, Cohesion reliability, and Minor Command capacity.
- **Operators** are governed mainly by Command, Control, prepared Major Operation slots, and operation-channel access.

Barebones implementation contract for CMD-001:

| Profile | Starting Command | Major Operation Slots | Minor Command Capacity | Control Scalar | Doctrine Scalar |
| --- | ---: | ---: | ---: | ---: | ---: |
| `marshal_alpha` | 2 | 0 | 2 | 0 | 1 |
| `operator_alpha` | 3 | 1 | 0 | 1 | 0 |

CMD-001 only implements data/state/HUD visibility for these values. It must not add active command spending or effects.

## In scope

- Add minimal Champion command profile/state sufficient to distinguish:
  - Marshal-like profile.
  - Operator-like profile.
- Add finite per-battle Command value/state for tactical encounters.
- Propagate command profile/state from strategic/tactical setup into tactical runtime state, using existing architecture boundaries.
- Show Champion command profile and current/maximum Command in the tactical HUD/status text.
- Add deterministic placeholder assignment for the current two Champions/factions if technically clean.
- Add tests proving state initialization, propagation, serialization/snapshot behavior where applicable, and HUD/status output.
- Add PlayMode evidence showing at least one Marshal-like and one Operator-like tactical encounter state, or one deterministic smoke that covers both profiles if simpler.

## Out of scope

- No active Command spend/action yet.
- No Marshal command effect.
- No Operator operation effect.
- No full Operations list/spellbook.
- No Champion levels, skill tree, Doctrine/passive system, perks, equipment, or inventory.
- No Command regeneration, cooldown, per-round operation cadence, reactions, interrupts, or targeting UI.
- No final Champion class names, final lore copy, icons, portraits, animations, VFX, or audio.
- No Intel integration or Field Upgrade replacement.
- No faction balance claims.

## Allowed stubs, mocks, placeholders, or temporary data

- Placeholder command profile IDs/labels are approved: `marshal_alpha` / “Marshal” and `operator_alpha` / “Operator”.
- Prototype profile values are approved for this story only:
  - `marshal_alpha`: Starting Command 2, Major Operation Slots 0, Minor Command Capacity 2, Control Scalar 0, Doctrine Scalar 1.
  - `operator_alpha`: Starting Command 3, Major Operation Slots 1, Minor Command Capacity 0, Control Scalar 1, Doctrine Scalar 0.
- Existing placeholder Champions/factions may be mapped to profiles for this story only.

## Dependencies

- Required prior stories:
  - EPIC-004 child stories DONE / merged.
  - Tactical battle setup and HUD/presentation infrastructure from prior tactical stories.
- Required data/assets:
  - Placeholder IDs/text only.
- Required architecture decisions:
  - Existing Unity technical scheme and control manifest.
- Required Unity/package setup:
  - Existing Unity Foundation CI.

## Acceptance criteria

- [ ] Given a tactical battle setup for a Marshal-like Champion, when tactical state is initialized, then the tactical state contains `marshal_alpha`, Starting Command 2, Major Operation Slots 0, Minor Command Capacity 2, Control Scalar 0, and Doctrine Scalar 1.
- [ ] Given a tactical battle setup for an Operator-like Champion, when tactical state is initialized, then the tactical state contains `operator_alpha`, Starting Command 3, Major Operation Slots 1, Minor Command Capacity 0, Control Scalar 1, and Doctrine Scalar 0.
- [ ] Given tactical HUD/status rendering, when a battle starts, then the visible tactical status identifies the Champion command profile, current/maximum Command, Major Operation Slots, and Minor Command Capacity.
- [ ] Given invalid or missing command profile data, when validation/factory code processes it, then it fails safely or falls back only through an explicitly tested placeholder default without crashing or partial mutation.
- [ ] Given this story has no active command spending, when the player interacts with existing tactical controls, then no new command action can be triggered.

## Verification requirements

- Unit tests: command profile/value validation helpers if pure domain logic is added.
- Unity edit-mode tests: BattleSetup/tactical state propagation and invalid/missing profile cases.
- Unity play-mode tests: HUD/status displays command profile and Command values in tactical mode.
- Integration/data validation tests: required if command profiles are authored in scenario/data definitions.
- Manual Unity scene/prefab checks: N/A unless scene/prefab edits are required; prefer code/test changes.
- Screenshot/video evidence: PNG evidence of tactical HUD/status with Command/profile visible.
- Performance budget or N/A: N/A; small state/UI text only.
- CI evidence: Unity Foundation CI exact-head required before merge.
- Playtest evidence, if applicable: N/A for this first state/HUD story.
- TDD evidence required? Yes for production logic and bug fixes.
- Automation deferred? No.

## Ambiguity Check

Status: PASS

Open questions:

- None for CMD-001 implementation.

Assumptions:

- Marshal and Operator are archetype poles, not final rigid classes.
- This story may show both profiles without implementing active commands.

Out of scope:

- Active command spend and command effects.
- Final class/progression design.

Allowed stubs/mocks:

- Placeholder profile IDs/labels and prototype Command values.

Human-approved exceptions:

- Narrow source-authority exception approved for cited Champion Operations sections despite draft/pending front matter.
- Prototype barebones profile values approved for CMD-001 only.

## Branch / PR requirements

- Branch name: `story/STORY-CMD-001-champion-command-archetype-state-hud`
- PR title: `STORY-CMD-001 Champion Command archetype state and tactical HUD`
- Required linked story ID: `STORY-CMD-001`
- Required linked GDD/ADR/control docs: tactical combat Champion Operations sections, strategic map handoff sections, control manifest, testing strategy, CI automation.
- Required root/scoped AGENTS.md instructions: Unity root plus scoped files touched.
- Required evidence summary: tests, PlayMode evidence, CI run URLs, omissions.
- Required omissions section: must state known omissions or `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Exact GDD source section is linked or explicitly N/A with approved exception.
- [x] Exact ADR/architecture/control-manifest source is linked or explicitly N/A.
- [x] Relevant root/scoped AGENTS.md instructions are identified or explicitly N/A.
- [x] UX/content/art/worldbuilding references are linked if relevant.
- [x] In-scope work is concrete and bounded.
- [x] Out-of-scope work is explicit.
- [x] Stubs/mocks/placeholders are explicitly listed.
- [x] Dependencies are listed and satisfied or marked blocking.
- [x] Acceptance criteria are observable and testable.
- [x] Verification requirements are defined according to `docs/architecture/testing-strategy.md`.
- [x] Required automated tests/validators/PlayMode evidence are listed, or approved exceptions are documented.
- [x] Ambiguity Check status is PASS.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Human approval has been given or delegated gate approval is recorded.

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

## Verdict

DONE / merged. Implemented barebones Marshal/Operator command profile state and tactical HUD visibility only; no active command spending or effects.


## Implementation evidence

- Unity PR: https://github.com/myriwe-bot/neon-champions-unity/pull/40
- Branch head reviewed: `d338529376acc10ab353736eea61eee7f0427da6`
- Merge commit on main: `804fe7db8b9f2426706cc614b099383493747df2`
- PR CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27463253643
- Post-merge main CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/27463585232
- Required jobs passed: Compile / Standalone Check, EditMode Tests, PlayMode Smoke Tests, Placeholder Validator.
- Review verdict: PASS, recorded on PR.
- Omissions/deferred: no active command spending/effects, no skill trees, no Doctrine mechanics, no full operation list, no progression, no final art/lore/UI, no Intel integration, no faction balance.
