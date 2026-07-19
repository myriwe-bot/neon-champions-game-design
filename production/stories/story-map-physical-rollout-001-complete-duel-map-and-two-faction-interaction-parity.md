---
title: STORY-MAP-PHYSICAL-ROLLOUT-001 Complete Duel Map and Two-Faction Interaction Parity
type: story
status: ready
phase: production
owner: shared
created: 2026-07-19
updated: 2026-07-19
approval: approved
related: [production/epics/epic-018-physical-adventure-map-and-player-entry-recovery, production/stories/story-map-visual-slice-001-physical-arctic-adventure-map-and-shell, production/stories/story-champion-army-interaction-001-discoverable-champion-army-and-selection-continuity, design/gdd/product-constitution, design/gdd/strategic-map, design/ux/player-shell, design/art/prototype-visual-target-and-asset-ledger, design/research/physical-adventure-map-direction-2026-07-17, docs/architecture/unity-technical-scheme, docs/architecture/testing-strategy, docs/architecture/ci-build-automation, docs/architecture/control-manifest]
---

# STORY-MAP-PHYSICAL-ROLLOUT-001 Complete Duel Map and Two-Faction Interaction Parity

## Status

READY / approved on 2026-07-19.

The representative HRC physical-map slice received owner visual APPROVE, `STORY-CHAMPION-ARMY-INTERACTION-001` then merged through Unity PR #174, and post-merge Unity `main` CI passed. The human owner explicitly requested the next large and meaningful implementation packet and approved its preparation. This activates the previously gated next step: scale the approved physical-map treatment across the complete current duel scenario and give HRC and QXZ equivalent normal interaction coverage.

This is the sole next Unity implementation packet after its README pointer activation is merged and post-merge verified.

## Story type

Visual/Feel + UI + Integration + bounded presentation refactor.

## Parent epic

- `production/epics/epic-018-physical-adventure-map-and-player-entry-recovery.md`

## Player value

As either HRC or QXZ, I need the whole current duel scenario to read as one coherent physical Arctic frontier—with bases, routes, sites, Champions, and the central crisis physically embodied—so exploration and interaction remain understandable after I leave the original HRC starting slice.

## Why this is the next meaningful slice

The approved representative slice proved the visual grammar but deliberately left six nodes, ten routes, the QXZ start, and most cross-map interaction in reduced out-of-slice placeholders or the old fallback presentation. The approved full-map rollout gate is now satisfied. This packet completes one coherent player-facing capability rather than adding another isolated backend mechanic.

It does not claim final art or change the graph rules. It turns the complete current scenario into a consistently playable physical map.

## Source-authority matrix

| Path | Status / purpose | Disposition |
|---|---|---|
| design-control root `AGENTS.md` | approved repository reading/order and document-control instructions | required repository instruction; not mechanics authority |
| this story | exact rollout scope, IDs, acceptance, evidence, branch | required authority |
| `production/epics/epic-018-physical-adventure-map-and-player-entry-recovery.md` | approved physical-map direction and recovery boundaries | required authority |
| `production/stories/story-map-visual-slice-001-physical-arctic-adventure-map-and-shell.md` | approved visual grammar, replacement boundary, pointer and evidence standards | required authority |
| `production/stories/story-champion-army-interaction-001-discoverable-champion-army-and-selection-continuity.md` | structured Champion army and clean context replacement | required regression authority |
| `design/gdd/product-constitution.md` §§Player promise, Core loop, Product rule | physical exploration, infrastructure, two playable factions | required authority |
| `design/gdd/strategic-map.md` §§2–3, 6, 8, 9.1 | two-faction duel/race map, physical corridors over hidden graph, readable interaction | required authority |
| `design/ux/player-shell.md` §§Global principles, Strategic shell, Base screen/panel, Accessibility | map dominance, selection hierarchy, truthful actions | required authority |
| `design/art/prototype-visual-target-and-asset-ledger.md` §§Strategic-map model, White Sky, Faction language, Champion/army, asset gate | physical/faction grammar and replaceability | required authority |
| `design/research/physical-adventure-map-direction-2026-07-17.md` | approved rationale and prohibited alternatives | required design context; no independent mechanics authority |
| `docs/architecture/unity-technical-scheme.md` | presentation/application/domain boundaries | required authority |
| `docs/architecture/testing-strategy.md` | TDD, PlayMode, visual/evidence layers | required authority |
| `docs/architecture/ci-build-automation.md` | exact-head configured checks | required authority |
| `docs/architecture/control-manifest.md` | implementation, provenance, branch and PR controls | required authority |
| Unity root `AGENTS.md` | implementation authority, architecture, test, asset, Git and stop rules | required repository instruction |
| Unity `Assets/NeonChampions/Runtime/Presentation/AGENTS.md` | presentation-local UX/evidence/authority rules | required scoped repository instruction |
| Unity `Assets/NeonChampions/Runtime/Data/AGENTS.md` | data inspection/validation rules; data edits remain excluded | required scoped repository instruction for preflight |
| Unity `Assets/NeonChampions/Tests/AGENTS.md` | TDD and evidence rules | required scoped repository instruction |
| Unity `production/evidence/AGENTS.md` | evidence package requirements | required scoped repository instruction |
| Unity `README.md` current-task pointer | implementation-repo story/prompt/branch/scope agreement | required control surface; not design authority and cannot attest to its own later merge/CI |
| Unity `mvp-greenland-duel-test.scenario.json` at `07aec85501a12252c5370e9e41a301c0f1afa0bf` | current literal topology, categories, stable IDs and runtime content | implementation fact only; Git blob `e2d547785c7501275de38d85f9ff11376d6f1b6b`, SHA-256 `91a253fd5f7c714db43d654ff81ce0ad47aa0b0c7cf89fb3ea8486417e6795ee`; must not become canon or be edited |

All required design/control sources are approved. The scenario file supplies current implementation facts only. If its blob/hash or node/route/site arrays differ at implementation preflight, stop and reconcile this packet rather than silently changing scope. If implementation touches another scoped Unity directory, its nearest `AGENTS.md` becomes required reading and cannot expand story authority.

### Current Unity implementation-fact inventory

These paths are required inspection surfaces, not independent design authority:

| Unity path | Current role | Disposition |
|---|---|---|
| `Assets/NeonChampions/Runtime/Presentation/PhysicalArcticMapSliceAdapter.cs` | HRC-only contract/model/role mapping and physical palette | primary bounded-refactor starting point |
| `Assets/NeonChampions/Runtime/Presentation/StrategicMapBootstrap.cs` | physical/fallback rendering, Input System/raycast dispatch, camera pan/zoom/focus, shell rebuild and evidence selectors | primary integration starting point; presentation changes allowed within story |
| `Assets/NeonChampions/Runtime/Presentation/StrategicPlayerShellViewModel.cs` | selected-context, structured army cards, action gating and base/site shell projection | required regression surface; change only if parity exposes a presentation defect |
| `Assets/NeonChampions/Runtime/Presentation/StrategicMapRenderedElement.cs` | rendered target kind/source identity used by pointer dispatch | required target-identity surface; preserve application command ownership |
| `Assets/NeonChampions/Runtime/Application/Strategic/StrategicMapInputSession.cs` | production selection/movement/site/base/tactical commands | read-only implementation fact; Application changes are excluded and require stop/amendment |
| `Assets/NeonChampions/Runtime/Application/Strategic/StrategicMapPresentationSmokeScenario.cs` | loads the pinned scenario and supplies the production smoke-session definition consumed by `StrategicMapInputSession` | required production-entry implementation fact; Application changes are excluded and require stop/amendment |
| `Assets/NeonChampions/Runtime/Data/Scenarios/mvp-greenland-duel-test.scenario.json` | exact pinned scenario topology/content | immutable implementation fact for this story |
| `Assets/NeonChampions/Tests/EditMode/Strategic/PhysicalArcticMapSliceTests.cs` | current adapter, context and runtime-refresh regressions | focused EditMode extension starting point |
| `Assets/NeonChampions/Tests/PlayMode/PhysicalArcticMapSlicePlayModeTests.cs` | current native physical-slice/input/context evidence | focused PlayMode/evidence extension starting point |
| `Assets/NeonChampions/Tests/PlayMode/PlayModeSmokeTests.cs` | camera, QXZ, composition, shell, input and broad regression surfaces | extend narrowly; do not weaken unrelated tests |
| `Assets/NeonChampions/Tests/PlayMode/StoryProofScenario001PlayModeTests.cs` | connected HRC/QXZ route and composition proof | required connected-route regression surface |
| `Assets/NeonChampions/Tests/PlayMode/PlayerEntryPlayModeTests.cs` | production title/faction-entry PlayMode coverage | required HRC/QXZ production-entry extension surface |
| `ci/RunWindowsPlayerLaunchSmoke.ps1` | current built-player production launch smoke | narrow HRC+QXZ launch-harness extension allowed; no unrelated workflow redesign |
| `ci/BuildStandaloneWindows64.ps1`, `ci/RunEditModeTests.ps1`, `ci/RunPlayModeTests.ps1`, `ci/RunPlaceholderValidator.ps1`, `ci/ValidatePlayModeEvidencePath.ps1` | configured required verification and evidence-path entry points | execute as required; changes excluded unless a narrowly proven story blocker requires stop/amendment |
| `.github/workflows/unity-foundation-ci.yml` | actual Compile/Standalone, validator, EditMode, PlayMode and evidence orchestration | required CI implementation fact; workflow changes are excluded unless a narrowly proven story blocker requires stop/amendment |
| `production/evidence/STORY-MAP-VISUAL-SLICE-001/` | approved representative physical-map baseline and provenance | historical comparison/regression evidence; never overwrite |
| `production/evidence/STORY-CHAMPION-ARMY-INTERACTION-001/` | approved structured-army/context baseline | historical comparison/regression evidence; never overwrite |

If current code moved or any listed path no longer owns the stated role, stop and reconcile the inventory. Do not silently substitute a broad architecture change.

## Estimate and split control

- Size: **large-capability**.
- Expected implementation shape: one shared scenario-wide presentation adapter/recipe boundary; bounded renderer/camera/input integration; focused EditMode and PlayMode extensions; a narrow two-faction standalone-smoke extension; one five-state evidence package.
- Expected effort: approximately **4–8 focused engineering days**, plus exact-head CI, independent review, evidence regeneration, and human visual review. This is a sizing estimate, not a deadline promise.
- Expected changed surface: primarily Presentation, focused tests, the launch-smoke script if needed, and the new evidence package. Domain, Application, scenario Data, packages, ProjectSettings, scenes, and prior evidence remain unchanged.

Mandatory stop/split rule at focused-GREEN checkpoint:

1. Stop and mark the story BLOCKED rather than broadening it if implementation requires Domain/Application/scenario mutation, topology/content/balance changes, package/settings/scene changes, unapproved assets, or a new camera/input architecture.
2. Stop and form a narrow prerequisite if any contracted route/site cannot be exercised legally through the current production runtime, if the pinned fixture contradicts actual traversal, or if QXZ standalone entry cannot be proved by a narrow extension of the existing launch harness.
3. Stop and split a test/evidence-harness prerequisite if complete two-Champion/ten-site/twelve-route proof requires broad CI/tooling redesign. Do not weaken or sample down the matrix.
4. Stop for human scope amendment if a shared renderer cannot replace HRC-only/fallback behavior without becoming an unrelated full renderer rewrite.
5. A pushed focused-GREEN checkpoint is recovery evidence only. No partial sub-slice may be called DONE or merged under this story unless the human explicitly amends the story and acceptance contract.

## Exact current rollout contract

### Nodes and sites

Convert all ten current nodes into deliberate physical locations through the existing presentation boundary:

| Node | Site/base | Existing role/context |
|---|---|---|
| `node_start_a` | `site_start_a` / `base_start_a` | HRC starting base |
| `node_placeholder_recruitment` | `site_placeholder_recruitment` | recruitment site |
| `node_guarded_alpha` | `site_guarded_alpha` | guarded resource site |
| `node_neutral_alpha` | `site_data_cache_alpha` | HRC-side data cache |
| `node_central_objective` | `site_central_objective` | central infrastructure objective |
| `node_neutral_beta` | `site_neutral_beta` | QXZ-side one-shot visit site |
| `node_guarded_beta` | `site_guarded_beta` | guarded resource site |
| `node_data_cache_beta` | `site_data_cache_beta` | QXZ-side data cache |
| `node_calibration_archive` | `site_calibration_archive` | calibration/archive visit site |
| `node_start_b` | `site_start_b` / `base_start_b` | QXZ starting base |

Use current player-facing snapshot/localization text. The `placeholder` substring in stable internal IDs does not authorize exposing it to players or inventing a final proper noun.

### Routes

Embody all twelve current graph edges as believable physical corridors while preserving literal route IDs, stored endpoint order, existing traversal semantics, movement costs, and legality. Do not infer a new one-way rule from JSON `from`/`to` field order:

- `route_start_a_neutral_alpha`
- `route_start_a_recruitment`
- `route_start_a_guarded_alpha`
- `route_neutral_alpha_central`
- `route_guarded_alpha_central`
- `route_central_neutral_beta`
- `route_neutral_beta_start_b`
- `route_start_b_data_cache_beta`
- `route_data_cache_beta_central`
- `route_guarded_beta_start_b`
- `route_central_guarded_beta`
- `route_central_calibration_archive`

The authored route-array order is binding and must remain exactly:

1. `route_neutral_alpha_central`
2. `route_start_a_neutral_alpha`
3. `route_start_a_recruitment`
4. `route_start_a_guarded_alpha`
5. `route_guarded_alpha_central`
6. `route_central_neutral_beta`
7. `route_neutral_beta_start_b`
8. `route_start_b_data_cache_beta`
9. `route_data_cache_beta_central`
10. `route_guarded_beta_start_b`
11. `route_central_guarded_beta`
12. `route_central_calibration_archive`

The bullet list above groups the physical corridor train for readability; it does not redefine serialized order.

### Actor and target coverage matrix

| Contracted target | Required physical/input proof |
|---|---|
| `champion_1` / `faction_1` at HRC-side nodes | physical HRC actor/entourage, real pointer selection, selected-army context, movement and focus anchor |
| `champion_2` / `faction_2` at QXZ-side nodes | physical QXZ actor/entourage, real pointer selection, selected-army context, movement and focus anchor |
| `site_start_a` / `base_start_a` | HRC landmark, real pointer open, correct HRC facility catalog, Champion-context replacement |
| `site_start_b` / `base_start_b` | QXZ landmark, real pointer open, correct QXZ facility catalog, Champion-context replacement |
| `site_placeholder_recruitment` | recruitment silhouette and legal production-path pointer/preview proof; internal placeholder ID never shown |
| `site_data_cache_alpha`, `site_data_cache_beta` | data-cache silhouettes and legal production-path pointer/preview/consumed-state proof on both halves |
| `site_guarded_alpha`, `site_guarded_beta` | guarded-site silhouettes and legal production-path pointer/encounter preview proof on both halves |
| `site_neutral_beta` | one-shot visit silhouette and legal production-path pointer/preview proof |
| `site_calibration_archive` | archive/calibration silhouette and legal production-path pointer/preview proof |
| `site_central_objective` | central objective silhouette and legal production-path pointer/pressure context proof |
| all twelve routes in authored order | every rendered segment is geometrically associated with its route; aggregate collider/camera-ray coverage spans each visible reachable corridor; at least one real Input System route command is proved for each route in a legal production state; unreachable corridors are not false clickable routes |

Use fresh legal production sessions/routes as needed. A test may derive expected presentation from runtime snapshots, but direct DTO mutation, teleporting, or synthetic player-facing success state does not satisfy input parity.

The default visual read is terrain/infrastructure, not route lines. Reachability and selected-path emphasis remain contextual and restrained.

## In scope

### Scenario-wide physical presentation

- Replace the HRC-only applicability/fallback split with one scenario-wide physical-map presentation contract for the complete current duel map.
- Reuse and refactor the approved HRC physical slice rather than duplicating a second hardcoded renderer.
- Remove normal-play `Out-of-slice` placeholder naming and reduced marker treatment for the ten contracted nodes and twelve routes.
- Preserve a stable presentation adapter/registry boundary keyed to current IDs and snapshot facts; presentation must not own gameplay state.
- Presentation-only anchors, route bends, silhouette recipes, and terrain grouping may be authored outside scenario rules. They must be deterministic, testable, replaceable, and must not alter scenario JSON or saved/domain state.
- Support pan, zoom, focus, and normal target interaction across the complete converted map. The whole scenario need not be readable in one fixed frame; the player must be able to inspect it without exposing a graph fallback.
- Use the same scenario-wide physical anchor/recipe registry for rendering, Champion/site focus, and camera bounds. Current legacy `ToWorld(node.X,node.Y)` focus/clamp behavior must not focus empty graph coordinates after physical anchors diverge.
- Preserve the existing camera contract: pointer drag and explicit pan remain bounded; zoom remains clamped; pan/zoom survive snapshot/UI refresh; Focus centers the selected physical Champion or site and applies the existing focus zoom. Tests must prove HRC start, center, archive, QXZ start, and moved-Champion focus against rendered physical targets.

### Two-faction parity

- `Play HRC` and `Play QXZ` both enter the same coherent physical-map model.
- The active faction must not determine whether the physical map exists. Active/selected/reachable styling may differ truthfully by state.
- HRC retains its approved repaired civic/rescue-orange grammar.
- QXZ receives the approved expedition/corporate grammar: pearl/white sealed geometry, pale-blue controlled signals, sensor precision, and useful climate/infrastructure silhouettes—not villain fortifications or an HRC recolor.
- Both Champions remain the sole selectable strategic actors for their factions, with small cosmetic composition-informed entourages and no independent gameplay authority.
- Selection, current movement, current attached army cards, base/site context, legal/disabled actions, and context replacement work for both factions through the existing snapshot/application boundaries.

### Interaction parity

- Every contracted site has a recognizable physical target and normal/hover-or-focus/selected state distinguishable by more than color.
- Real Input System/raycast input reaches existing site/champion/route commands; no direct presentation mutation or fake button is allowed.
- Reachable physical route segments are pointer-usable wherever the existing route command is legal. Decorative terrain must not occlude current in-scope targets.
- HRC and QXZ base selection opens the existing truthful six-facility context for the selected base; no cross-faction catalog leakage.
- Champion -> base/site -> Champion transitions replace context cleanly and suppress Champion-only actions while another context is visibly selected.
- Existing recruitment, one-shot visit, data-cache, guarded encounter, objective, save/resume, opponent, and tactical-handoff rules remain unchanged but their current map targets stay reachable and readable.

### Visual hierarchy and evidence

- Physical geography includes coherent snow/ice, exposed ground/rock, dark water/coast or barriers, industrial/civic infrastructure, and the White Sky central crisis anchor.
- The center and both faction approaches read as one connected place, not three disconnected dioramas.
- Critical text uses controlled panel backing; raw IDs, localization keys, debug summaries, local paths, and `Out-of-slice` labels are absent in normal play.
- New non-code assets must pass the approved provenance/replaceability contract. No new external or AI-generated asset is required; stop rather than guess provenance.

## Out of scope

- Node/route/site additions, deletions, renames, direction changes, movement-cost changes, scenario JSON changes, topology changes, free movement, tile/hex/province conversion, terrain movement rules, pathfinding, weather, fog, supply, strategic AI redesign, save-schema changes, economy/balance, tactical rules/UI, new units/facilities/sites, campaign content, map editor, final art/audio, or broad onboarding.
- New base construction/recruitment mechanics, inventory, equipment, stack transfer/rearrangement, independent entourage behavior, QXZ/HRC faction redesign, or canon proper names.
- One giant always-visible map frame, permanent luminous route lines, permanent node circles, polygon regions, tiny labels stamped over terrain, decorative clickable objects without commands, or hidden direct-state test setup presented as normal evidence.
- Broad renderer architecture replacement, package/settings/render-pipeline changes, scene ownership changes, or unrelated refactors.

## Allowed placeholders

- Existing ledgered/code-built prototype geometry, procedural textures, and presentation recipes remain `replace-later`.
- New deterministic primitive/procedural presentation is allowed through a stable registry/recipe boundary with reproducibility evidence.
- Existing internal IDs and localization placeholders remain implementation facts but must not leak into normal UI.
- No new gameplay mocks, synthetic route/site state, fake inventory, or unlabeled generated assets.

## Dependencies

- `STORY-STANDALONE-ENTRY-001`: DONE / post-merge verified.
- `STORY-MAP-VISUAL-SLICE-001`: DONE / owner visual APPROVE / post-merge verified.
- `STORY-CHAMPION-ARMY-INTERACTION-001`: DONE / Unity PR #174 / post-merge verified.
- Existing physical-slice renderer/adapter, snapshot model, pointer/raycast command path, shell view model, camera controls, and evidence harness are implementation starting points—not immutable architecture.
- Unity README activation pointer must name this story and pass exact-head plus post-merge CI before implementation begins.

## Acceptance criteria

- [ ] Production title -> Play HRC and title -> Play QXZ both reach the physical duel map without Editor intervention or fallback graph/region presentation.
- [ ] All ten contracted nodes/sites and all twelve contracted routes are represented through the scenario-wide physical presentation contract.
- [ ] No contracted element uses `Out-of-slice` object naming/treatment or exposes raw node/route/site/localization IDs in normal UI.
- [ ] Existing scenario JSON, stable IDs, node/route/site arrays, route endpoint order/traversal semantics/costs, domain rules, save state, AI policy, and tactical behavior are byte-identical to the activation ancestor.
- [ ] Both faction bases and Champions have distinct approved physical grammars beyond recolor, while active/selected/reachable state remains readable beyond hue.
- [ ] The complete actor/target matrix above is proved: both Champions, all ten sites, and every one of the twelve routes has the required rendered-target and legal real-input coverage.
- [ ] Decorative terrain/structures do not occlude current in-scope pointer targets; screen-space or raycast coverage proves every visible route segment that is intended to accept input.
- [ ] HRC and QXZ Champion selection shows actual current movement and structured attached-army cards from snapshot data; no fabricated inventory or stale cross-context cards.
- [ ] HRC and QXZ base selection shows the correct existing faction-owned six-facility catalog and suppresses Champion-only actions until Champion context returns.
- [ ] Recruitment, data-cache/visit, guarded encounter, central objective, save/resume, opponent movement, and tactical handoff regressions remain green through normal application paths.
- [ ] Camera pan/zoom/focus uses the physical anchor registry, reaches and frames both starts, both side clusters, the central objective, the calibration archive, and moved Champions, remains bounded/clamped, and persists through snapshot/UI refresh without exposing old graph presentation.
- [ ] Physical geography remains map-dominant and coherent at native 1920×1080; critical text/card content fits, does not overlap siblings/hints, and uses approved contrast baselines.
- [ ] No per-frame geometry/material/UI recreation is introduced; scenario-wide render-object/material counts and two repeated render/capture counts are recorded and stable.
- [ ] Exact-head Compile/Standalone, EditMode, PlayMode, and Placeholder Validator jobs pass.
- [ ] Required native evidence is inspected and receives explicit human APPROVE / REVISE / REJECT before merge. Approval of this packet does not waive the final visual gate.

## Verification requirements

### TDD and automated coverage

- Focused RED/GREEN required before broad suites.
- EditMode: exact ten-node/twelve-route contract; scenario-wide applicability independent of active faction; deterministic anchor/recipe mapping; distinct faction recipe mapping; no scenario/domain mutation; stable snapshot-derived army/context data; malformed/missing contracted ID rejection.
- PlayMode: production HRC and QXZ entry; real pointer/raycast Champion/base/site/route selection; cross-map pan/zoom/focus; Champion -> site/base -> Champion context replacement; target non-occlusion; route-segment aggregate hit coverage; raw-ID/path/debug leakage; text/card fit and overlap at 1920×1080.
- Regression: full existing EditMode, PlayMode, validator, compile, and built-player launch checks. Standalone proof must execute two independent production launches: title -> Play HRC -> physical HRC map and title -> Play QXZ -> physical QXZ map. A compile-only result or HRC-only launch does not satisfy QXZ parity.

### Native evidence

Store under `production/evidence/STORY-MAP-PHYSICAL-ROLLOUT-001/`:

1. `hrc-start-and-west-approach-1920x1080.png`
2. `central-corridors-and-objective-1920x1080.png`
3. `qxz-start-and-east-approach-1920x1080.png`
4. `qxz-champion-army-selected-1920x1080.png`
5. `qxz-base-selected-1920x1080.png`

Each materially different state must be captured in an isolated Unity process if sequential capture shows contamination/ghosting. The README must record immutable SHA, dimensions/hashes, capture source and selector, exact visible IDs/categories, normal-input route, object/material/UI counts, tests/CI, changed files, provenance, omissions, and native-size visual verdict.

### Performance and asset proof

- Record representative HRC/center/QXZ renderer, material, collider, and UI-object counts.
- Prove no per-frame recreation and stable repeat counts.
- List all new or changed non-code assets and ledger rows, or explicitly state none.
- Temporary evidence workflows are allowed only as branch-scoped transport and must be removed before final mergeable head.

## Ambiguity Check

Status: PASS.

Human-approved decisions recorded on 2026-07-19:

1. The next packet should be large and meaningful rather than another narrow isolated fix.
2. The approved representative physical-map treatment now scales to the complete current ten-node/twelve-route duel scenario.
3. HRC and QXZ receive equivalent physical-map and interaction coverage; QXZ follows its already-approved visual grammar rather than becoming an HRC recolor.
4. Rules remain the existing hidden node-route graph; this is not a topology or gameplay rewrite.
5. Current scenario IDs/categories and existing player-facing text are reused; no new canon names/content are invented.
6. Final exact-head visual approval remains mandatory before merge.

Open questions: none. An implementer can complete this story without inventing mechanics, balance, topology, canon, content, or asset provenance.

## Branch / PR requirements

- Branch: `story/STORY-MAP-PHYSICAL-ROLLOUT-001-complete-duel-map`
- PR title: `STORY-MAP-PHYSICAL-ROLLOUT-001 Complete physical duel map rollout`
- Create from exact clean Unity `main` after this story's README activation pointer merges and passes post-merge CI.
- Draft PR/checkpoint required immediately after focused GREEN; do not wait for broad suites/evidence before publishing recoverable work.
- Final PR must be non-draft only after required evidence is committed and the human visual verdict is APPROVE.
- PR body must link this story and exact design commit; list the ten nodes/twelve routes, changed files/assets, RED/GREEN proof, input/raycast coverage, evidence hashes, object/material/UI counts, provenance, omissions/deferred work, exact head, and CI URLs.
- Codex must commit and push the actual implementation branch and create/update the PR. `PR-ready` or local-only work is not completion.
- Codex must not merge. Independent exact-head reviews, CI, human visual approval, merge, and post-merge verification remain external gates.

## Story readiness gate

- [x] Stable ID/title/type/parent/status/approval.
- [x] Complete approved source-authority matrix.
- [x] Exact current ten-node/twelve-route scope and categories pinned.
- [x] Runtime/data compatibility preflight completed against current scenario JSON.
- [x] Large but coherent presentation capability; unrelated gameplay remains excluded.
- [x] Large-capability estimate, expected changed surface, and mandatory stop/split rules are explicit.
- [x] Current Unity runtime/test/CI/prior-evidence surfaces are inventoried by exact path and disposition.
- [x] Two-faction parity and approved visual grammar explicit.
- [x] TDD, pointer/raycast, native evidence, performance, provenance, exact-head CI, and human visual gate explicit.
- [x] Ambiguity Check PASS and human approval recorded.
- [x] Branch/publication/recovery contract defined.

## Activation evidence

- Design authority commit: `0696abbaefc53af009b739c47a810143930a1417`; publish CI `29685079236` passed.
- Authority clarification commit: `b7bff8049af40959832e606d2bf0296b4acb1442`; publish CI `29685225278` passed.
- Readiness-blocker correction commit: `f0cfe06b36baf470e2f30e8918ba95202751ac43`; final publish/review evidence is recorded in design control before pointer activation.
- Unity README pointer PR/exact-head/post-merge CI: required before Codex execution.

## Verdict

READY / approved. The packet is complete and implementation-authorized, but Codex must fail closed until the Unity README current-task pointer is activated and verified.