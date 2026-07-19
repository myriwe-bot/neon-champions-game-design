---
title: STORY-CHAMPION-ARMY-INTERACTION-001 Discoverable Champion Army and Selection Continuity
type: story
status: done
phase: production
owner: shared
created: 2026-07-18
updated: 2026-07-19
approval: approved
related: [production/epics/epic-018-physical-adventure-map-and-player-entry-recovery, production/stories/story-map-visual-slice-001-physical-arctic-adventure-map-and-shell, production/stories/story-prototype-continuity-qa-001-build-resume-pressure-playtest-closeout, design/gdd/strategic-map, design/ux/player-shell, design/art/prototype-visual-target-and-asset-ledger, docs/architecture/unity-technical-scheme, docs/architecture/testing-strategy, docs/architecture/ci-build-automation, docs/architecture/control-manifest]
---

# STORY-CHAMPION-ARMY-INTERACTION-001 Discoverable Champion Army and Selection Continuity

## Status

DONE / approved / merged / post-merge verified. Unity PR #174 merged as `07aec85501a12252c5370e9e41a301c0f1afa0bf` after exact-head CI and two immutable reviews passed at implementation head `bffeb0b9969081d635adc0a28579c484911fc6ce`. Post-merge Unity `main` run `29684259824` passed all four configured jobs.

Approval basis: the human owner instructed the agent on 2026-07-18 to verify/fix/merge the current story, prepare the next implementation packet, and continue until done. Scope is bounded to the already-approved order-3 interaction follow-up and preserved player complaint below.

## Story type

UI / Integration / Test.

## Parent epic

- `production/epics/epic-018-physical-adventure-map-and-player-entry-recovery.md`

## Player value

As a player, I need Champion selection to reveal a structured, stable view of the actual attached army and to survive switching between Champion and base context, so I can find my units, understand current counts and roles, and know what is selectable without decoding a debug summary or assuming a nonexistent inventory system.

## Exact complaint preserved as acceptance authority

- "Champion inventory and units/stacks could not be found."

The prior slice fixed physical-map readability and direct base opening. This follow-up closes the remaining army-discovery complaint; it must not reframe it as a request for a new inventory or stack-management system.

## Source-authority matrix

| Path | Approved sections / purpose | Disposition |
|---|---|---|
| `production/stories/story-champion-army-interaction-001-discoverable-champion-army-and-selection-continuity.md` | exact scope, acceptance, evidence, branch | required authority |
| `production/epics/epic-018-physical-adventure-map-and-player-entry-recovery.md` §§Human authority, Gate, Capability sequence, Boundaries | ordered repair train | required authority |
| `production/stories/story-map-visual-slice-001-physical-arctic-adventure-map-and-shell.md` §§Exact complaints, Champion and army summary, Base and site interaction, Out of scope | approved predecessor and replacement boundary | required authority |
| `design/gdd/strategic-map.md` §§6 Core Loop Contract, 8 UX / Readability Requirements Draft | Champion selection, movement, interaction visibility | required authority |
| `design/ux/player-shell.md` §§Global principles, Strategic shell, Base screen/panel, Accessibility baseline | map dominance, contextual selection, army summary, explainable actions | required authority |
| `design/art/prototype-visual-target-and-asset-ledger.md` §Champion and army representation | one selectable Champion; cosmetic entourage boundary | required authority |
| `docs/architecture/unity-technical-scheme.md` | presentation/application/domain boundaries | required authority |
| `docs/architecture/testing-strategy.md` §§Required Test and Evidence Layers | TDD and PlayMode/input evidence | required authority |
| `docs/architecture/ci-build-automation.md` | exact-head build/test gate | required authority |
| `docs/architecture/control-manifest.md` §§1-5 | implementation, source, architecture, data controls | required authority |
| current Unity `StrategicMapPresentationSnapshot`, `StrategicHeroBarSnapshot`, `StrategicHeroBarArmySlotSnapshot`, `StrategicPlayerShellViewModel` | existing snapshot/role/count facts | implementation facts only; do not turn placeholders into design authority |

## In scope

- Preserve the approved physical HRC map composition and map-dominant shell.
- When the physical HRC Champion is selected through the normal Input System/raycast path, show one structured army slot/card per actual current `StrategicHeroBarArmySlotSnapshot` in stable snapshot order.
- Each visible army slot must show the player-facing unit name, current/maximum count, and truthful player-facing role text already supplied by the snapshot/view-model boundary.
- Make the selected Champion state visibly stable and distinguishable without color alone; the structured army region must remain visible until the player selects a different valid context.
- Switching Champion -> HRC base -> Champion through real pointer input must replace context cleanly in both directions: base facilities must not remain over the Champion panel, and Champion army cards must not remain over the base catalog.
- Keep the existing action bar explainable. If stack rearrangement, inventory, equipment, or per-stack actions are unavailable, show no active control for them. One concise non-interactive deferral statement is allowed only if necessary to prevent a false affordance.
- Preserve the existing direct HRC-base open/build context and the current physical Champion/map pointer behavior.
- Use current snapshot data; update correctly after existing recruitment or battle-loss state changes without hardcoded stack names/counts.
- Add focused automated coverage and exact evidence at 1920×1080.

## Out of scope

- New inventory, equipment, loot, Champion progression, level/class mechanics, stack rearrangement, split/merge/transfer, per-stack map actions, unit upgrades, recruitment rules, combat rules, balance, economy, AI, save schema, topology, scenario data, movement rules, new units/facilities/content, tactical UI, or final art.
- Making cosmetic entourage members independently selectable or mapping one visual follower to one stack/count.
- Full-map/QXZ physical conversion, map-layout redesign, new route/site art, or broad onboarding.
- Raw IDs, localization keys, debug summaries, fabricated portraits, fake buttons, disabled-button walls, or controls that bypass normal application commands.
- New packages, settings, render-pipeline changes, scene ownership changes, broad refactors, or unrelated CI changes.

## Allowed placeholders and temporary data

- Existing code-built/ledgered prototype visual assets and the approved HRC physical slice remain replace-later.
- Existing truthful `Class: prototype`, `Level: prototype`, or `Stack rearrangement deferred` data may remain only when it does not imply implemented mechanics or crowd the normal army view.
- No new gameplay mock, fake inventory, synthetic army data, or unlabeled AI-generated asset.

## Dependencies

- `STORY-STANDALONE-ENTRY-001`: DONE and post-merge verified.
- `STORY-MAP-VISUAL-SLICE-001`: DONE and post-merge verified before this packet activates.
- Existing snapshot army-slot data and player-facing role labels must be consumed, not duplicated.
- Existing normal pointer/raycast and application-command paths remain authoritative.

## Acceptance criteria

- [ ] Production title -> Play HRC reaches the approved physical slice with no regression.
- [ ] Clicking the physical HRC Champion through real Input System pointer/raycast input selects `champion_1` and reveals exactly the current attached army slots from the snapshot.
- [ ] Every visible slot shows player-facing unit name, current/maximum count, and truthful role text; no raw stack/unit/faction/node IDs or localization keys are visible.
- [ ] Initial HRC evidence truthfully includes the current Sled Logistics Team snapshot entry and any other stacks actually present; tests derive expected names/counts from the snapshot/catalog rather than fabricating state.
- [ ] The army view uses structured cards/rows rather than one dense debug-like line and fits at native 1920×1080 without clipping, overlap, or covering critical map context.
- [ ] Selected Champion state remains distinguishable beyond hue and persists until another valid context is selected.
- [ ] Champion -> HRC base through pointer input removes/replaces the Champion army context and opens the existing base catalog; HRC base -> Champion restores the current army context and removes/replaces the base catalog.
- [ ] Recruitment or battle-loss changes already supported by the game are reflected from the next snapshot without stale or hardcoded counts.
- [ ] No clickable inventory, equipment, rearrangement, transfer, or per-stack action is shown unless an existing application command actually supports it; this story adds none.
- [ ] Existing movement, base build, recruitment, battle handoff, topology, save, AI, and domain behavior remain unchanged.
- [ ] Keyboard/mouse focus order and meaningful selected/card boundaries do not rely on color alone; normal text and boundaries retain approved contrast baselines.
- [ ] Exact-head EditMode, PlayMode, validator, compile, and repeated standalone entry checks pass.
- [ ] Required native evidence is inspected and receives explicit human APPROVE / REVISE / REJECT before merge.

## Verification requirements

- TDD: required. Capture focused RED before production changes and GREEN afterward for structured slot mapping and Champion/base/Champion context replacement.
- EditMode: snapshot/view-model mapping, stable order, player-facing names/roles/counts, no fabricated inventory/action state, and data-driven count refresh.
- PlayMode: production HRC path plus real Input System/raycast Champion -> base -> Champion sequence; assert exact visible card count/content, catalog replacement, no stale panel, no raw IDs, and fit/overlap policy.
- Regression: full configured EditMode, PlayMode, placeholder/provenance validator, compile, and two-launch Windows player smoke.
- Native 1920×1080 PNGs under `production/evidence/STORY-CHAMPION-ARMY-INTERACTION-001/`:
  1. `champion-army-selected-1920x1080.png`;
  2. `base-after-champion-1920x1080.png`;
  3. `champion-after-base-1920x1080.png`.
- Evidence README: exact SHA, source/data inventory, RED/GREEN proof, commands/results, PNG dimensions/hashes, raw-ID/path/fit checks, changed files, omissions, and performance/object-count note.
- Performance: no per-frame card/object/material recreation beyond the existing snapshot-triggered rebuild; record before/after UI object count for the three required states.
- Human gate: inspect all native PNGs at exact head. Automation cannot waive the visual/discoverability verdict.

## Ambiguity Check

Status: PASS.

Resolved:

- “Inventory” in the complaint does not authorize an inventory system. The packet exposes only the real attached army data and explicitly avoids false inventory affordances.
- The HRC representative slice remains the bounded proof surface. Full-map/QXZ conversion is excluded.
- Base behavior is regression/selection-continuity scope, not new base mechanics.
- Actual snapshot data controls stack count/order/content.

Open questions: none.
Human-approved exceptions: none.

## Branch / PR requirements

- Branch: `story/STORY-CHAMPION-ARMY-INTERACTION-001-discoverable-army-selection`
- PR title: `STORY-CHAMPION-ARMY-INTERACTION-001 Discoverable Champion army selection`
- Required starting head: Unity `main` `b634439960d08165ce44a3745ead2d1d62ddaecf`, the post-merge-verified README activation pointer commit; create the story branch from exactly this clean head.
- Non-draft PR required only after exact evidence is committed and human visual verdict is APPROVE; use draft during implementation/review.
- PR must link this story, list exact source/design SHAs, RED/GREEN proof, changed files, native evidence hashes, CI URLs, omissions/deferred work, and exact head.
- Codex must checkpoint, commit, push, and create/update the PR immediately after focused GREEN and before broad suites or evidence capture.
- If a local run stops with story-owned files plus preserved Unity settings drift, resume with `production/sprints/codex-story-champion-army-interaction-001-local-recovery.prompt.txt`; do not restart or discard the local implementation.

## Story readiness gate

- [x] Stable ID, title, type, parent, status, and delegated human approval.
- [x] Exact approved source matrix.
- [x] Bounded in/out scope and placeholder rules.
- [x] Observable acceptance criteria and correct evidence layers.
- [x] TDD, normal pointer path, native evidence, exact-head CI, and human gate required.
- [x] Ambiguity Check PASS.
- [x] Branch/PR/omissions contract defined.

## Verdict

DONE / approved / merged / post-merge verified. Final implementation head `bffeb0b9969081d635adc0a28579c484911fc6ce` passed exact-head CI run `29683728194` and immutable domain/runtime plus UI/tests/evidence review. Unity PR #174 merged as `07aec85501a12252c5370e9e41a301c0f1afa0bf`; post-merge `main` run `29684259824` passed Compile/Standalone, EditMode, PlayMode, and Placeholder Validator. Structured army discovery, runtime refresh, and Champion -> base -> Champion context replacement shipped without domain/application/scenario/rule drift.
