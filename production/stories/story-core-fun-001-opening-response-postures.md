---
title: STORY-CORE-FUN-001 Opening Response Postures
type: story
status: done
phase: production
owner: shared
created: 2026-07-25
updated: 2026-07-25
approval: approved
related: [production/epics/epic-021-contested-crisis-core-fun-experiment, design/gdd/core-fun-prototype, design/gdd/intel-resource, docs/architecture/unity-technical-scheme, docs/architecture/testing-strategy, docs/architecture/control-manifest]
---

# STORY-CORE-FUN-001 Opening Response Postures

## Status

DONE / merged / `REJECT CLOSEOUT` in the 2026-07-26 unaided owner replaytest.

Unity PR [#192](https://github.com/myriwe-bot/neon-champions-unity/pull/192) merged on 2026-07-25 and passed its automated contract. The owner replaytest then rejected the player-facing language and could not understand the situation, alternatives, sacrifices, or selected effect. Historical implementation authority only; do not rerun this presentation contract.

## Story type

Logic + UI + Integration + Save compatibility.

## Player value

As the local player, I choose what I sacrifice before acting: route tempo, fighting strength, or a verified public account. The choice must visibly change the journey and cannot be undone.

## Binding design contract

Before normal map, base, or End Turn input, show one modal choice:

1. **Mobility / `ARRIVE FIRST`**
   - Active faction's starting Champion: `MovementPointsMaximum +2`, `MovementPointsRemaining +2`.
   - Live fixture result: `6/6 -> 8/8`.
   - Persistent refresh maximum: `8`.
   - Sacrifice copy: `No reinforcements. No verified public account.`
2. **Force / `ARRIVE READY`**
   - First active-Champion army stack: `CurrentCount +4`, `MaximumCount +4`.
   - HRC: `sled_logistics_team 5/5 -> 9/9`.
   - QXZ: `climate_bulwark 7/7 -> 11/11`.
   - Sacrifice copy: `No mobility boost. No verified public account.`
3. **Verification / `VERIFY THE FAILURE`**
   - Persist faction posture as verified Evidence/Proof state; it never reads, spends, or creates Intel.
   - Effective Central Relay hold requirement for that faction is `3`; otherwise `5`.
   - On holder change, existing hold-reset behavior remains and the effective requirement follows the new holder.
   - Rival direction copy explicitly says the rival is committed to the Central Relay.
   - Sacrifice copy: `No mobility boost. No reinforcements.`

Selection is free, immediate, saved, irreversible, and applies once. Re-selection fails without mutation. Legacy saves with no posture reopen the modal and keep prior values unchanged until selection.

## Architecture contract

- Add a faction-level posture enum/state to Domain runtime; no generalized doctrine/module framework.
- Add one engine-free Domain preview/apply service. Validate all prerequisites before mutation.
- Route player selection through `StrategicMapInputSession`; Presentation never mutates runtime directly.
- Project posture state through the application snapshot/readable adapter.
- Use a full-screen raycast-blocking opening modal; world, base, and End Turn input cannot fire through it.
- Save DTO field is backward-compatible/optional; mapper round-trips the value.
- Objective service resolves an effective hold requirement from the current holder's posture; do not permanently rewrite authored scenario data.
- Existing Intel resource amounts and Intel services are untouched.

## In scope

- Domain posture state/service and objective integration.
- Save DTO/mapping/validation compatibility.
- Input-session command/result/diagnostics.
- Readable-core-loop projection and opening modal with three exact cards.
- Bootstrap action wiring.
- Focused EditMode/domain/save/projection tests.
- PlayMode proof for both factions, modal blocking, each choice, save/resume, and no reapplication.
- Existing full CI matrix and built-player smoke.

## Out of scope

- Buildings, Assets, Operations, Signal, Intel rebalance, new resources, new units, map topology, rival AI policy, restoration mechanics, full Evidence framework, final art, tactical redesign, or generalized posture authoring.
- Claiming the decision is fun without owner replaytest.

## Acceptance criteria

- [x] New HRC and QXZ games show exactly three posture choices before normal interaction.
- [x] Modal describes exact benefit and sacrifice; no option mentions spending Intel.
- [x] Modal blocks world/base input and End Turn until successful selection.
- [x] Mobility produces `8/8` from current `6/6` and future refresh respects `8`.
- [x] Force produces exact HRC `9/9` and QXZ `11/11` first-stack results.
- [x] Verification leaves movement, army, and Intel unchanged; its holder wins at `3` own-turn checks rather than `5`.
- [x] A non-Verification holder uses `5`; a holder change resets progress and updates the displayed requirement truthfully.
- [x] Selection persists through save/resume and numerical grants are not reapplied.
- [x] Re-selection and invalid preconditions return diagnostics without partial mutation.
- [x] Legacy save payloads without posture deserialize to `None` and reopen the choice.
- [x] Existing movement, recruitment, construction, AI, battle, objective, save, and title/faction-entry tests remain green.
- [x] Exact-head CI and independent spec/code review pass before merge.

## Verification requirements

- TDD is required for production rules.
- Domain/EditMode: three previews/applies, exclusivity, invalid preconditions, effective objective requirement, control change, turn refresh.
- Save/EditMode: round trip all values; missing field becomes `None`; no grant replay.
- Projection/EditMode: exact labels, benefits, sacrifices, selected-state summary.
- PlayMode: pointer-select each option; blocked pre-choice map/end-turn input; HRC and QXZ effects; save/resume modal absence.
- Full configured Unity CI on exact PR head and exact post-merge main.
- Human: fresh owner replaytest after merge; no screenshot/video request.
- Performance: N/A beyond no per-frame rebuild; modal uses existing refresh lifecycle.

## Source authority matrix

| Path | Purpose | Status / approval | Disposition |
|---|---|---|---|
| `design/gdd/core-fun-prototype.md` | exact posture and Intel separation contract | approved / approved | required authority |
| this story | scope, architecture, values, tests | ready / approved | required authority |
| `design/gdd/intel-resource.md` | Intel non-use boundary | draft / partial | narrow approved constraint only: Intel is not Proof/posture currency |
| `docs/architecture/control-manifest.md` | Unity dependency/input controls | current repository control | required authority |
| `docs/architecture/unity-technical-scheme.md` | layer boundaries | current repository control | required authority |
| live scenario fixture at implementation base | exact starting numbers | implementation fact | required preflight, not canon |
| other draft GDDs/epics | context | mixed | excluded from implementation authority |

## Ambiguity Check

PASS. The owner approved the experiment and explicitly requested implementation. Exact tuning values and bounded technical shape are recorded here under that authority. No open decision requires invention.

## Branch / PR

- Branch: `story/STORY-CORE-FUN-001-opening-response-postures`
- PR title: `STORY-CORE-FUN-001 Opening response postures`
- PR: [myriwe-bot/neon-champions-unity#192](https://github.com/myriwe-bot/neon-champions-unity/pull/192).
- Final reviewed head: `87f6c627379ad80fdaa8f9376d705959332bfb97` — immutable review `PASS`.
- Exact-head CI: [30177057877](https://github.com/myriwe-bot/neon-champions-unity/actions/runs/30177057877) — all four required jobs passed.
- Squash merge: `673970739bace47cad255e205fbac7f7b8314fab`.
- Reviewed and merged Git tree: `014194bec33182568711d0b0f32c9a2f33b57db3`.
- Post-merge `main` CI: [30177571918](https://github.com/myriwe-bot/neon-champions-unity/actions/runs/30177571918) — all four required jobs passed.
- Owner replaytest: `REJECT CLOSEOUT` on 2026-07-26; automation could not override the human readability verdict.

## Human replaytest result

See `production/playtests/playtest-journal.md#[2026-07-26]-story-core-fun-001-opening-response-owner-replaytest--reject-closeout--choice-and-map-context-unreadable`.

Exact rejected terms include `No reinforcements`, `No verified public account`, and `stack capacity`. Their presence in the merged story records what was implemented; it no longer establishes approved player-facing design language.

## Verdict

DONE / MERGED / `REJECT CLOSEOUT` — superseded for player-facing repair by `STORY-CORE-FUN-002`.
