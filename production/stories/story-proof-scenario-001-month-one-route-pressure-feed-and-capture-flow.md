---
title: STORY-PROOF-SCENARIO-001 Month-One Route, Pressure, Feed, and Capture Flow
type: story
status: proposed
phase: production
owner: shared
created: 2026-07-15
updated: 2026-07-15
approval: pending
related: [production/epics/epic-016-accelerated-playable-product-foundation, production/planning/month-one-proof-scenario-and-capture-plan, design/gdd/product-constitution, design/ux/player-shell, production/stories/story-faction-composition-001-three-line-faction-composition-and-tactical-identity-proof]
---

# STORY-PROOF-SCENARIO-001 Month-One Route, Pressure, Feed, and Capture Flow

## Status

READY-candidate / approval pending. This packet is prepared for review but is not implementation authority. Do not run Codex until the human promotes it to `status: ready` and `approval: approved`, design/control publishes that promotion, and the Unity README current-task pointer is updated through CI.

## Value

As an HRC or QXZ player, I want one coherent faction-selectable scenario route from briefing through exploration, construction, recruitment, tactical conflict, disputed evidence, and objective resolution, so the presentable proof reads as a game rather than a collection of isolated feature demonstrations.

## Story type and estimate

Scenario Data + Existing-System Integration + Strategic Presentation + Connected PlayMode Evidence. Large story, but bounded to composing already-merged systems and one small Feed-consequence projection. No new campaign, combat, economy, information-war, or AI system.

Performance budget: no measurable regression to the current strategic/tactical frame or input baseline; no per-frame scenario reconstruction or new polling loop.

## Source authority

Required implementation authority:

- `production/planning/month-one-proof-scenario-and-capture-plan.md` — approved-provisional scenario structure, beats, map budget, shot list, and gate metrics.
- `production/epics/epic-016-accelerated-playable-product-foundation.md` — approved proof-build outcome and boundaries.
- `design/gdd/product-constitution.md` — approved product north star.
- `design/ux/player-shell.md` — approved normal-shell readability and interaction contract.
- `production/stories/story-ui-shell-001-map-first-strategic-ui-and-normal-player-shell.md` — completed faction choice/player-shell baseline.
- `production/stories/story-art-look-001-vertical-look-and-asset-provenance-integration-spike.md` — completed White Sky/provenance presentation baseline.
- `production/stories/story-base-content-001-hrc-qxz-six-facility-prototype-content-and-base-presentation.md` — completed six-facility and recruitment-content authority.
- `production/stories/story-faction-composition-001-three-line-faction-composition-and-tactical-identity-proof.md` — completed three-line composition and return-summary authority.
- `production/stories/story-pressure-001-objective-pressure-and-victory-readability-smoke.md`, `production/stories/story-pressure-002-opponent-contest-and-loss-pressure-smoke.md`, and `production/stories/story-ai-001-dumb-strategic-ai-playtest-opponent.md` — completed pressure/opponent behavior to reuse without redesign.
- `docs/architecture/control-manifest.md`, `docs/architecture/testing-strategy.md`, and `docs/architecture/ci-build-automation.md` — approved implementation, TDD, evidence, and CI rules.

Context only, not implementation authority:

- World-wiki Arctic and polluted-feed bridges explain intent but are not required reading. This self-contained story supplies every binding scenario ID, behavior, and provisional line of copy needed for implementation.
- Draft roster, final campaign naming, and broad Digital-Net/polluted-feed mechanics are explicitly excluded.

## Binding scenario-data contract

Preserve existing internal scenario/map/faction IDs for compatibility, including legacy internal identifiers that contain `greenland`; they must remain invisible in normal player-facing UI. The player-facing region remains an unnamed fictional Arctic region. Do not display `Greenland`, `Kalaallit Nunaat`, or `Meridian Shelf`.

Expand the current authored map from eight to exactly ten nodes while preserving all existing node, route, site, base, facility, offer, unit, terrain, layout, and objective IDs unless this table explicitly adds one:

| New object | Stable ID | Type / behavior | Binding data |
|---|---|---|---|
| QXZ proof cache node | `node_data_cache_beta` | site node | position `(1.75, 2.2)`; route from `node_start_b`; `data_center_perimeter` |
| QXZ proof cache site | `site_data_cache_beta` | `DataCache` | unguarded, one-time `+5 Intel`, no recruitment; readable label `Weather Archive` |
| QXZ proof route | `route_start_b_data_cache_beta` | ground route | `node_start_b` ↔ `node_data_cache_beta`; movement cost `2`; `glacier_road` |
| QXZ proof-to-center route | `route_data_cache_beta_central` | ground route | `node_data_cache_beta` ↔ `node_central_objective`; movement cost `2`; `glacier_road`; preserve as the declined direct route during the QXZ information-driven reversal |
| Calibration archive node | `node_calibration_archive` | site node | position `(0, -2.2)`; linked from central objective; `data_center_perimeter` |
| Calibration archive site | `site_calibration_archive` | `OneShotVisitSite` | unguarded, no resource reward, one-time Feed consequence; readable label `Calibration Archive` |
| Calibration archive route | `route_central_calibration_archive` | ground route | `node_central_objective` ↔ `node_calibration_archive`; movement cost `2`; `glacier_road` |

Player-facing provisional labels for the existing proof locations must be readable and replaceable through localization/projection boundaries. Use these labels for this proof without renaming stable IDs:

- `site_start_a` → `HRC Base`
- `site_start_b` → `QXZ Base`
- `site_placeholder_recruitment` → `Fishery Relay`
- `site_data_cache_alpha` → `Local Sensor Cache`
- `site_guarded_alpha` → `West Calibration Yard`
- `site_neutral_beta` → `Airstrip Relay`
- `site_guarded_beta` → `East Security Corridor`
- `site_central_objective` → `Meridian Calibration Station`

The authored opening must expose three legible first-route choices from either faction start. The existing HRC branches remain its three choices. QXZ uses `site_neutral_beta`, `site_guarded_beta`, and new `site_data_cache_beta` as its three opening branches. The Calibration Archive remains a linked central branch rather than a fourth opening choice.

The exact opening implications are asymmetric by design:

- HRC: Fishery Relay = neutral Survey Drones recruitment; West Calibration Yard = guarded weak-risk Intel; Local Sensor Cache = unguarded Intel/proof.
- QXZ: Airstrip Relay = neutral one-shot tempo/positioning; East Security Corridor = guarded strong-risk route; Weather Archive = unguarded Intel/proof. QXZ recruitment remains a visible base decision rather than a route reward.

This asymmetry satisfies the approved map budget without inventing another recruitment offer. Do not claim that each faction has a recruitment branch.

For this scenario only, change `site_central_objective.startsGuarded` from `true` to `false` and `objective.holdRequiredCount` from `2` to `5`; preserve `site_central_objective`, `node_central_objective`, and every objective/contest/victory rule. The guarded tactical battle remains on `site_guarded_alpha` or `site_guarded_beta`. The unguarded center lets the already-merged opponent capture by cycle 2, while five own-turn hold checks prevent unchanged AI from resolving victory before the player has six own turns for build, two recruits, cache, guarded battle, and central contest. This is exact scenario pacing data, not a new objective rule or AI policy.

Preserve route IDs but author the complete route array in this exact evaluation order so unchanged first-legal-route AI advances instead of entering either dead end:

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

This makes `route_start_a_neutral_alpha` the first route that matches HRC's start while leaving `route_neutral_alpha_central` first at the next node. It makes `route_neutral_beta_start_b` the first route that matches QXZ's start while leaving `route_central_neutral_beta` first at the next node. No AI policy change is authorized.

## Binding briefing contract

The faction-choice entry must include this concise normal-shell briefing before either faction is selected:

- Header: `WHITE SKY CALIBRATION FAILURE`
- Body: `A calibration station near a fishery and airstrip is issuing contradictory failure reports. Choose an emergency authority, build a response base, recover the archive, and hold the station while the rival advances. Neither account is canonical truth.`

The briefing must fit at 1920×1080, preserve the existing HRC/QXZ choice controls, and expose no internal scenario/region IDs.

## Binding connected routes

The connected proof is not an open-ended test-author choice. Automate these literal route/action sequences, while using existing legal input APIs rather than direct runtime mutation.

### HRC route

1. Choose HRC; read the binding briefing.
2. At HRC Base, build `facility_hrc_scout_relay`; use the existing starting-hub and unlocked offers to field Settlement Watch, Hunter-Scouts, and the starting Sled Logistics Team without changing costs or stock.
3. Move `node_start_a → node_neutral_alpha`; interact with Local Sensor Cache and receive its existing `+5 Intel` proof result.
4. Information-driven reversal: move `node_neutral_alpha → node_start_a → node_guarded_alpha` rather than continuing directly to center.
5. Interact with West Calibration Yard, complete the existing guarded tactical battle, and return with post-battle counts preserved.
6. Move `node_guarded_alpha → node_central_objective`; interact with/contest Meridian Calibration Station under the existing objective rules.
7. Move `node_central_objective → node_calibration_archive`; interact once and display the exact HRC Feed consequence.
8. Return `node_calibration_archive → node_central_objective`, then progress the scenario's five-own-turn hold objective to a real victory or defeat frame while the existing opponent takes its normal turns.

### QXZ route

1. Choose QXZ; read the binding briefing.
2. At QXZ Base, inspect the visible six-facility construction decision; do not mutate resources or force an illegal build.
3. Move `node_start_b → node_data_cache_beta`; interact with Weather Archive and receive its exact one-time `+5 Intel` result.
4. Information-driven reversal: move `node_data_cache_beta → node_start_b` rather than taking the still-legal direct route to center. At QXZ Base, build `facility_qxz_stratospheric_lab`, then use the existing starting-hub and unlocked offers to field Meridian Security, Strato Sensor Swarm, and the starting Climate Bulwark without changing costs or stock.
5. Move `node_start_b → node_guarded_beta`; interact with East Security Corridor, complete the existing guarded tactical battle, and return with post-battle counts preserved.
6. Move `node_guarded_beta → node_central_objective → node_calibration_archive`; contest the station normally, then interact once and display the exact QXZ Feed consequence.
7. Return `node_calibration_archive → node_central_objective`, then progress the scenario's five-own-turn hold objective to a real victory or defeat frame while the existing opponent takes its normal turns.

If either literal route is illegal under unchanged current costs/movement/turn rules, stop with the exact blocker rather than mutating resources, teleporting, suppressing opponent actions, or weakening evidence.

## Binding route-reversal cue

The first interaction with `site_data_cache_alpha` or `site_data_cache_beta` preserves its existing one-time `+5 Intel` reward and adds only this state-backed Feed guidance:

- Shared fact: `Partial maintenance index recovered. The direct station route omits locally serviced calibration yards.`
- HRC direction: `Cross-check West Calibration Yard before advancing.`
- QXZ direction: `Cross-check East Security Corridor before advancing.`
- Provenance/status: `Source: cache index • Status: incomplete.`

The direct cache-to-center route remains visibly legal. The connected proof deliberately backtracks to the named guarded yard/corridor because of this incomplete-source cue; that is the approved information-driven route reversal. Do not unlock/lock routes, change rewards, or create hidden information state.

## Binding Feed-consequence contract

Interacting with `site_calibration_archive` after reaching it through normal movement produces one state-backed, one-time Feed result. This is presentation/content integration, not a new information-state, reputation, Proof-resource, propaganda, or branching-narrative system.

The visible Feed result must contain all three layers:

1. Shared event fact: `Calibration archive recovered: sensor drift and delayed maintenance confirmed.`
2. Active-faction interpretation:
   - HRC: `HRC: local witnesses say continuity powers concealed preventable risk.`
   - QXZ: `QXZ: damaged sensors cannot distinguish sabotage from maintenance failure.`
3. Provenance/status: `Source: station archive + local witness relay • Status: disputed.`

Both interpretations describe the same recovered event, neither is canonical truth, and choosing a faction changes only the visible interpretation—not rewards, objective rules, or hidden simulation state. Repeated interaction must not reapply or duplicate the consequence.

## In scope

- Make the existing player-entry faction choice start either HRC or QXZ as the human side and set only the unchosen side to the completed `StrategicAI` controller; do not add AI behavior.
- Author and validate the exact ten-node topology above.
- Preserve the six-facility, three-line composition, objective hold/contest, tactical handoff/result, and return-summary contracts.
- Connect the literal deterministic HRC and QXZ routes through faction choice, briefing, first tradeoff, information-driven reversal, facility decision, recruitment/composition, guarded battle, Calibration Archive Feed consequence, and real existing-rule victory/defeat resolution.
- Show opponent movement and central-objective capture/pressure by cycle 2 using the exact unguarded-center, five-check hold, and complete route-order data contract above; do not retune AI.
- Replace normal-shell placeholder/raw location copy on the proof route with the provisional labels above while keeping stable IDs in debug/domain state.
- Add focused scenario validation for new IDs, routes, site behavior, and duplicate/missing references.
- Produce the approved eight-shot capture list plus the required second-faction Feed counterpart using real normal-shell gameplay at 1920×1080.

## Out of scope

- Final region, settlement, station, or campaign names; final canon; new factions or Champions.
- New campaign framework, scenario selector beyond the existing faction entry, save/load, tutorial, dialogue system, cutscenes, quest graph, branching narrative, or editor UI.
- New resources, facilities, offers, units, balance, tactical mechanics, objective/victory rules, opponent logic, pathfinding, or economy.
- Proof/Attention/Reputation resources; polluted-information states; false reports; provenance simulation; propaganda choices; fog-of-war; route unlocking; legal/admissibility systems.
- Final art, models, animation, audio, VFX, icons, or broad localization framework.
- Renaming legacy internal IDs solely to remove `greenland` or `placeholder`; normal UI must sanitize them instead.

## Acceptance criteria

- [ ] Normal player entry can start either HRC or QXZ as the human faction, with the existing opponent controlling the other side and no hotseat-only step required for the connected proof.
- [ ] The exact binding briefing appears before faction choice, fits the normal 1920×1080 shell, and contains no raw/internal IDs or forbidden region names.
- [ ] Imported and fallback scenarios contain exactly ten nodes and the exact new node/site/route definitions above.
- [ ] Both faction starts expose the exact three readable opening choices and asymmetric implications specified above; recruitment remains available through HRC's Fishery Relay and both faction bases, without adding an offer.
- [ ] `site_central_objective` is unguarded only in this scenario, `holdRequiredCount` is exactly `5`, the objective engine/rules are unchanged, and route authoring order lets the unmodified opponent capture/pressure center by cycle 2 while leaving the player the exact five-check counterplay window needed to reach it.
- [ ] Normal UI uses the binding provisional location labels and exposes no raw node/site/route/faction IDs, unresolved localization keys, `Greenland`, or player-facing placeholder terms on story-owned states.
- [ ] Both proof caches preserve the existing one-time `+5 Intel` reward and show the exact shared incomplete-source fact, active-faction yard/corridor direction, and provenance/status cue without changing route legality or hidden state.
- [ ] The literal connected HRC and QXZ routes above pass through normal input/turn APIs and prove faction choice, briefing, route tradeoff and reversal, facility choice, recruitment/composition, guarded tactical handoff/result, return to strategic state, Feed consequence, and real victory/defeat resolution.
- [ ] The Calibration Archive Feed result is state-backed, one-time, faction-specific only in interpretation, and contains the exact shared fact, selected interpretation, and provenance/status lines.
- [ ] The existing objective hold/contest/victory engine and dumb opponent behavior are reused unchanged; only the explicitly authorized scenario guard flag, five-check hold pacing, route order, new nodes/sites/routes, labels, and Feed/briefing presentation change.
- [ ] A timed normal-input proof run from title entry to real resolution completes in 20–30 minutes without developer intervention; the evidence README records faction, start/end timestamps, elapsed time, route deviations, and any failed unaided task.
- [ ] Existing movement, base/economy, recruitment, three-line army, tactical, Sensor Lock, AI, objective, import/fallback, and return-summary tests remain green.
- [ ] No new external/generated non-code asset is introduced; if implementation unexpectedly needs one, stop rather than bypass the provenance contract.
- [ ] EditMode, PlayMode, validator, standalone build, exact-head PR CI, and post-merge main CI pass.

## Verification and evidence

Required evidence under `production/evidence/STORY-PROOF-SCENARIO-001/`:

- `01-hero-map-pressure-1920x1080.png` — White Sky, readable routes, active base and Champion, three opening choices, rival movement/central pressure.
- `02-hrc-base-construction-1920x1080.png` — HRC six-facility choice and selected/constructed response.
- `03-qxz-base-construction-1920x1080.png` — QXZ six-facility choice and contrasting selected/constructed response.
- `04-army-champion-composition-1920x1080.png` — normal-shell Champion selection with readable three-line composition.
- `05-tactical-wide-intent-1920x1080.png` — readable factions, three-line deployment, terrain, objective, and intended action.
- `06-tactical-close-action-1920x1080.png` — close action with command/target forecast and real result feedback; QXZ Sensor Lock is the preferred existing-system proof.
- `07-feed-reveal-hrc-1920x1080.png` — shared fact, exact HRC interpretation, and provenance/status without a text wall.
- `08-victory-or-defeat-1920x1080.png` — real existing-rule resolution with consequence and next-question hook.
- Supplemental `07b-feed-reveal-qxz-1920x1080.png` — exact QXZ interpretation of the same shared fact and provenance/status. This is required because one still cannot prove both faction-selectable interpretations.
- README with hashes, exact test names, timed-run record, exact-head CI URL recorded on the PR, changed-asset inventory, and omissions.

Automated capture assertions must bind semantics to named player-facing objects, verify active 1920×1080 render state, bounds/non-overlap/text fit, exact labels/Feed lines, and absence of raw IDs/placeholders. Regenerate each materially different full-shell capture from a fresh scene/process if sequential capture causes ghosting.

The approved plan's 30–60 second video remains required at EPIC-016 capability-sequence step 6, the human proof-build playtest/gate review. This story must add `capture-sequence.md` beside the stills with an exact ordered real-gameplay recording script, target duration per segment totaling 30–60 seconds, shot-to-acceptance mapping, and a prohibition on camera-only mockups. Video recording/editing/export is intentionally sequenced to the human gate rather than smuggled into this Unity integration story; promoting this candidate constitutes explicit approval of that sequencing, not cancellation of the video target.

## Ambiguity gate

PASS as a candidate design: the exact topology additions, provisional labels, Feed copy, reuse boundaries, and evidence contract are specified. Implementation approval is still pending. Human approval may accept this packet as written or revise its scenario labels/copy before promotion. Do not infer approval from preparation alone.

## Proposed branch / PR

- Branch: `story/STORY-PROOF-SCENARIO-001-month-one-route-pressure-feed`
- PR title: `STORY-PROOF-SCENARIO-001 month-one route pressure Feed and capture flow`
- Evidence path: `production/evidence/STORY-PROOF-SCENARIO-001/`

## Verdict

READY-candidate / approval pending. Recommended next EPIC-016 packet after the merged faction-composition proof; not runnable until explicit human approval and Unity pointer activation.
