---
title: Prototype Visual Target and Asset Ledger Contract
type: art-spec
status: approved
phase: pre-production
owner: shared
created: 2026-07-12
updated: 2026-07-17
approval: approved
related: [design/research/zero-budget-prototype-assets-and-reference-games-2026-07-12, design/ux/player-shell]
---

# Prototype Visual Target and Asset Ledger Contract

## Target

White-daylight cyberpunk: pale engineered sky, dark industrial infrastructure, snow/ice/rust, highly controlled faction emissions, readable silhouettes, and a restrained player shell. The proof should look intentionally stylized, not like unrelated free packs hidden by bloom.

## Strategic-map visual model

Human-approved on 2026-07-13: use a **hybrid physical map**. The dominant read is a real elevated landscape with terrain, structures, sites, and embodied Champion/unit presence. Routes, reachability, ownership, and objective pressure appear as restrained operational overlays on that world rather than as the world itself.

Human-reaffirmed on 2026-07-17 after rejecting the implemented polygon/node surface: `hybrid physical map` means a physical corridor adventure map over hidden graph rules, not a region-polygon reskin. Prepare one representative map-and-shell slice for human review before converting the whole scenario. See `design/research/physical-adventure-map-direction-2026-07-17.md`.

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

- HRC: human-approved controlled heterogeneity. Repaired layers, civic/rescue orange, warm practical lights, reused structures, visible local modification, coalition markings, mesh beacons, labour/rescue/activist/volunteer patches, and occasional repurposed corporate technology unify groups that retain distinct origins. HRC should look technologically capable, countercultural in places, and politically broad—not primitive, ethnically uniform, uniformly peaceful, or anti-development by default.
- QXZ: human-approved blend of climate-engineering expedition and sleek corporate futurism. Use pearl/white sealed geometry, pale-blue hazard light, sensor precision, atmospheric and marine-maintenance machinery, premium clean surfaces, and discreet security embedded inside infrastructure and procedure. QXZ should read first as a builder of useful, beautiful megaprojects—not as a generic occupying army.

## Neon distribution and security posture

Human-approved on 2026-07-13:

- Concentrate neon and controlled emissions around Champions, inhabited frontier culture, vehicles, public screens, repair shops, sensors, and faction infrastructure. Wilderness remains dark/natural enough for these islands of identity and power to matter.
- Ordinary infrastructure has an uneven security posture. Safe/local places may remain recognizably civilian; corporate extraction and continuity sites are more controlled; contested corridors show improvised escalation.
- Do not depict the region as uniformly fortified or occupied by mass armies.
- Champion-led forces are small, high-capability task groups or special-operations-scale formations. They may be called armies in strategy-game terms, but their visual scale should not imply conventional divisions or permanent front lines.

## Champion and army representation

Human-approved on 2026-07-13: the strategic-map actor is one embodied Champion accompanied by a small, cosmetic, composition-informed entourage.

- The Champion remains the single selectable gameplay actor and owns movement, occupancy, interaction, and route state.
- Two or three compact follower, drone, or vehicle silhouettes may communicate dominant army roles or faction character.
- The entourage is presentation-only: it has no independent pathfinding, occupancy, targeting, action authority, or one-to-one promise with stack counts.
- Composition changes may alter the entourage's broad silhouette mix, but exact unit/count representation is not required for the proof.
- At distant zoom or in crowded views, the entourage may collapse into the Champion silhouette/marker to preserve readability.
- HRC expression should resemble an improvised rescue/security column using adapted vehicles, local equipment, and drones. QXZ expression should resemble a disciplined protected mandate team with controlled formation and sensor escorts.
- The vertical-look spike may use bounded placeholder entourage silhouettes, but must prove that the model reads more like a traveling force than a lone token.

## Zero-budget pipeline

CC0 modular geometry + controlled PBR material library + shared White Sky shaders + custom decals/icons/VFX/UI. Use generated imagery only as provenance-tracked temporary direction or replace-later material.

## Asset acceptance gate

Every imported asset must pass license, provenance, silhouette, camera readability, scale, material-remap, animation, performance, and replacement-status checks.

## Canonical ledger

Unity repository path: `Assets/Provenance/asset-ledger.csv`.
Required columns: `asset_id, source_url, author, license, license_url, downloaded_date, original_filename, local_path, modifications, attribution_text, intended_use, origin_type, generator, generation_record, replacement_target, status, reviewer`.
Allowed status: `prototype`, `replace-later`, `candidate-final`, `rejected`.

Allowed `origin_type` values: `human-authored`, `external`, `procedural`, `ai-generated`.

## AI-generated non-code asset rule

Human-approved on 2026-07-14. This rule applies to every non-code game asset type now or later, including images, textures, materials, models, animation, audio, music, voice, video, VFX source media, UI art, icons, portraits, and generated narrative/content files used as runtime assets. Code is explicitly exempt.

- Every AI-generated non-code asset filename must begin with the literal marker `ai-generated__`, for example `ai-generated__hrc-champion-portrait-01.png` or `ai-generated__white-sky-wind-loop-01.wav`.
- Store such files under an obvious isolated path such as `Assets/Generated/AI/<asset-type>/` as well as marking the filename. A directory alone is not sufficient.
- Every such asset must have an `asset-ledger.csv` row with `origin_type=ai-generated`, the generator/tool and model when known, a durable prompt/recipe or generation-record path, source-input provenance, intended use, and a non-empty `replacement_target`.
- AI-generated assets default to `status=replace-later`. Promoting one to `candidate-final` requires explicit human review; promotion never removes the AI label or provenance history.
- Runtime/content references must use a stable logical asset ID or replaceable registry/configuration boundary rather than depending on the generated filename as permanent identity.
- Replacing an AI-generated asset must add the replacement as a separately named file, repoint the stable reference, and then remove or archive the generated file and its Unity `.meta` safely. Do not overwrite a human/contractor replacement under an `ai-generated__` filename.
- Validators must fail when an AI-generated file lacks the filename marker, isolated path, complete ledger metadata, `replace-later` status by default, or a replacement target; they must also fail when a file marked `ai-generated__` is absent from the ledger.
- Agents must stop rather than obscure, guess, or strip AI provenance.

The same replaceability principle applies across future non-code asset categories: generated assets must remain isolated from authored replacements and swappable without redesigning gameplay or presentation architecture.

## Vertical-look spike

Before broad asset import, produce one representative scene containing: strategic site/base silhouette, one HRC unit group, one QXZ unit group, snow/industrial terrain, selection state, one action VFX/SFX event, and player-shell framing. Approve or revise that image before scaling content.

## Capture quality gate

No raw IDs; stable hierarchy at 1080p; factions distinguishable without labels; interactable sites readable by silhouette; selected/reachable/hostile states remain distinguishable without color alone; license ledger complete for every visible external asset.
