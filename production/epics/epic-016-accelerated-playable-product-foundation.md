---
title: EPIC-016 Accelerated Playable Product Foundation
type: epic
status: active
phase: production
owner: shared
created: 2026-07-12
updated: 2026-07-16
approval: approved
related: [production/planning/full-project-review-and-completion-plan-2026-07-12, design/gdd/product-constitution, design/ux/player-shell]
---

# EPIC-016 Accelerated Playable Product Foundation

## Outcome

Transform the tested debug-shaped prototype into a presentable, player-readable proof that demonstrates strategic exploration, base construction, tactical combat, and one Feed consequence without rewriting the proven domain layer.

## Gate

A new player can complete a faction-selectable 20–30 minute HRC/QXZ slice and explain their objective, resources, construction choice, army, tactical actions, and narrative consequence without raw IDs or live guidance.

## Capability sequence

1. `STORY-UI-SHELL-001` — DONE / merged map-first strategic shell and normal player flow; Unity PR #145.
2. `STORY-ART-LOOK-001` — DONE / merged vertical-look and asset-provenance integration spike; Unity PR #149, merge `686db4b618ed55111d0ee97ca43a7a6bfc358794`, post-merge CI passed.
3. `STORY-BASE-CONTENT-001` — DONE / merged HRC/QXZ six-facility prototype content and base presentation; Unity PR #152, merge `d0fcc4d4921c398e52993794ac067d6e439d580d`, post-merge CI passed.
4. `STORY-FACTION-COMPOSITION-001` — DONE / merged through Unity PR #155, merge `892672180b3c6e79d810b767fac371a369197e78`; exact-head and post-merge CI passed.
5. `STORY-PROOF-SCENARIO-001` — DONE / merged through Unity PR #158, merge `74f0d79fcf269cb84e14108626aac1c450d5392e`; exact-head and post-merge CI passed.
6. `STORY-PROOF-QA-001` — READY-candidate / approval pending; deferred human proof-build playtest and optional capture gate. No current READY Unity implementation packet.

Implementation sequence is complete. EPIC-016 remains ACTIVE / awaiting deferred human QA closeout rather than DONE.

## Boundaries

Preserve tested domain/application behavior; decompose presentation only where touched. No broad system expansion, full campaign, public editor, multiplayer, final art, or unrelated architecture rewrite.
