---
title: STORY-ART-LOOK-001 Vertical Look and Asset Provenance Integration Spike
type: story
status: ready-candidate
phase: production
owner: shared
created: 2026-07-13
updated: 2026-07-13
approval: pending
related: [production/epics/epic-016-accelerated-playable-product-foundation, design/art/prototype-visual-target-and-asset-ledger, design/research/zero-budget-prototype-assets-and-reference-games-2026-07-12, design/ux/player-shell]
---

# STORY-ART-LOOK-001 Vertical Look and Asset Provenance Integration Spike

## Value

As a player or reviewer, I want one coherent White Sky strategic presentation frame with visibly distinct HRC and QXZ forms so I can judge whether the zero-budget art pipeline can produce a recognizable Neon Champions identity before broad asset import.

## In scope

- Create `Assets/Provenance/asset-ledger.csv` with the approved columns, allowed statuses, one schema/example row, and automated validation for required fields and allowed status values.
- Build one representative vertical-look scene or bounded presentation mode using the merged player shell, existing strategic presentation boundary, and approved hybrid physical-map model: real terrain/structures with restrained route and objective overlays.
- Show all of these in the same reviewable frame or tightly paired captures:
  - one strategic site/base silhouette;
  - one HRC unit group;
  - one QXZ unit group;
  - snow/ice plus industrial terrain language;
  - selected, reachable, and hostile states distinguishable without color alone;
  - one small action VFX event and one temporary/provenanced SFX event or an explicitly documented audio-N/A result if no legally suitable zero-cost source can be integrated safely;
  - normal player-shell framing without raw IDs.
- Establish a small reusable White Sky material/palette contract and faction-shape accents without broad asset-system or shader-framework replacement.
- Represent each strategic force as one selectable Champion with a small cosmetic, composition-informed entourage. Followers must not gain independent gameplay state, pathfinding, occupancy, targeting, or exact stack-count semantics.
- Express the approved scene rules: luminous engineered White Sky with a localized blue-grey wound, beautiful frontier wilderness interrupted by infrastructure and localized exploitative industrial scars, and restrained cyberpunk emissions rather than an ugly or monotonous snowfield.
- Prefer existing/procedural geometry for the spike. Import at most a narrowly justified CC0/acceptable-license sample needed to prove the ledger/import path.
- Produce current 1920×1080 PNG evidence and a concise before/after and provenance review.

## Out of scope

Broad asset-pack import; final art; full scenario reskin; final HRC/QXZ units or buildings; production animation set; full audio pass; final logo/portraits; render-pipeline migration; shader-framework rewrite; Addressables migration; new gameplay mechanics; tactical-shell redesign; base-building content implementation; public marketing release.

## Acceptance criteria

- The ledger exists at `Assets/Provenance/asset-ledger.csv`, validates required columns/allowed statuses, and every visible external asset in the evidence has a complete ledger row.
- Evidence visibly reads as White Sky cyberpunk rather than default primitives or unrelated free packs.
- HRC and QXZ groups are distinguishable without labels through at least two of silhouette, material treatment, equipment shape, structural language, or controlled emissions.
- Strategic site/base, selected/reachable/hostile states, and the player shell remain readable at 1920×1080 without raw IDs.
- The scene/presentation contains snow/ice and industrial language plus one visible action VFX event.
- Any included SFX has recorded source/license/attribution; otherwise the evidence explicitly records audio as N/A for legal/provenance reasons rather than inventing or importing an unverified file.
- Existing strategic rules, input, AI, tactical handoff, and merged player-shell journey remain green.
- EditMode/validator coverage checks the ledger contract; PlayMode/smoke coverage checks the representative presentation and state readability; exact-head and post-merge Unity CI pass.
- PR body lists all external assets, provenance, omissions, placeholders, replace-later status, and screenshot paths.

## Evidence

- `production/evidence/STORY-ART-LOOK-001/README.md`
- current 1920×1080 PNG normal frame and selected/action frame;
- optional short GIF/video only if the VFX cannot be judged from paired stills;
- ledger-validator results;
- exact-head CI recorded on the PR, not through a self-invalidating evidence commit loop.

## Ambiguity gate

FAIL. The hybrid physical-map model, White Sky/regional scene rules, and Champion-plus-cosmetic-entourage representation were human-approved on 2026-07-13, but `design/art/prototype-visual-target-and-asset-ledger.md` and the zero-budget asset research otherwise remain `in-review` / `approval: pending`. Human approval must still confirm HRC/QXZ physical languages, ledger path/columns, and the bounded external-asset rule before this story becomes READY. If implementation would require render-pipeline migration, broad shader architecture, uncertain asset licensing, or invented faction visual canon, stop.

## Proposed branch

`story/STORY-ART-LOOK-001-vertical-look-provenance-spike`

## Verdict

READY-CANDIDATE / approval pending. Do not run Codex implementation yet.
