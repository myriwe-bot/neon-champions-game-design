---
title: STORY-CHAMP-OPS-001 Champion Asset Slot and Prototype Operation On-Ramp
type: story
status: ready
phase: production
owner: shared
created: 2026-06-29
updated: 2026-06-29
source_lore: [champions, digital-net, greenland, white-sky]
related:
  [
    production/epics/epic-vslice-mvp-011-champion-assets-and-operations-depth,
    production/planning/next-implementation-direction-brief-2026-06-29,
    design/gdd/strategic-map,
    design/gdd/intel-resource,
    design/gdd/tactical-combat/champion-operations-and-progression,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-CHAMP-OPS-001 Champion Asset Slot and Prototype Operation On-Ramp

## Status

READY / approved for Unity implementation. Human approval recorded 2026-06-29: "Approved". This approves the Champion Assets / Operations direction from `production/planning/next-implementation-direction-brief-2026-06-29.md` and this first narrow implementation packet.

## Story type

Strategic UX + domain/presentation on-ramp with PlayMode evidence.

## Parent / context

Parent: `EPIC-VSLICE-MVP-011 Champion Assets and Operations Depth`.

The immediate goal is not a full Champion inventory or spellbook. The goal is a first visible strategic Champion asset/operation surface that proves Champions can project non-magical operational leverage on the map using existing prototype resource/Command/Intel language.

## Player/design value

As a player, I need the selected Champion to show at least one prepared operational asset and one readable operation option so Champions start feeling like command/legitimacy actors with assets and leverage, not only army carriers.

## Source authority

Required sources:

- `production/planning/next-implementation-direction-brief-2026-06-29.md` — approved direction and first-slice boundary.
- `production/epics/epic-vslice-mvp-011-champion-assets-and-operations-depth.md` — parent scope and exclusions.
- `design/gdd/tactical-combat/champion-operations-and-progression.md` §§29-80 — Marshal/Operator poles, Command, Operations, Doctrine framing.
- `design/gdd/tactical-combat/champion-operations-and-progression.md` §§98-198 — Command economy, Operation cadence, and channel vocabulary.
- `design/gdd/intel-resource.md` — existing Intel resource language and prior placeholder spend precedent.
- `design/gdd/strategic-map.md` — current Champion/map/site/HUD boundaries.
- `docs/architecture/control-manifest.md`, `docs/architecture/testing-strategy.md`, `docs/architecture/ci-build-automation.md`.

Source authority note: the Champion Operations split article remains draft/pending in front matter, but human approval for EPIC-011 authorizes the cited sections only for this bounded story. Do not use that article to implement full Champion progression, inventory, skill trees, loadouts, Bio/Echo channels, or final balance.

## In scope

- Add a minimal presentation/runtime surface for the active Champion that shows:
  - one prototype command-layer Asset slot or prepared Asset label;
  - one prototype Operation option tied to that Asset;
  - a player-facing cost/availability summary using existing resource/Command/Intel language;
  - a short result/feedback text after the operation is previewed or applied.
- Implement exactly one small strategic prototype Operation, preferably a scouting/forecast/marking operation that affects current map readability rather than combat rules. Acceptable effect examples:
  - mark a nearby guarded site or route as "forecasted" / "scouted" for the current turn;
  - reveal/forecast existing defender/context text already derivable from current scenario state;
  - add a temporary operation marker/status to the selected Champion/site/route presentation.
- Use existing resources/state where practical. A narrow one-time or per-turn cost may use existing Intel/Command-like counters, but do not create a new resource economy.
- Add validation so unavailable/insufficient/duplicate operation use fails cleanly without partial mutation.
- Add focused EditMode or equivalent tests for presentation/state/validation logic.
- Add PlayMode smoke/evidence showing the operation option, cost/availability, and visible result.
- Capture evidence under Unity `production/evidence/STORY-CHAMP-OPS-001/`.

## Out of scope

- Full Champion asset inventory, equipment slots, drag/drop UI, rarity, tiers, upgrades, dismantling, transfer, loss on defeat, or loot rules.
- Full Operations spellbook, operation loadout preparation, multiple Operations, cooldown system, reaction windows, counter-operations, or round cadence rules.
- New resources, Intel subtypes, new income, markets, dirty information/fog-of-war, misinformation, blackmail, feed pollution, legitimacy, or PR systems.
- New map topology, new sites/routes/objectives, new factions/units, new tactical combat mechanics, damage/action rules, AI, win/loss rules, final art/audio/VFX/icons/localization/accessibility framework.
- Final content naming. Prototype labels are acceptable and must be marked as prototype.

## Acceptance criteria

- [ ] Active Champion UI/status shows a clearly labeled prototype Asset/Operation surface.
- [ ] The operation option is visible in player-facing language, with cost/availability and a short explanation.
- [ ] Applying or previewing the operation produces a visible strategic-map result/feedback without entering tactical combat or changing victory rules.
- [ ] Insufficient/unavailable/duplicate operation attempts are rejected with clear diagnostics/feedback and no partial mutation.
- [ ] Existing strategic movement, site interaction, resource HUD, objective, and tactical handoff smokes continue to pass.
- [ ] Evidence under Unity `production/evidence/STORY-CHAMP-OPS-001/` includes notes/screenshots for the operation option, cost/availability, result feedback, and any omissions.
- [ ] Exact-head Unity Foundation CI passes before merge.

## Verification requirements

Required unless a blocker is documented in PR evidence:

- `git diff --check`.
- Focused EditMode tests for any application/domain/presentation snapshot or validation changes.
- PlayMode smoke test or generated PNG/text evidence for the strategic UI path.
- Placeholder validator.
- Standalone Windows64 build if the Unity CI workflow runs it.
- Exact-head Unity Foundation CI before merge, and post-merge main CI after merge.

## Ambiguity Check

Status: PASS.

Human-approved assumptions:

- `Approved` means approve the recommended Champion Assets / Operations direction from the 2026-06-29 decision brief.
- The first implementation packet is `STORY-CHAMP-OPS-001 Champion Asset Slot and Prototype Operation On-Ramp`.
- The first operation should prove a visible strategic Champion operation/asset surface, not a full spellbook or inventory.
- Prototype labels are acceptable if clearly not canon/final.
- The operation may use existing Intel/Command language but must not invent a new economy.

## Branch / PR requirements

- Branch name: `story/STORY-CHAMP-OPS-001-champion-asset-operation-on-ramp`.
- PR title: `STORY-CHAMP-OPS-001 champion asset operation on-ramp`.
- Required linked story ID: `STORY-CHAMP-OPS-001`.
- Required evidence path: `production/evidence/STORY-CHAMP-OPS-001/` in Unity.
- Required omissions section: explicitly list deferred asset/operation systems or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent/context.
- [x] User/player/system value is clear.
- [x] Source authority and narrow source-authority exception are explicit.
- [x] In-scope and out-of-scope are bounded.
- [x] Acceptance criteria are observable.
- [x] Verification requirements are defined.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Ambiguity Check status is PASS.
- [x] Human approval has been recorded.

## DONE gate

- [ ] Implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required evidence exists.
- [ ] Required tests/CI pass, or human-approved exceptions are documented.
- [ ] PR/code review is complete if a Unity PR is opened.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY / approved for Unity implementation. Runnable Codex prompt prepared at `production/sprints/codex-story-champ-ops-001.prompt.txt`.
