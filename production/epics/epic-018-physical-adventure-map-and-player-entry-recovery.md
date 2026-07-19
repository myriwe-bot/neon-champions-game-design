---
title: EPIC-018 Physical Adventure Map and Player Entry Recovery
type: epic
status: active
phase: production
owner: shared
created: 2026-07-17
updated: 2026-07-19
approval: approved
related: [design/gdd/product-constitution, design/gdd/strategic-map, design/ux/player-shell, design/art/prototype-visual-target-and-asset-ledger, design/research/physical-adventure-map-direction-2026-07-17, production/stories/story-prototype-continuity-qa-001-build-resume-pressure-playtest-closeout, production/stories/story-map-physical-rollout-001-complete-duel-map-and-two-faction-interaction-parity]
---

# EPIC-018 Physical Adventure Map and Player Entry Recovery

## Outcome

Recover the prototype as a launchable, readable game surface: the Windows build reaches the normal title and scenario path without Editor intervention, and the strategic layer begins replacing its visible polygon/node graph with a physical Arctic adventure map over the existing authored corridor graph.

## Human authority

Approved on 2026-07-17 after the human-owned continuity playtest returned `BLOCKED / REJECT CLOSEOUT`.

Exact approved direction:

- retain the node-route graph as the temporary rules substrate;
- remove the visible polygon/node metaphor from normal play;
- embody routes as physical roads, tracks, passes, bridges, coast/sea/air links, and infrastructure corridors;
- make bases, sites, Champions, armies, and interactions discoverable;
- defer full square-tile, hex, free-movement, province, and terrain-pathfinding systems;
- fix standalone entry first;
- then prepare one representative human-reviewable map-and-shell vertical slice before scaling the whole map.

## Gate

A clean Windows executable launches through the normal title/faction-choice path without manual scene or bootstrap intervention. The next visual slice must then prove, by human review, that one representative portion of the strategic map reads as a physical place rather than a graph and that Champion/base interaction is discoverable.

## Capability sequence

1. `STORY-STANDALONE-ENTRY-001` — DONE / merged as Unity PR #170 and post-merge verified; the executable now proves title -> scenario -> HRC strategic map through the normal production path.
2. `STORY-MAP-VISUAL-SLICE-001` — DONE / merged through Unity PR #172 and post-merge verified; the representative HRC physical-map-and-shell slice received owner visual APPROVE over unchanged graph rules.
3. `STORY-CHAMPION-ARMY-INTERACTION-001` — DONE / merged through Unity PR #174 and post-merge verified; exposes the truthful current Champion army and clean Champion -> base -> Champion context continuity.
4. `STORY-MAP-PHYSICAL-ROLLOUT-001` — READY / approved; scale the owner-approved physical-map treatment across the complete current ten-node/twelve-route duel scenario with HRC/QXZ interaction parity.
5. Human replaytest — DRAFT only; return to continuity/save/opponent-pressure validation after the complete current scenario uses one coherent physical map.

The fourth child is the sole next approved implementation packet after its Unity README pointer activation merges and passes post-merge CI.

## Boundaries

- No gameplay-rule, economy, AI-policy, tactical-combat, save-schema, scenario-topology, balance, or content expansion inside the standalone-entry repair.
- No full-map art production before the representative visual slice receives human approval.
- No tile/hex/free-movement rewrite without a later explicit human decision based on successful playtest evidence.
- Existing deterministic behavior remains a temporary implementation baseline, not final design authority.
- AI/procedural non-code assets remain provenance-labeled, isolated, replaceable, and validator-covered.

## Closeout relation

EPIC-017 implementation remains technically merged, but its human continuity closeout was rejected because the standalone build failed and the strategic map was unusable. EPIC-017 may not be called complete from automation. This recovery epic owns the next player-facing repair sequence.

## Verdict

ACTIVE / approved. Orders 1–3 are DONE. `STORY-MAP-PHYSICAL-ROLLOUT-001` is READY / approved as the sole next implementation packet; Unity pointer activation remains the execution precondition.
