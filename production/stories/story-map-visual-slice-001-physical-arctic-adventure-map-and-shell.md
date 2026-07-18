---
title: STORY-MAP-VISUAL-SLICE-001 Physical Arctic Adventure Map and Shell Vertical Slice
type: story
status: ready
phase: production
owner: shared
created: 2026-07-17
updated: 2026-07-17
approval: approved
related: [production/epics/epic-018-physical-adventure-map-and-player-entry-recovery, design/gdd/strategic-map, design/ux/player-shell, design/art/prototype-visual-target-and-asset-ledger, design/research/physical-adventure-map-direction-2026-07-17, docs/architecture/unity-technical-scheme, docs/architecture/testing-strategy, docs/architecture/control-manifest, production/playtests/playtest-journal]
---

# STORY-MAP-VISUAL-SLICE-001 Physical Arctic Adventure Map and Shell Vertical Slice

## Status

READY / human-approved and Unity-pointer-activated on 2026-07-17 after `STORY-STANDALONE-ENTRY-001` merged and passed post-merge CI. Sole current Unity implementation packet.

The physical-adventure-map direction and ordered repair train were approved on 2026-07-17. The human owner then explicitly requested that the current repair be reviewed/merged and the next implementation packet prepared and continued through completion. This promotes this exact representative-slice packet; it does not authorize full-map rollout.

## Story type

Visual/Feel + UI + Integration vertical slice with a stable replacement boundary.

## Parent epic

- `production/epics/epic-018-physical-adventure-map-and-player-entry-recovery.md`

## Player value

As a player, I need to perceive a frozen physical place, a Champion-led army, recognizable infrastructure, and obvious interaction targets before I read route rules, so I can understand what to inspect and where I can go without decoding a graph.

## Exact complaints preserved as acceptance authority

- "There seems to be no interactivity whatsoever."
- "The readability on the map is horrible."
- "I have no idea what do do."
- "The map is very strange and text is unreadable, it is in general a mess."
- The polygons did not communicate what they represented.
- The base could not be opened or upgraded through the discovered path.
- Champion inventory and units/stacks could not be found.
- `Mobility support` was unexplained.
- The visible node-map basis remained a concern.

Spelling in direct quotations is intentionally preserved.

## Source-authority matrix

| Path | Status / approval | Purpose | Disposition |
|---|---|---|---|
| `production/stories/story-map-visual-slice-001-physical-arctic-adventure-map-and-shell.md` | ready / approved | exact slice scope, IDs, acceptance, evidence, branch | required authority |
| `production/epics/epic-018-physical-adventure-map-and-player-entry-recovery.md` | active / approved | ordered repair train and topology boundaries | required authority |
| `design/gdd/strategic-map.md` §9.1 | approved / approved | physical corridor map over hidden graph | required authority |
| `design/ux/player-shell.md` §§Global principles, Strategic shell, Base screen/panel | approved / approved | map dominance, selection, context, base presentation | required authority |
| `design/art/prototype-visual-target-and-asset-ledger.md` §§Strategic-map visual model, White Sky, faction language, Champion and army representation, asset gate, vertical-look spike, capture quality | approved / approved | visual grammar, provenance, replaceability | required authority |
| `design/research/physical-adventure-map-direction-2026-07-17.md` | approved / approved | approved research rationale and prohibited alternatives | required design context; no independent mechanics authority |
| `docs/architecture/unity-technical-scheme.md` | approved / approved | presentation/application/domain boundaries | required authority |
| `docs/architecture/testing-strategy.md` | approved / approved | TDD, PlayMode, evidence layers | required authority |
| `docs/architecture/control-manifest.md` | approved / approved | agent, provenance, and merge controls | required authority |
| `production/stories/story-standalone-entry-001-windows-player-entry-and-launch-smoke.md` | done / approved | prerequisite launch evidence | historical prerequisite; no visual implementation authority |
| Unity `Assets/NeonChampions/Runtime/Data/Scenarios/mvp-greenland-duel-test.scenario.json` | current implementation data | literal existing IDs and topology | implementation fact only; IDs below are pinned by this story |

## Exact representative HRC corridor

Use the real current HRC scenario state and unchanged graph/domain rules. The required visual slice is keyed to these existing authored IDs:

- HRC base: `node_start_a` / `site_start_a` / `base_start_a`.
- Resource destination: `node_neutral_alpha` / `site_data_cache_alpha`.
- Guarded destination: `node_guarded_alpha` / `site_guarded_alpha`.
- Distant/connected crisis anchor: `node_central_objective` / `site_central_objective`.
- Embodied route A: `route_start_a_neutral_alpha`.
- Embodied route B: `route_start_a_guarded_alpha`.
- Existing onward routes may provide distant context but are not part of the required converted slice.

Do not rename IDs, alter adjacency, change movement cost, add/remove nodes/routes/sites, or modify scenario JSON to make the composition easier. Presentation-only anchor/layout data may map these IDs to improved world positions without mutating authoritative scenario or runtime state.

## Required representative composition

The normal HRC strategic-map view must show:

- the HRC base as a recognizable repaired civic/industrial compound with HRC rescue-orange practical signals;
- the HRC Champion as the single gameplay actor, accompanied by a small presentation-only logistics/rescue entourage;
- two physical ground corridors from the base: one toward the data-cache/resource destination and one toward the guarded industrial destination;
- the central White Sky/calibration infrastructure as a visible distant or connected anchor;
- physical terrain hierarchy: snow/ice, exposed rock or industrial ground, dark water/coast or another believable barrier, and infrastructure shaping the route choices;
- a restrained top bar;
- a persistent selected-Champion/army summary;
- a direct, discoverable HRC-base selection/open state with contextual action presentation.

This is a gate artifact and runnable slice, not permission to convert or reskin every node.

## In scope

### Bounded presentation replacement

- Introduce one bounded replaceable presentation component/adapter for the exact representative slice rather than extending the colored region-polygon metaphor.
- Consume the current `StrategicMapPresentationSnapshot` and existing stable IDs; presentation must not own or mutate gameplay state.
- Keep out-of-slice scenario elements functional. They may retain placeholder presentation outside the required evidence framing, but must not intrude into or visually dominate the representative slice.
- Preserve current zoom/pan/focus behavior where it intersects the slice.

### Physical world grammar

- Replace visible region polygons, node circles, permanent dark/neon graph lines, corridor labels, and tiny terrain-overlaid labels inside the slice.
- Embody the two required edges as plausible roads, ice tracks, bridges, passes, maintenance corridors, or other grounded infrastructure paths.
- Use recognizable physical silhouettes for the base, data-cache/resource site, guarded site, Champion group, and central calibration infrastructure.
- Keep route/reachability/ownership information as restrained contextual overlays that recede when not relevant.
- No critical explanatory text may sit directly over uncontrolled/noisy terrain without backing.

### Champion and army summary

- Pointer selection of the physical HRC Champion must use the normal Input System/raycast path and expose movement plus inspectable army-stack name/count information.
- The initial HRC summary must visibly include the current `Sled Logistics Team x5` stack or whatever exact current snapshot data resolves at implementation time; tests must bind to snapshot data rather than hardcode fabricated state.
- `Mobility support` must either receive plain-language role help grounded in current implementation data or be removed from the visible summary if no truthful explanation exists. Do not invent an active ability, bonus, inventory system, or final unit taxonomy.
- The entourage remains cosmetic: no independent pathfinding, occupancy, input, targeting, or one-to-one stack-count promise.

### Base and site interaction

- The physical HRC base must have a clear normal, hover/focus, and selected state using more than color alone.
- Clicking the physical base through the normal pointer/raycast path must select/open `site_start_a` / `base_start_a` even when the Champion was previously selected; it must not silently reinterpret the click as movement to the current node.
- The resulting context must visibly identify the base and expose the existing base/facility context or a truthful relevant action/denial reason. Do not add new facilities or rules.
- At least the data-cache/resource and guarded destinations must have recognizable click/hover affordance, but their full interaction redesign remains outside this slice.

### Evidence and provenance

- Capture native 1920x1080 normal, Champion-selected, and HRC-base-selected/open states from the production strategic map.
- Any new non-code asset must comply with the approved asset ledger and validator contract.
- AI-generated non-code assets are allowed only with literal `ai-generated__` filenames, isolated `Assets/Generated/AI/<asset-type>/` storage, complete ledger metadata, `replace-later` status, replacement target, and stable logical reference. Stop rather than guessing provenance.
- Deterministic procedural assets must include generator/recipe provenance and reproducibility evidence when newly added.

## Out of scope

- Full scenario or QXZ-side conversion.
- Square-cell, hex, free movement, terrain movement costs, new pathfinding, province simulation, fog, weather, supply, strategic AI redesign, save-schema changes, topology changes, gameplay balance, new facilities/units/sites, tactical changes, final art, or broad onboarding.
- Deleting or rewriting the hidden node-route graph.
- Treating `region` as permission for another colored polygon quilt.
- Permanent luminous graph edges, tiny always-on site labels, or critical white text over pale/noisy terrain.
- Fake inventory, fake buttons, nonfunctional clickable decoration, or controls that bypass the existing input/application path.
- Scaling the approved slice treatment across all ten nodes before explicit human visual approval.

## Allowed placeholders and temporary data

- Existing project-authored procedural texture/primitive assets may be reused when they remain provenance-ledgered and visibly serve the new physical composition.
- New code-built primitive geometry and deterministic procedural textures are allowed as `replace-later` assets through a stable presentation/registry boundary.
- Presentation-only layout anchors keyed to the exact slice IDs are allowed. They must not modify scenario JSON, movement legality, or saved/domain state.
- No new gameplay mocks, synthetic inventory, or fake scenario content.

## Acceptance criteria

- [ ] Starting HRC through the production title/scenario path reaches the representative physical corridor slice.
- [ ] With overlays off, the required 1920x1080 frame reads first as a physical Arctic place with recognizable base, roads/corridors, sites, Champion group, and distant calibration infrastructure—not as a graph or polygon quilt.
- [ ] No permanent node circles, graph edges, region polygons, corridor labels, or critical unbacked terrain text are visible inside the required slice frame.
- [ ] Actual current node/route/site IDs, adjacency, movement costs, movement legality, AI policy, scenario topology, save state, and domain rules remain unchanged.
- [ ] Clicking the physical Champion through normal pointer input selects it and shows current movement plus stack name/count information.
- [ ] Champion-selected state shows the two legal required corridors as restrained reachable/path overlays without turning them into permanent graph lines.
- [ ] Clicking the physical HRC base through normal pointer input—also after Champion selection—selects/opens the base context rather than issuing movement or doing nothing.
- [ ] Base normal/hover-or-focus/selected states remain distinguishable without relying only on hue.
- [ ] `Mobility support` is truthfully explained in plain language or removed; no unsupported mechanic is implied.
- [ ] Critical normal text meets the approved 4.5:1 baseline; meaningful non-text boundaries meet the approved 3:1 baseline, with measured values recorded for the required UI colors/plates.
- [ ] The normal, Champion-selected, and base-selected/open captures are native 1920x1080, free of raw IDs/debug UI/local paths, and visually inspected at native size.
- [ ] Every new non-code asset has compliant provenance, replaceability, and validator coverage; no unlabeled AI-generated asset enters the diff.
- [ ] Existing full EditMode, PlayMode, placeholder/provenance validator, and standalone build checks remain green.
- [ ] The human owner gives explicit APPROVE / REVISE / REJECT on the exact candidate-head visual evidence before this story merges or any full-map rollout story is formed.

## Verification requirements

- TDD: required for production input/presentation behavior. Capture focused RED/GREEN proof for the base-click and Champion-click paths plus any new presentation contract.
- EditMode: exact ID/layout contract, snapshot-to-presentation mapping, no domain/scenario mutation, provenance/registry validation, and contrast calculations where practical.
- PlayMode: production title -> HRC path; actual Input System pointer/raycast selection of Champion and base; selected/reachable state; evidence capture at 1920x1080. Direct method calls alone do not satisfy pointer discoverability.
- Standalone: build must succeed and launch through the repaired production entry. Reuse or extend the built-player smoke only when the environment can truthfully capture the representative slice; do not replace the required PlayMode/visual/human gate with compile-only evidence.
- Visual review: inspect every required PNG at native resolution for physical-place read, silhouette, text fit, contrast, raw-ID/path leakage, and discoverability.
- Evidence path: `production/evidence/STORY-MAP-VISUAL-SLICE-001/` with README, focused test outputs, asset/provenance inventory, contrast measurements, and three required PNGs.
- Performance: record rendered-object/material counts before and after for the required slice and avoid per-frame material/geometry recreation. No broad optimization is required.
- CI: all configured exact-head jobs must pass before merge; final human visual verdict remains non-waivable.

## Ambiguity Check

Status: PASS.

Human-approved answers:

1. Visual model: physical Arctic adventure map over the hidden authored graph.
2. Representative scope: exact HRC starting corridor IDs listed above, not arbitrary nodes and not the full scenario.
3. Interaction target: the HRC base specifically, not an optional generic site.
4. Army scope: truthful selected-Champion stack summary and role explanation only; no invented inventory.
5. Topology: no tile/hex/free-movement rewrite.
6. Asset policy: zero-budget replaceable/provenance-first pipeline remains mandatory.
7. Rollout gate: human approval of exact candidate-head evidence before merge/full-map scaling.

No implementer design, architecture, content, balance, UX, canon, or topology decision remains open. Composition choices inside this bounded contract remain subject to human visual review rather than becoming silent permanent authority.

## Branch / PR requirements

- Branch: `story/STORY-MAP-VISUAL-SLICE-001-physical-arctic-map-shell`
- PR title: `STORY-MAP-VISUAL-SLICE-001 Physical Arctic adventure map and shell slice`
- Non-draft PR required for final gate; it may remain draft while evidence is incomplete.
- PR must link this story and list exact converted IDs/routes, changed presentation files/assets, RED/GREEN proof, normal pointer-path tests, all three captures, provenance/ledger changes, contrast measurements, rendered-object/material counts, omissions, exact head SHA, and CI URLs.
- Codex must commit and push the actual branch, create or update the PR, and print local/remote SHA plus PR URL.
- Codex must not merge. Independent technical review, exact-head CI, human visual approval, and post-merge verification remain external gates.

## Story readiness gate

- [x] Stable story ID/type/owner/parent/status/approval.
- [x] Complete approved source-authority matrix.
- [x] Exact current scenario IDs and topology pinned.
- [x] Concrete bounded in-scope and explicit exclusions.
- [x] Truthful placeholder/provenance policy.
- [x] Observable acceptance criteria including real pointer paths.
- [x] Test, standalone, visual, human, performance, and CI evidence layers.
- [x] Branch/publication/merge contract.
- [x] Ambiguity Check PASS.
- [x] Human approval recorded.

## Activation evidence

- Design authority merge commit: `dc4c4b429bc955f716cd2367e79297e767aa8d4c`.
- Design publish CI: <https://github.com/myriwe-bot/neon-champions-game-design/actions/runs/29610677245> — passed.
- Unity pointer PR: <https://github.com/myriwe-bot/neon-champions-unity/pull/171>.
- Pointer exact head: `f2dbb5bf9ac23890a435ea714c6549cf626fb3c9`.
- Pointer exact-head CI: <https://github.com/myriwe-bot/neon-champions-unity/actions/runs/29610911768> — Compile/Standalone with state-bound built-player launch, EditMode, PlayMode, and Placeholder Validator passed.
- Pointer merge commit: `4057207919bf4add15a418b8a5071d4490946b85`.
- Post-merge Unity `main` CI: <https://github.com/myriwe-bot/neon-champions-unity/actions/runs/29611677131> — all four configured jobs passed.

## Verdict

READY / approved and pointer-activated; the human explicitly approved the bounded visual revision on 2026-07-18 after exact-head candidate `69e33189f448e184df7163dd7bfbfa67466920f5` received `REVISE`. Shell readability, production pointer paths, selected/base states, and technical evidence passed, but the central map still read as flat primitives and graph corridors rather than a convincing physical Arctic place. Continue only from the approved runnable packet `production/sprints/codex-story-map-visual-slice-001-visual-revision.prompt.txt`. Keep Unity PR #172 draft; do not merge, scale to the full map, or activate the follow-up until regenerated exact-head evidence receives a fresh visual verdict.
