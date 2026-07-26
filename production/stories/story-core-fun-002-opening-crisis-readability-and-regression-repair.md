---
title: STORY-CORE-FUN-002 Opening Crisis Readability and Regression Repair
type: story
status: done
phase: production
owner: shared
created: 2026-07-26
updated: 2026-07-26
approval: approved
related: [production/epics/epic-021-contested-crisis-core-fun-experiment, production/stories/story-core-fun-001-opening-response-postures, production/playtests/playtest-journal, design/gdd/core-fun-prototype, design/ux/player-shell, docs/architecture/unity-technical-scheme, docs/architecture/testing-strategy, docs/architecture/control-manifest]
---

# STORY-CORE-FUN-002 Opening Crisis Readability and Regression Repair

## Status

DONE / MERGED / OWNER REPLAYTEST PENDING. Unity PR #194 merged the repair, and delayed-review follow-up PR #196 merged as `0149668ecf2bd0dd21f119923922296b91227697`, closing the surviving P1 Force-feedback and Central-Relay-name gaps. Automation proves the bounded contracts; it does not prove first-contact comprehension or fun.

## Delayed independent review repair

- Force result must name the actual first-stack unit and report HRC `5 -> 9` or QXZ `7 -> 11` immediately after selection.
- The same `site_central_objective` must be player-facing `Central Relay` in the briefing, physical map object, selection title, objective text, and relevant tests.
- Existing mechanics, layout, gate, save behavior, and all other site names remain unchanged.
- Follow-up candidate `a0f5bedbfa76dc091a1d4717626e7810350e275d` passed exact-head run `30196880961`; merge and candidate trees are identical at `6f66b38ae3fc382e8cba6c00f614229923214fe1`.

## Implementation evidence

- Design authority: `b8b2d06984ec30bcd0b6cf64ca18495394273901`; publish run `30194390046` passed.
- Unity activation pointer: PR #193 merged as `b6cf9125214cbc4270aa78d48357e6b04e604c8f`.
- Unity implementation: PR #194.
- Final candidate head: `cbcc0aafd2e8af2b402bcb0d34b6a367af7bf73c`.
- Exact-head CI: run `30195930086` passed Compile/Standalone launch, EditMode, PlayMode, and Placeholder Validator.
- Merge: `b2e6344091b6a58514302f8f43d1b23cfb95ebc5`.
- Candidate and merge trees are identical at `12c805088f0dd9d637e1c777346ac1c70ce384ef`; redundant post-merge run `30196206689` was cancelled.
- Manual evidence run `30195477014` at preceding runtime-equivalent head `dbc238834b73371f1bb82e6e0c81947bcad2baa9` passed and generated 240 files, but GitHub rejected artifact creation because the repository artifact-storage quota was full. No screenshot inspection is claimed.

## Story type

UI + Visual/Feel + Integration + regression repair + human replaytest preparation.

## Player value

As a new player, I understand the emergency, the map’s basic orientation, the rival’s commitment, the objective, all three opening alternatives, and exactly what changes after I choose—without reading a design document or decoding internal terminology.

## Human rejection authority

Source: `production/playtests/playtest-journal.md#[2026-07-26]-story-core-fun-001-opening-response-owner-replaytest--reject-closeout--choice-and-map-context-unreadable`.

The implementation must preserve the exact complaints there, including:

- “I do not understand what the sacrifices mean.”
- “What is ‘no reinforcements’ or ‘no verified public account’?”
- “This is not in accordance to our design language and not approved by me.”
- “Also, what is stack capacity?”
- “I know nothing on the rival.”
- “I do not know where the objective is.”
- “I do not know how large the map itself is even.”
- “The ‘End turn’ button is once again unlabeled.”

## Binding repair contract

### Preserve mechanics; replace rejected language

This story does not redesign the effects. It preserves the current bounded experiment:

- Movement: active Champion `6/6 -> 8/8`, including turn refresh.
- Force: HRC first stack `5/5 -> 9/9`; QXZ first stack `7/7 -> 11/11`.
- Relay preparation: if the faction controls the Central Relay, required own-turn hold progress is `3` rather than `5`.

Normal player copy must not contain `posture`, `stack capacity`, `verified public account`, `No reinforcements`, or `checks` when it means turns.

### Opening briefing

Before the cards, show four plainly separated facts:

1. `WHAT IS HAPPENING` — the Central Relay supports navigation, emergency communications, and clinic/port coordination, and it is failing.
2. `WHERE` — a truthful orientation strip from the player’s starting base, through the Central Relay near the middle of the playable map, to the rival’s starting base. This is orientation, not a tile grid, boundary, or exact minimap.
3. `RIVAL` — identify the actual rival faction, its opposite starting side/direction, and its current commitment to taking the Relay only where supported by current scenario/AI facts.
4. `OBJECTIVE` — reach and take the Central Relay, then hold it for the current required turns.

### Comparable cards

Each card presents the same fields in the same order:

- concrete action first;
- exact immediate/current change;
- exact values left unchanged.

Required meanings:

- Move farther: movement `6 -> 8`; starting army count and Relay hold requirement remain unchanged.
- Bring four more units: name the actual first-stack unit and show HRC `5 -> 9` or QXZ `7 -> 11`; movement and Relay hold requirement remain unchanged.
- Shorten the Relay hold: after taking the Relay, hold `3 turns instead of 5`; movement and starting army count remain unchanged.

Flavor labels may remain secondary replace-later labels. They cannot carry the explanation.

### Keyword hover-help trial

Add one shallow reusable hover/focus help layer for legitimate terms still visible in the repaired copy, initially Central Relay, Movement, Army, and Hold turns or the exact final equivalents.

- Highlighted terms have a consistent accent and affordance.
- Hover or keyboard focus opens one concise tooltip in a stable screen-bounded panel.
- Exit/focus change closes it.
- No nested tooltips or encyclopedia in this story.
- The opening remains understandable when no tooltip is opened.

### Selected effect visibility

After selection:

- show an immediate factual result banner with the exact `before -> after` or `5 -> 3 turns` consequence;
- show a dedicated persistent response badge near the relevant Champion/objective state, not buried in the faction text block;
- pair the badge with the changed movement, named army count, or objective requirement;
- restore the same badge/value through Save -> title -> process-compatible Continue without reapplying the grant.

### Regression repair

- `END TURN` and `Save / Menu` must render visibly, non-empty, unclipped, and inside their control bounds at 1280x720, 1920x1080, and one resized state.
- Objective, rival, and selected-response text receive equivalent production-path visibility/bounds checks.
- Inspect native evidence to identify the reported blue lines. Remove/recolor/recompose only if evidence proves they falsely read as a boundary; do not infer the cause from a color constant.
- Verify existing base opening, base-return movement, panning, zoom, fullscreen crispness, recruitment explanation, rival visibility, and objective landmark. Fix only proven regressions.

## In scope

- Readable opening projection and canvas composition.
- A bounded reusable keyword hover/focus component.
- Persistent selected-response presentation.
- Production-path layout and visibility regression tests.
- HRC/QXZ parity and existing save/Continue integration.
- Native evidence and exact-head CI/review.

## Out of scope

- New posture effects or balance.
- Final names, canon, crisis truth, accepted-account system, Evidence framework, rival adaptation, restoration, route rewrite, movement topology, AI policy, combat cadence, economy/buildings, Champion depth, unit design, tactical redesign, final art, audio, or generalized encyclopedia.
- Claiming the decision or wider game is fun before owner replaytest.

## Acceptance criteria

- [ ] Within 30 seconds and without tooltips, a new player can identify the emergency, own start, Central Relay, rival faction/direction/commitment, objective, map orientation, three choices, and each opportunity cost.
- [x] Normal opening UI contains none of the rejected/internal terms.
- [x] HRC and QXZ force cards use actual unit display names and exact faction-specific counts.
- [x] Each card states exact change and exact unchanged alternatives in the same comparison structure.
- [x] Tooltip terms highlight consistently; hover/focus shows accurate bounded help; exit/focus change closes it; no nested system is added.
- [x] Full-screen modal and application command gate continue to block map, drag, zoom, WASD, pause, save, and End Turn until selection.
- [x] Selection shows an immediate exact result and a persistent dedicated badge paired with the changed runtime value.
- [x] Save/Continue preserves the response, value, badge, and no-reapplication behavior; legacy saves reopen the repaired choice.
- [x] END TURN, Save / Menu, objective, rival, and response badge are covered by production-path presence and bounds checks, including focused 1280x720 HRC/QXZ opening paths.
- [ ] Native evidence resolves the reported blue-line concern truthfully and confirms no false boundary cue remains in normal opening/map play.
- [x] Existing base, movement, camera, display, recruitment, opponent, battle, objective, and save regressions remain green.
- [ ] Exact-head CI passed before merge and independent pre-implementation audit findings were incorporated, but the combined independent code/visual criterion remains open because native artifact delivery failed and no screenshot inspection is claimed.
- [ ] Fresh standalone owner replaytest remains pending after merge; automation does not claim acceptance.

## Verification requirements

- TDD for projection/help/layout behavior where feasible.
- EditMode: faction-specific projection, forbidden-copy checks, comparison fields, help catalog, selected summary.
- PlayMode: title -> faction -> repaired opening; pointer and keyboard help; input/command gate; each response; visible labels/bounds; post-choice badge; HRC/QXZ parity; Save/Continue and legacy save.
- Evidence: native 1920x1080 HRC and QXZ openings, post-choice state for all effects, and 1280x720 layout proof under a story-scoped evidence directory.
- CI: Compile/Standalone, EditMode, PlayMode, Placeholder Validator on one immutable candidate head.
- Human: fresh owner replaytest with no screenshot/video request.

## Source authority matrix

| Path | Purpose | Status / approval | Disposition |
|---|---|---|---|
| `production/playtests/playtest-journal.md` 2026-07-26 entry | exact rejection and acceptance drivers | approved evidence | required authority |
| this story | bounded repair contract | ready / approved | required authority |
| `design/gdd/core-fun-prototype.md` | experiment and current numerical effects | approved with 2026-07-26 terminology correction | required narrow authority |
| `design/ux/player-shell.md` | normal-shell hierarchy | approved | required authority where non-conflicting |
| architecture/testing/control docs | boundaries and evidence | current | required authority |
| live scenario/snapshot/runtime | faction values, names, rival/map facts | implementation facts | required preflight, not canon |
| deeper EPIC-021 drafts | future crisis depth | draft | excluded |

## Ambiguity Check

PASS for this bounded repair. The owner authorized radical correction and implementation. Existing numbers are preserved; rejected phrases are removed; no new mechanic or canon is required. If truthful rival commitment, map orientation, or blue-line diagnosis cannot be derived from current implementation facts, stop that subpart rather than inventing an answer.

## Branch / PR

- Branch: `story/STORY-CORE-FUN-002-opening-crisis-readability`
- PR title: `STORY-CORE-FUN-002 Opening crisis readability and regression repair`
- Publish an early draft checkpoint after focused GREEN.
- Final candidate requires exact-head CI, independent review, native evidence inspection, and non-draft PR.
- Completion requires commit, push, PR, merge, and post-merge/tree-identity reconciliation; `PR-ready` is not completion.

## Verdict

DONE / DELAYED P1 REVIEW CLOSED / OWNER REPLAYTEST PENDING — deeper crisis implementation remains blocked.
