---
title: STORY-ART-LOOK-001 Vertical Look and Asset Provenance Integration Spike
type: story
status: done
phase: production
owner: shared
created: 2026-07-13
updated: 2026-07-14
approval: approved
related: [production/epics/epic-016-accelerated-playable-product-foundation, design/art/prototype-visual-target-and-asset-ledger, design/research/zero-budget-prototype-assets-and-reference-games-2026-07-12, design/ux/player-shell]
---

# STORY-ART-LOOK-001 Vertical Look and Asset Provenance Integration Spike

## Value

As a player or reviewer, I want one coherent White Sky strategic presentation frame with visibly distinct HRC and QXZ forms so I can judge whether the zero-budget art pipeline can produce a recognizable Neon Champions identity before broad asset import.

## In scope

- Create `Assets/Provenance/asset-ledger.csv` with the approved columns, allowed values, one schema/example row, and automated validation for required fields and values.
- Enforce the approved cross-asset AI rule for every AI-generated non-code asset used by the spike: literal `ai-generated__` filename prefix, isolated `Assets/Generated/AI/<asset-type>/` path, complete generation/provenance metadata, default `replace-later` status, and a stable logical replacement boundary. Code is exempt.
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
- Express QXZ first as a sleek climate-engineering/megaproject expedition with discreet embedded security, not a generic corporate army. Concentrate neon around Champions, inhabited frontier culture, vehicles, sensors, public systems, and infrastructure rather than applying it uniformly to wilderness.
- Express HRC through controlled heterogeneity: a shared civic/rescue-orange and warm-mesh recognition layer across visibly different local, labour, rescue, ecological/counterculture, volunteer, and defector equipment. Do not reduce HRC to primitive locals, peaceful environmentalists, or a standardized militia.
- Keep Champion-led forces at small task-group/special-operations visual scale; do not imply conventional mass armies or permanent front lines.
- Prefer existing/procedural geometry for the spike. Import at most a narrowly justified CC0/acceptable-license sample needed to prove the ledger/import path.
- Do not overwrite a later human/contractor replacement under an AI-generated filename. Add the replacement separately, repoint the stable reference, and safely remove/archive the generated asset and `.meta`.
- Produce current 1920×1080 PNG evidence and a concise before/after and provenance review.

## Out of scope

Broad asset-pack import; final art; full scenario reskin; final HRC/QXZ units or buildings; production animation set; full audio pass; final logo/portraits; render-pipeline migration; shader-framework rewrite; Addressables migration; new gameplay mechanics; tactical-shell redesign; base-building content implementation; public marketing release.

## Acceptance criteria

- The ledger exists at `Assets/Provenance/asset-ledger.csv`, validates required columns/allowed values, and every visible external or AI-generated asset in the evidence has a complete ledger row.
- Validation fails for an AI-generated non-code asset missing the `ai-generated__` filename prefix, isolated AI path, `origin_type=ai-generated`, generation record, replacement target, or default `replace-later` status, and for a marked AI-generated file missing from the ledger.
- A test/evidence example proves that presentation references use a stable logical asset boundary and can be repointed to a separately named replacement without gameplay or presentation-architecture redesign.
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

PASS. The hybrid physical-map model, White Sky/regional scene rules, Champion-plus-cosmetic-entourage representation, HRC/QXZ physical languages, neon distribution, and small-task-group scale were human-approved on 2026-07-13. On 2026-07-14 the human approved the ledger path/columns and bounded external-asset rule, adding the binding requirement that every AI-generated non-code asset type be visibly labeled in its filename and provenance, isolated, and cleanly replaceable; code is exempt. The research note is reference-only, not authority for exact assets. If implementation would require render-pipeline migration, broad shader architecture, uncertain asset licensing, hidden AI provenance, or invented faction visual canon, stop.

## Proposed branch

`story/STORY-ART-LOOK-001-vertical-look-provenance-spike`

## Completion evidence

- Unity PR: https://github.com/myriwe-bot/neon-champions-unity/pull/149
- Final PR head: `b8bea3a1a034c43ef990cfb9678337c419fa8442`
- Exact-head PR CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/29331732275
- Squash merge commit: `686db4b618ed55111d0ee97ca43a7a6bfc358794`
- Post-merge `main` CI: https://github.com/myriwe-bot/neon-champions-unity/actions/runs/29332199330
- Evidence: `production/evidence/STORY-ART-LOOK-001/` in the Unity repository, including current 1920×1080 normal and selected/action captures.
- Delivered provenance boundary: validated asset ledger plus a deterministic, project-authored, replace-later procedural terrain plate behind a stable registry/resource boundary. No AI-generated or external non-code asset was integrated.

## Verdict

DONE / merged on 2026-07-14. The bounded White Sky look/provenance spike passed final visual review, exact-head CI, and post-merge `main` CI. Replace-later prototype art remains explicitly non-final.
