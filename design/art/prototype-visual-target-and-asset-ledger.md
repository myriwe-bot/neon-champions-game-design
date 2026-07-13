---
title: Prototype Visual Target and Asset Ledger Contract
type: art-spec
status: in-review
phase: pre-production
owner: shared
created: 2026-07-12
updated: 2026-07-12
approval: pending
related: [design/research/zero-budget-prototype-assets-and-reference-games-2026-07-12, design/ux/player-shell]
---

# Prototype Visual Target and Asset Ledger Contract

## Target

White-daylight cyberpunk: pale engineered sky, dark industrial infrastructure, snow/ice/rust, highly controlled faction emissions, readable silhouettes, and a restrained player shell. The proof should look intentionally stylized, not like unrelated free packs hidden by bloom.

## Strategic-map visual model

Human-approved on 2026-07-13: use a **hybrid physical map**. The dominant read is a real elevated landscape with terrain, structures, sites, and embodied Champion/unit presence. Routes, reachability, ownership, and objective pressure appear as restrained operational overlays on that world rather than as the world itself.

- Do not preserve the current colored node graph as the final visual metaphor.
- Replace abstract region rectangles and luminous connection lines with physical terrain boundaries, roads/tracks/corridors, and recognizable site silhouettes wherever the authored topology allows.
- Overlays may clarify legal routes and pressure, but should recede when not relevant and must not obscure terrain or structures.
- The map need not simulate free movement: the approved node-route rules remain authoritative beneath the physical presentation.
- Avoid both extremes: neither a fully abstract command dashboard nor an unmarked realistic landscape that hides game state.

## White Sky and regional scene rules

Human-approved on 2026-07-13:

- Above the disputed calibration station, the otherwise engineered White Sky has a localized blue-grey thinning or **wound**. It makes the crisis physically visible without turning the whole scene into a disaster storm.
- Daylight is luminous, uncanny, and subtly stratified, combining engineered atmospheric bands with some soft, quiet, almost shadowless beauty.
- The overall image may feel industrial and controlled, but it must not be ugly. White Sky should be memorable and beautiful as well as artificial.
- The region is a varied frontier rather than an endless snowfield: untouched wilderness and natural beauty coexist with connected settlements, roads, utilities, industrial coast, exposed post-retreat terrain, abandoned or temporary infrastructure, and points of careless extraction.
- Cyberpunk identity comes from the collision of wilderness with neon/emissive faction systems, sensors, extraction infrastructure, improvised settlements, and climate-control machinery—not from covering the landscape in city-scale neon.
- Some zones may show visibly careless resource development, including open-cut or strip-mining scars, spoil, rusting equipment, contaminated runoff, or abruptly abandoned works. These are localized contrasts, not the whole region's visual identity.
- Use terrain and seasonal variety where plausible: exposed rock, dark water, ice, snow, tundra/low vegetation, rust, mine spoil, industrial concrete, habitation, and engineered light.

## Faction language

- HRC: repaired layers, civic/rescue orange, warm practical lights, reused structures, visible local modification.
- QXZ: pearl/white sealed geometry, pale-blue hazard light, sensor precision, branded climate systems, controlled cleanliness.

## Zero-budget pipeline

CC0 modular geometry + controlled PBR material library + shared White Sky shaders + custom decals/icons/VFX/UI. Use generated imagery only as provenance-tracked temporary direction or replace-later material.

## Asset acceptance gate

Every imported asset must pass license, provenance, silhouette, camera readability, scale, material-remap, animation, performance, and replacement-status checks.

## Canonical ledger

Unity repository path: `Assets/Provenance/asset-ledger.csv`.
Required columns: `asset_id, source_url, author, license, license_url, downloaded_date, original_filename, local_path, modifications, attribution_text, intended_use, status, reviewer`.
Allowed status: `prototype`, `replace-later`, `candidate-final`, `rejected`.

## Vertical-look spike

Before broad asset import, produce one representative scene containing: strategic site/base silhouette, one HRC unit group, one QXZ unit group, snow/industrial terrain, selection state, one action VFX/SFX event, and player-shell framing. Approve or revise that image before scaling content.

## Capture quality gate

No raw IDs; stable hierarchy at 1080p; factions distinguishable without labels; interactable sites readable by silhouette; selected/reachable/hostile states remain distinguishable without color alone; license ledger complete for every visible external asset.
