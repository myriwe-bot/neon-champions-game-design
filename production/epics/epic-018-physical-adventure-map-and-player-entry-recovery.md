---
title: EPIC-018 Physical Adventure Map and Player Entry Recovery
type: epic
status: active
phase: production
owner: shared
created: 2026-07-17
updated: 2026-07-20
approval: approved
related: [design/gdd/product-constitution, design/gdd/strategic-map, design/ux/player-shell, design/art/prototype-visual-target-and-asset-ledger, design/research/physical-adventure-map-direction-2026-07-17, production/stories/story-prototype-continuity-qa-001-build-resume-pressure-playtest-closeout, production/stories/story-map-physical-rollout-001-complete-duel-map-and-two-faction-interaction-parity, production/stories/story-prototype-continuity-qa-002-recovery-replaytest, production/stories/story-standalone-display-001-safe-default-window-and-manual-launch-parity]
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
4. `STORY-MAP-PHYSICAL-ROLLOUT-001` — DONE / merged as Unity PR #176 / post-merge verified by `main` run `29699588200`; the complete ten-node/twelve-route duel scenario now uses the shared physical presentation with HRC/QXZ interaction parity.
5. `STORY-PROTOTYPE-CONTINUITY-QA-002` human replaytest — DONE / `BLOCKED — REJECT CLOSEOUT`; ordinary double-click launch showed the Unity splash then a black window, while CI-style forced 1920x1080 launch succeeded on the same machine.
6. `STORY-STANDALONE-DISPLAY-001` — MERGED / automated PASS / human recheck pending; Unity PR #180 merged as `56122d14…`, exact-head run `29761977696` and post-merge run `29762704689` passed.

No EPIC-018 implementation packet is runnable. The owner must first double-click the exact repaired `main` build without arguments. The full recovery replaytest must be repeated after repair and cannot be passed by automation.

## Boundaries

- No gameplay-rule, economy, AI-policy, tactical-combat, save-schema, scenario-topology, balance, or content expansion inside the standalone-entry repair.
- No full-map art production before the representative visual slice receives human approval.
- No tile/hex/free-movement rewrite without a later explicit human decision based on successful playtest evidence.
- Existing deterministic behavior remains a temporary implementation baseline, not final design authority.
- AI/procedural non-code assets remain provenance-labeled, isolated, replaceable, and validator-covered.

## Closeout relation

EPIC-017 implementation remains technically merged, but its human continuity closeout was rejected because the standalone build failed and the strategic map was unusable. EPIC-017 may not be called complete from automation. This recovery epic owns the next player-facing repair sequence.

## Verdict

ACTIVE / approved. Orders 1–4 are DONE. Order 5 returned `BLOCKED — REJECT CLOSEOUT`. Order 6 is merged and automation-green but awaits mandatory human double-click verification.
