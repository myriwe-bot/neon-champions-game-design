---
title: Zero-Budget Prototype Assets and Reference Games — 2026-07-12
type: research
status: in-review
phase: pre-production
owner: shared
created: 2026-07-12
updated: 2026-07-12
related:
  - production/planning/full-project-review-and-completion-plan-2026-07-12
  - production/planning/accelerated-prototype-and-early-access-plan-2026-07-10
approval: pending
---

# Zero-Budget Prototype Assets and Reference Games — 2026-07-12

## Recommendation

Use a **deliberately stylized hybrid placeholder pipeline** for the one-month prototype:

1. CC0 low-poly/modular 3D geometry for terrain, infrastructure, and simple unit bases;
2. CC0 PBR materials/HDRIs for snow, ice, rock, metal, concrete, rust, and industrial surfaces;
3. custom faction materials, decals, silhouettes, lights, VFX, UI, and color/shape language;
4. generated concept images only as internal direction or clearly provenance-tracked temporary portraits/backgrounds;
5. CC0 or carefully attributed UI icons and sound effects;
6. no attempt to disguise unrelated packs as final art.

The goal is not “free assets that look final.” The goal is a coherent, screenshot-worthy prototype whose visual system can later be replaced by original/contracted art without redesigning the game.

## Can shaders make free assets distinctive?

**Yes, but not by themselves.** Shaders can unify unrelated assets and create the White Sky identity through:

- controlled palette and value compression;
- snow/ice accumulation masks;
- faction emissive colors;
- wind, frost, scanline, feed corruption, and holographic overlays;
- distance fog and engineered-sky lighting;
- rim lighting and unit selection outlines;
- terrain blending and decal layers;
- damage, maintenance, contamination, and ownership states;
- strategic-map iconography and stylized depth.

Shaders cannot fix:

- generic or incompatible silhouettes;
- mismatched scale and topology;
- poor animation;
- missing faction architecture language;
- unclear tactical roles;
- inconsistent camera/perspective;
- incoherent UI.

Therefore use a **kitbash acceptance rule**: an asset is acceptable only if its silhouette, scale, camera readability, license, and material remapping fit the visual target. Reject packs that require hiding their basic shape.

## Zero-cost source shortlist

### Kenney

- Source: https://kenney.nl/assets
- License/source statement: https://kenney.nl/support
- Verified current statement: Kenney asset-page game assets are CC0, usable commercially, with attribution not required.
- Relevant example: https://kenney.nl/assets/modular-space-kit — 40 modular sci-fi/station files, CC0.
- Best use: blockout infrastructure, modular stations, generic UI/input assets, prototypes.
- Risk: clean, toy-like low-poly language may need aggressive materials, decals, lighting, and silhouette additions to reach Neon Champions tone.

### Poly Haven

- Source: https://polyhaven.com/
- License: https://polyhaven.com/license
- Verified current statement: textures, HDRIs, and 3D models are CC0 and may be used commercially without attribution.
- Best use: snow/ice/rock/industrial materials, skies/HDRIs, environmental props.
- Risk: realistic scans can clash with stylized low-poly geometry unless texture density and shading are tightly controlled.

### ambientCG

- Source: https://ambientcg.com/
- Verified current statement on site: assets are CC0, free without attribution, including commercial use.
- Best use: PBR snow, ice, ground, concrete, metal, fabric, rust, and surface variation.
- Risk: same realism/stylization mismatch as Poly Haven; build a controlled material library rather than importing freely.

### OpenGameArt

- Search used: https://opengameart.org/art-search-advanced?keys=sci-fi+isometric
- Live results included isometric sci-fi buildings, industrial plants, interface SFX, laser SFX, maintenance rooms, characters, and strategy-building packs.
- Best use: concept/blockout candidates, UI/SFX candidates, temporary 2D strategic icons.
- Risk: licenses vary per asset. Do not treat the whole site as CC0. Every imported item needs a recorded asset-page URL, author, exact license, attribution requirement, and modification notes.

### itch.io free strategy assets

- Source: https://itch.io/game-assets/free/tag-strategy
- Live results included Strategy Game Resource Icons, free 3D land units, and a free sci-fi UI pack.
- Best use: discovering prototype-specific packs.
- Risk: licenses and AI provenance vary by publisher. “Free” does not mean CC0 or commercially unrestricted. Record and review each license separately.

### Game-icons.net

- Source/license: https://game-icons.net/about.html
- Verified current statement: icons are offered under CC BY 3.0 and require credit to the original author.
- Best use: temporary action/resource/status icons, heavily restyled through a consistent frame/stroke system.
- Risk: attribution ledger is mandatory; generic fantasy symbols may undermine the no-direct-magic identity.

### Freesound

- Source: https://freesound.org/
- License FAQ: https://freesound.org/help/faq/#licenses-0
- Verified caution: licenses vary; some sounds cannot be used commercially and many require attribution. Filtering to CC0 or acceptable CC BY assets is required.
- Best use: temporary environmental, UI, mechanical, impact, radio, wind, and industrial sounds.
- Risk: inconsistent recording quality, licensing, loudness, and potential platform claims. Keep source files and license snapshots.

## Suggested zero-budget art direction

### Strategic map

- 2.5D/isometric or elevated orthographic map.
- Simplified land masses and routes with strong value hierarchy.
- White Sky palette: cold pale environment, dark infrastructure, controlled faction emissions.
- Sites are recognizable silhouettes, not text labels on circles.
- HRC: repaired/local/adaptive structures, warm practical lights, layered additions, visible reuse.
- QXZ: clean climate-finance infrastructure, controlled geometry, sensor precision, branded environmental systems.

### Tactical battle

- Low-poly units with strong role silhouettes and colored equipment/lighting, not merely recolored identical soldiers.
- Snow/ice industrial boards using a small number of reusable modular pieces.
- Clear base rings, facing/selection, cover, range, and objective states.
- VFX carries identity: HRC improvisation/relay/repair; QXZ prediction/control/environmental authority.

### UI

- Do not skin the current debug panels.
- Build an intentionally designed information hierarchy inspired by modern tactics games.
- Use one typography family, one icon grammar, restrained faction accents, and plain-language labels.

## Asset workflow for the first month

1. Create `assets/provenance/asset-ledger.csv` before importing external assets.
2. Record source URL, author, license, downloaded date, original filename, modifications, attribution, and intended replacement status.
3. Choose one geometry family for infrastructure and one for units; do not mix packs opportunistically.
4. Create a master material/shader library before producing many scenes.
5. Produce one vertical-look scene and screenshot gate.
6. Only after that gate, expand assets to the scenario.
7. Mark every imported asset `prototype`, `replace-later`, or `candidate-final`.

## Budget options after the one-month prototype

These are planning bands, not current vendor quotes.

### Band 0 — effectively zero

- CC0/free assets, in-house kitbashing, shaders, generated internal concepts, volunteer testing.
- Appropriate for: first playable and investor proof.
- Main risk: large time cost and visible genericness.

### Band 1 — micro-budget

- Roughly €1,000–€5,000 total.
- Buy a few coherent commercial packs, commission a key logo/Champion image, acquire fonts/music/SFX, and pay for a small amount of UI/VFX cleanup.
- Appropriate for: a strong fundraising trailer and public prototype.
- Main risk: insufficient for fully original faction/unit production.

### Band 2 — focused indie vertical slice

- Roughly €10,000–€30,000.
- Contract key character art, UI treatment, several unit/structure families, animation/VFX/audio polish, and trailer support while retaining kitbashed environment assets.
- Appropriate for: public demo/vertical slice and serious investor outreach.
- Main risk: requires tight art direction and milestone contracts.

### Band 3 — original Early Access production

- Roughly €50,000–€150,000+ depending on geography, asset count, animation, audio, and contractor seniority.
- Supports a meaningful original-art conversion, but not an unconstrained AA content scope.
- Appropriate only after prototype metrics, fundraising, and a locked production plan.

Recommendation: remain in Band 0 for the month-one prototype, then fund only a small Band 1 “identity package” if the game and fundraising material justify it. Do not buy many unrelated packs.

## Reference games to study

### Existing owner references

#### Heroes of Might and Magic III

Study for:

- strategic-map readability;
- one-more-turn route planning;
- resource and mine language;
- town-building cadence and anticipation;
- army composition and upgrade readability;
- adventure-map density.

Do not copy its opaque legacy UX or fantasy assumptions.

#### Heroes of Might and Magic: Olden Era

Study for:

- modernized HoMM interaction and visual hierarchy;
- contemporary town/faction presentation;
- how classic strategic density is communicated to modern players.

Treat preview/early-access observations as provisional where applicable.

#### XCOM: Enemy Unknown / Enemy Within

Study for:

- tactical camera and selection clarity;
- readable action economy;
- hit/forecast presentation;
- base-level strategic decisions;
- research/resource pacing;
- soldier identity and consequence.

Avoid importing XCOM's cover-and-percent-hit structure automatically.

#### Shadowrun Returns series

Study for:

- cyberpunk tactical readability;
- dialogue and world exposition without encyclopedic overload;
- portraits, environments, and UI working together under constrained production budgets;
- mission scripting and compact authored campaigns.

#### Sid Meier's Civilization V

Study primarily for UI feel rather than mechanical scope:

- calm, authoritative screen composition;
- readable top-bar resources and turn state;
- restrained panels, texture, iconography, and typography;
- contextual information revealed when needed instead of permanent debug density;
- satisfying button states, selections, notifications, and end-turn cadence;
- a visually dominant map with strategic information kept accessible;
- an interface that feels embedded in a complete political-strategic world.

Do not copy Civilization's city/empire scale, diplomacy breadth, or hex-map assumptions automatically. The target lesson is **confidence, hierarchy, tactility, and map-first presentation**.

### Additional recommended references

#### Songs of Conquest

- Source: https://store.steampowered.com/app/867210/Songs_of_Conquest/
- Why: the closest modern commercial reference for strategic exploration plus tactical combat, town/faction identity, readable pixel-art presentation, campaign/skirmish, and editor/community content.
- Study specifically: settlement growth readability, map density, wielder/army relationship, battle pacing, modern HoMM-like UI.

#### Invisible, Inc.

- Source: https://store.steampowered.com/app/243970/Invisible_Inc./
- Why: cyberpunk turn-based information design, readable uncertainty, threat forecasting, clean stylized presentation, and procedural replayability.
- Study specifically: how hidden information remains fair and how UI communicates risk without text walls.

#### Jagged Alliance 3

- Source: https://store.steampowered.com/app/1084160/Jagged_Alliance_3/
- Why: strategic territory layer connected to characterful tactical squads, campaign persistence, logistics, and readable modern turn-based combat.
- Study specifically: character identity, strategic-tactical consequences, map-sector pressure, and how tactical complexity is surfaced.

#### BATTLETECH

- Source: https://store.steampowered.com/app/637090/BATTLETECH/
- Why: tactical unit identity, heat/resource pressure, campaign maintenance, damage persistence, and strategic management.
- Study specifically: making maintenance and damage consequential rather than routine chores.

#### Into the Breach

- Official/retail source to locate during focused mechanics research.
- Why: perfect-information tactical forecasts, compact boards, enemy-intent readability, and objective tradeoffs.
- Study specifically: how tiny action spaces produce deep decisions and how consequences are previewed.

#### Against the Storm

- Official/retail source to locate during focused economy/town research.
- Why: constrained building choices, variable blueprints, settlement identity, pressure clocks, and repeated short-form strategic runs.
- Study specifically: meaningful building choice without requiring a gigantic fixed town tree.

#### Age of Wonders 4

- Official/retail source to locate during faction/customization research.
- Why: strategic/tactical integration, readable affinity systems, faction variation, and modern information hierarchy.
- Study specifically: how faction mechanics remain legible across strategic and tactical layers.

## Reference synthesis for Neon Champions

- **Strategic map and base loop:** HoMM3 + Songs of Conquest.
- **Overall UI feel and strategic authority:** Civilization V, adapted to a smaller Champion-led map.
- **Modern tactical clarity:** XCOM + Into the Breach.
- **Cyberpunk presentation on constrained budget:** Shadowrun Returns + Invisible, Inc.
- **Character consequence and strategic/tactical continuity:** Jagged Alliance 3.
- **Maintenance as meaningful pressure:** BATTLETECH.
- **Variable building decisions and replayability:** Against the Storm.
- **Faction-system breadth:** Age of Wonders 4, used cautiously to avoid scope explosion.

No single reference should define the game. Neon Champions should combine HoMM's map desire, XCOM's interaction clarity, Shadowrun's cyberpunk authorship, and its own infrastructure/information/Champion thesis.
