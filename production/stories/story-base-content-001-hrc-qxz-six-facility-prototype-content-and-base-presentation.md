---
title: STORY-BASE-CONTENT-001 HRC/QXZ Six-Facility Prototype Content and Base Presentation
type: story
status: ready
phase: production
owner: shared
created: 2026-07-14
updated: 2026-07-14
approval: approved
related: [production/epics/epic-016-accelerated-playable-product-foundation, design/gdd/prototype-faction-contracts, design/gdd/strategic-map, design/ux/player-shell, design/art/prototype-visual-target-and-asset-ledger, production/stories/story-base-001-base-definition-and-facility-construction-core, production/stories/story-base-002-administration-income-chain-and-recruitment-dwellings]
---

# STORY-BASE-CONTENT-001 HRC/QXZ Six-Facility Prototype Content and Base Presentation

## Value

As an HRC or QXZ player, I want my base to present six faction-specific, understandable facility choices whose construction visibly changes income, recruitment, or existing Champion support, so that the proof build demonstrates meaningful faction identity and base progression rather than placeholder facility IDs.

## Story type and estimate

Content + Strategic Economy Integration + UI/Presentation. Medium story: one bounded implementation packet, expected to reuse existing base/effect/player-shell boundaries rather than introduce a new system.

Performance budget: no measurable regression to the current strategic-shell frame or input responsiveness; facility state is evaluated at base-panel refresh, construction, or active-faction turn boundaries rather than every frame. Existing standalone-build and PlayMode smoke timing is the acceptance baseline.

## Source authority

- `design/gdd/prototype-faction-contracts.md` is authoritative for the approved-provisional HRC/QXZ facility names, functions, contrasts, six-choice breadth, and three-to-four-affordable proof target.
- `design/gdd/strategic-map.md` §§12-16 and completed `STORY-BASE-001` / `STORY-BASE-002` remain authoritative for one build per base per cycle, recurring resources, recruitment offers, runtime state, validation, and strategic/tactical boundaries.
- `design/ux/player-shell.md` governs the normal base-inspection/build flow.
- `design/art/prototype-visual-target-and-asset-ledger.md` governs presentation assets and provenance.

## Proposed prototype mapping and tuning

These implementation values were human-approved on 2026-07-14. They are prototype tuning, not final balance.

| Faction | Facility | Candidate effect | Candidate cost / prerequisite |
|---|---|---|---|
| HRC | Council Office | Starting/prebuilt administration; +5 Credits at active-faction turn start | prebuilt baseline |
| HRC | Repair Cooperative | +5 Materials at active-faction turn start | 25 Credits + 10 Materials; Council Office |
| HRC | Watch Muster | Unlock Settlement Watch recruitment offer | 20 Credits + 5 Materials; Council Office |
| HRC | Scout Relay | Unlock Hunter-Scouts recruitment offer | 25 Credits + 8 Materials; Council Office |
| HRC | Witness Mesh | +1 Intel at active-faction turn start | 20 Credits + 2 Intel; Council Office |
| HRC | Operations Garage | Apply an authored 10 Credits / 5 Materials discount to the existing starting-hub reinforcement/support action | 35 Credits + 15 Materials; Repair Cooperative |
| QXZ | Concession Office | Starting/prebuilt administration; +7 Credits at active-faction turn start | prebuilt baseline |
| QXZ | Climate Fabricator | +6 Materials at active-faction turn start | 25 Credits + 1 Intel; Concession Office |
| QXZ | Mandate Barracks | Unlock Meridian Security recruitment offer | 20 Credits + 1 Intel; Concession Office |
| QXZ | Stratospheric Lab | Unlock Aerosol Techs recruitment offer | 25 Credits + 2 Intel; Concession Office |
| QXZ | Risk Analytics Cell | +1 Intel at active-faction turn start | 25 Credits + 2 Intel; Concession Office |
| QXZ | Continuity Suite | Apply an authored 10 Credits / 2 Intel discount to the existing starting-hub reinforcement/support action | 35 Credits + 3 Intel; Climate Fabricator |

The scenario economy must make roughly three or four facilities per faction realistically constructible during the proof, not all six. If current scenario length or resource rewards make that impossible, adjust only prototype costs/rewards and document the tuning; do not expand the economy system.

## In scope

- Replace generic/placeholder facility presentation in the proof scenario with exactly the six approved-provisional facilities for each faction.
- Preserve stable IDs and scenario-authored/localization-key-driven display data; no player-facing raw IDs.
- Extend existing facility effect metadata only as narrowly required for:
  - recurring Credits, Materials, or Intel income at the already-authorized turn boundary;
  - facility-gated recruitment offers using existing recruitment services;
  - an authored cost discount on the existing starting-hub reinforcement/support action.
- Keep effect resolution data-driven. Do not hardcode HRC/QXZ branches in UI or command services.
- Show the full six-facility catalog in the normal base panel with readable built, available, affordable, prerequisite-blocked, and already-built states.
- Show facility name, short function, cost, prerequisite, and expected effect before construction.
- After construction, visibly show resource change, constructed state, and the effect unlocked or improved.
- Preserve the merged White Sky presentation and use faction-appropriate shape/material accents for the base panel or facility markers where practical.
- Use only existing/project-authored presentation assets unless a separately justified asset passes the approved provenance contract.
- Add migration/compatibility handling if existing saves or scenario fixtures reference the old placeholder facility IDs; no silent state loss.
- Produce current 1920×1080 evidence for HRC and QXZ base panels plus one constructed/effect-result state.

## Out of scope

- New base capture, siege, garrison, marketplace, trading, logistics, weather, fog, strategic AI, editor UI, or topology systems.
- A full HoMM town tree, upgrades, mutually exclusive branches, or more than six facilities per faction.
- New tactical unit-line behavior; the next EPIC-016 story owns the three-line tactical identity pass.
- New Champion progression or Operations mechanics. The support facilities may only alter the existing reinforcement/support action through authored cost metadata.
- Final facility art, animation, audio, icons, faction canon, or final balance.
- Broad refactoring of the strategic economy, player shell, render pipeline, or asset architecture.

## Acceptance criteria

- [ ] The proof scenario exposes exactly six named HRC and six named QXZ facilities matching `prototype-faction-contracts.md`.
- [ ] No player-facing base panel, build result, or evidence capture shows placeholder localization text or raw facility IDs.
- [ ] Facility definitions and effects are scenario-authored, serializable, validated, and resolved without faction-specific UI/service branches.
- [ ] Credits, Materials, and Intel recurring effects apply once at the active-faction turn boundary, only from owned constructed facilities, with visible feedback and no preview/failed-turn mutation.
- [ ] Watch Muster, Scout Relay, Mandate Barracks, and Stratospheric Lab gate their authored existing-unit recruitment offers with deterministic stock/refresh behavior.
- [ ] Operations Garage and Continuity Suite visibly change the cost/affordability of the existing starting-hub reinforcement/support action through authored effect metadata.
- [ ] One build per base per strategic cycle, affordability, prerequisites, duplicate protection, and no-partial-mutation behavior remain green.
- [ ] The base panel communicates all six choices and built/available/blocked states at 1920×1080 in the normal player shell.
- [ ] Prototype scenario tuning allows approximately three or four facilities per faction to be constructed during the proof but does not make all six routine purchases.
- [ ] Existing strategic movement, site interaction, objective pressure, AI, tactical handoff, recruitment, and battle-result smoke behavior remain green.
- [ ] Asset validation passes; every visible external/generated non-code asset is source-identifiable, ledgered where required, and replaceable. AI-generated assets, if any, obey the literal `ai-generated__` naming/path/provenance contract.
- [ ] EditMode, PlayMode, validator, standalone-build, exact-head PR CI, and post-merge main CI pass.

## Verification and evidence

- EditMode tests for definition/effect validation, resource timing, ownership filtering, support-discount calculation, migration, and no partial mutation.
- PlayMode tests for HRC and QXZ base-panel states, build/result flow, gated recruitment, support discount, normal-shell readability, and preserved connected-loop smoke.
- PNG evidence under `production/evidence/STORY-BASE-CONTENT-001/`:
  - HRC six-facility base panel at 1920×1080;
  - QXZ six-facility base panel at 1920×1080;
  - constructed facility with visible effect/result at 1920×1080.
- PR body lists prototype tuning, old-ID migration/compatibility, assets/provenance, omissions, placeholders, evidence, and exact-head CI.

## Ambiguity gate

PASS. On 2026-07-14 the human explicitly approved `STORY-BASE-CONTENT-001 as proposed`, including the facility mapping, prototype values, prerequisites, three-to-four-affordable target, recruitment gates, and reinforcement/support discounts. These values remain tunable prototype balance rather than final canon. If the support-discount mapping would require a new Champion system rather than a narrow extension of the existing starting-hub reinforcement action, stop and return the blocker.

## Proposed branch

`story/STORY-BASE-CONTENT-001-six-facility-content-and-presentation`

## Verdict

READY / human-approved on 2026-07-14. Codex may implement only this bounded story from the activated checked-in prompt.
