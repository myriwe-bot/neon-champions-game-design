---
title: STORY-QA-008 Strategic Map Region Playtest and Closeout Review
type: story
status: ready
phase: production
owner: shared
created: 2026-06-18
updated: 2026-06-18
source_lore: [greenland, white-sky, digital-net]
related:
  [
    production/epics/epic-vslice-mvp-007-strategic-map-readability-bases-and-spatial-presentation,
    production/stories/story-strat-map-region-001-region-site-presentation-prototype,
    design/gdd/strategic-map,
    design/research/homm-like-strategic-map-topology-reference,
    docs/architecture/control-manifest,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-QA-008 Strategic Map Region Playtest and Closeout Review

## Status

READY / approved. Human approval recorded 2026-06-18 from chat: `Approved`, in response to the guarded `STORY-QA-008` closeout candidate.

Approved scope: a narrow EPIC-007 closeout/review pass that replays the current vertical-slice strategic map at 1280x720, verifies the new region/site/corridor presentation is readable and clickable, and fixes only concrete readability/clickability regressions found during that review.

## Story type

QA / Playability Review + Narrow Fix Pass.

## Parent epic

- [EPIC-VSLICE-MVP-007 Strategic Map Readability, Bases, and Spatial Presentation](../epics/epic-vslice-mvp-007-strategic-map-readability-bases-and-spatial-presentation.md)

## User/player/system value

As a player, I need the now-merged strategic map readability, base reinforcement, and region/site presentation work to be reviewed as one playable surface before the project starts another mechanics train, so the next design decision is based on actual readability evidence rather than isolated green CI.

## Source requirements

- Parent epic:
  - `production/epics/epic-vslice-mvp-007-strategic-map-readability-bases-and-spatial-presentation.md` DONE gate and child-story outcomes.
- Merged story evidence:
  - Unity `production/evidence/STORY-STRAT-READ-002/`.
  - Unity `production/evidence/STORY-STRAT-BASE-001/`.
  - Unity `production/evidence/STORY-STRAT-MAP-REGION-001/`.
- GDD/reference:
  - `design/gdd/strategic-map.md` §§1-13.
  - `design/research/homm-like-strategic-map-topology-reference.md` Option B and minimum map readability contract.
- Control/verification:
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

## In scope

If approved, this story may:

- Replay or run the strategic-map prototype at 1280x720 and inspect the current region/site/corridor map surface.
- Verify that active faction/Champion, reachable destinations, path costs, site categories, guarded/ownership state, starting-hub reinforcement, and selected-site interaction previews remain understandable together.
- Fix only concrete player-facing readability/clickability regressions found during the review, such as overlapping labels, unreachable/colliding buttons, illegible site/corridor text, misleading interaction preview text, or missing return-summary/readability text already required by EPIC-007.
- Add or update PlayMode smoke tests and PNG evidence under `production/evidence/STORY-QA-008/` showing the reviewed/fixed surface.
- Produce a concise closeout verdict recommending the next epic direction: strategic playtest iteration, tactical unit/data depth, base/recruitment depth, or pause for human playtest.

## Out of scope

Not authorized by this story:

- No new strategic mechanics, economy, base/town-building system, garrisons, reserves/caravans, recruitment stock economy, or tactical rules.
- No tile/hex/freeform movement, terrain pathfinding, road modifiers, fog/scouting/logistics/weather, strategic AI, procedural generation, or map editor.
- No final art/icons/VFX/audio/animation/localization/content rewrite.
- No broad UI redesign beyond concrete readability/clickability fixes found during the closeout review.
- No next-epic implementation without separate READY story approval.

## Allowed stubs, mocks, placeholders, or temporary data

- Existing prototype region names, site labels, corridor labels, tints, marker shapes, and screenshots may remain placeholders if readable enough.
- Additional diagnostic/test-only labels or evidence captures are allowed if they do not become new design authority.

## Dependencies

- `STORY-STRAT-READ-002` DONE / merged.
- `STORY-STRAT-BASE-001` DONE / merged.
- `STORY-STRAT-MAP-REGION-001` DONE / merged.
- Current Unity `main` post-merge CI green for all three stories.

## Acceptance criteria

- [ ] The strategic map at 1280x720 can be inspected with the merged EPIC-007 surface active.
- [ ] Player-facing readability is judged against the minimum map readability contract: active actor, movement/reachability, path cost, site category, ownership/guarded state, interaction preview, battle/return context where available.
- [ ] Any concrete in-scope readability/clickability blocker discovered is fixed and covered by PlayMode smoke/regression evidence.
- [ ] Evidence PNGs under `production/evidence/STORY-QA-008/` show the final reviewed surface.
- [ ] Unity Foundation CI passes on exact PR head before merge.
- [ ] Closeout verdict records whether EPIC-007 is accepted, needs another narrow readability fix, or should pause for human playtest/next-epic decision.

## Verification requirements

- Unity PlayMode smoke/evidence is required if any Unity code/UI changes are made.
- EditMode tests are required for any application/domain projection changes.
- Placeholder validator must remain green.
- Exact-head Unity Foundation CI is required before merge.
- If no code changes are made after review, evidence and closeout documentation must still record what was inspected and why no fix was needed.

## Ambiguity Check

Status: PASS. Human approval recorded 2026-06-18.

Human-approved answers:

1. Yes: run this closeout/review pass before starting the next mechanics/design epic.
2. Codex may fix concrete readability/clickability issues it finds during review if they are directly tied to EPIC-007 commitments.
3. If review passes, record a closeout verdict; do not start the next epic without separate human direction.

Approved assumptions:

- This is a narrow QA/readability closeout pass, not a new mechanics packet.
- Concrete readability/clickability regressions may be fixed if they are directly tied to EPIC-007 commitments.
- Broader design direction remains human-owned after the closeout verdict.

Human-approved exceptions:

- None. Story scope remains a narrow QA/readability closeout pass and does not authorize new mechanics or next-epic implementation.

## Branch / PR requirements

- Branch name: `story/STORY-QA-008-strategic-map-region-playtest-closeout`.
- PR title: `STORY-QA-008 Strategic map region playtest and closeout review`.
- Required linked story ID: `STORY-QA-008`.
- Required evidence summary: inspected flows, tests run, evidence path, CI URL, closeout verdict.
- Required omissions section: explicitly list unresolved readability/playtest issues or state `No known omissions`.

## Story readiness gate

- [x] Story has stable ID, title, type, status, and parent epic.
- [x] User/player/system value is clear.
- [x] Source requirements are linked.
- [x] In-scope work is bounded.
- [x] Out-of-scope work is explicit.
- [x] Dependencies are listed and satisfied.
- [x] Acceptance criteria are observable.
- [x] Verification requirements are defined.
- [x] Branch / PR / CI traceability requirements are stated.
- [x] Ambiguity Check status is PASS.
- [x] Human approval has been given or delegated gate approval is recorded.

## DONE gate

- [ ] Implementation/review matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required evidence exists.
- [ ] Required tests/CI pass or human-approved exceptions are documented.
- [ ] Closeout verdict is recorded.
- [ ] PR/code review is complete.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY for implementation.
