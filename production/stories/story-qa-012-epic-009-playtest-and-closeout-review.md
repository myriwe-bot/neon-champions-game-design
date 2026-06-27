---
title: STORY-QA-012 EPIC-009 Playtest and Closeout Review
type: story
status: ready
phase: production
owner: shared
created: 2026-06-27
updated: 2026-06-27
source_lore: [greenland, white-sky, digital-net]
related:
  [
    production/epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction,
    production/stories/story-map-real-001-scenario-authored-strategic-map-shell,
    production/stories/story-base-001-base-definition-and-facility-construction-core,
    production/stories/story-base-002-administration-income-chain-and-recruitment-dwellings,
    production/stories/story-map-site-001-site-route-base-and-objective-readability-pass,
    production/stories/story-base-loop-001-base-building-scenario-smoke,
    design/gdd/strategic-map,
    docs/architecture/testing-strategy,
    docs/architecture/ci-build-automation,
  ]
approval: approved
---

# STORY-QA-012 EPIC-009 Playtest and Closeout Review

## Status

READY / approved. Human approved on 2026-06-27 with: `Approved`. This story is authorized as the next EPIC-009 closeout/playtest implementation packet. Approved scope: QA/playability closeout over the merged EPIC-009 strategic-map/base-building surface, with only narrow readability/clickability/evidence fixes allowed if concrete blockers are found.

## Story type

QA / Playability Review + Narrow Fix Pass.

## Parent epic

- [EPIC-VSLICE-MVP-009 Strategic Map Geography, Bases, and Facility Construction](../epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction.md)

## User/player/system value

As project director, I need the now-merged scenario-authored strategic map, bases, facility construction, income/recruitment effects, readability pass, and connected base-building smoke reviewed as one playable surface before EPIC-009 is closed or a new mechanics train starts.

## Source requirements

- Parent epic:
  - `production/epics/epic-vslice-mvp-009-strategic-map-geography-bases-and-facility-construction.md`.
- Merged story evidence:
  - Unity `production/evidence/STORY-MAP-REAL-001/`.
  - Unity `production/evidence/STORY-BASE-001/`.
  - Unity `production/evidence/STORY-BASE-002/`.
  - Unity `production/evidence/STORY-MAP-SITE-001/`.
  - Unity `production/evidence/STORY-BASE-LOOP-001/`.
- GDD/control:
  - `design/gdd/strategic-map.md` §§1-16.
  - `docs/architecture/control-manifest.md`.
  - `docs/architecture/testing-strategy.md`.
  - `docs/architecture/ci-build-automation.md`.

## In scope

If approved, this story may:

- Replay or run the current Unity `main` strategic-map prototype at 1280x720.
- Inspect the complete EPIC-009 surface together:
  - scenario-authored map labels/regions/sites/routes;
  - owned bases and selected-base panel;
  - facility build preview/result;
  - income/recruitment refresh after turn advance;
  - Champion movement to a meaningful site;
  - guarded interaction / tactical handoff and return summary;
  - objective holder/progress/status after the loop.
- Fix only concrete player-facing readability/clickability regressions found during the review, such as unreadable overlapping labels, misleading base/facility/recruitment feedback, unreachable controls, missing objective return state, or screenshot/evidence gaps directly tied to EPIC-009 commitments.
- Add or update PlayMode smoke tests and PNG evidence under `production/evidence/STORY-QA-012/` if a fix is made or if the closeout review needs new evidence.
- Produce a concise closeout verdict recommending one of:
  - `CLOSE EPIC-009`;
  - `ONE NARROW FOLLOW-UP`;
  - `REJECT CLOSEOUT / NEEDS HUMAN PLAYTEST`.

## Out of scope

Not authorized by this story:

- No new strategic mechanics, facility tiers, costs, resources, factions, units, routes, sites, objectives, victory rules, base capture/siege/garrisons, marketplace, supply, fog, strategic AI, editor UI, or final art/audio/VFX/localization.
- No tactical combat rule changes.
- No full town tree, upgraded dwellings, multi-base economy expansion, or map-editor implementation.
- No next-epic implementation story promotion without separate human approval.
- No broad UI redesign beyond concrete closeout blockers.

## Allowed placeholders

- Existing prototype labels, simple markers, placeholder IDs, and screenshot style may remain if they are readable enough to support closeout judgment.
- Evidence-only labels/captures are allowed if they do not become new design authority.

## Acceptance criteria

- [ ] The merged EPIC-009 loop can be reviewed on current Unity `main` at 1280x720.
- [ ] The review explicitly addresses map/site/base/route readability, base facility construction, income/recruitment refresh, movement/site interaction or battle, and objective pressure.
- [ ] Any concrete in-scope closeout blocker discovered is fixed narrowly and covered by PlayMode/regression evidence.
- [ ] Evidence under `production/evidence/STORY-QA-012/` documents the final inspected/fixed surface, or the story records why existing evidence was sufficient.
- [ ] Unity Foundation CI passes at exact PR head before merge if any Unity branch is created.
- [ ] Closeout verdict states whether EPIC-009 can close, needs one narrow follow-up, or should pause for human playtest.

## Verification requirements

- Placeholder validator remains green.
- EditMode tests pass if any application/domain projection changes are made.
- PlayMode tests pass if any Unity code/UI/evidence changes are made.
- Standalone Windows64 build passes if a Unity PR is opened.
- Exact-head Unity Foundation CI passes before merge if implemented as a Unity branch.
- If no code changes are made, closeout documentation must still record what was inspected and why no fix was needed.

## Ambiguity Check

Status: PASS. Human approval recorded 2026-06-27.

Human-approved answers:

1. Run this QA/playtest closeout packet as the next step.
2. Allow only narrow readability/clickability/evidence fixes directly tied to EPIC-009 commitments.
3. Record a closeout verdict; do not close EPIC-009 or start a next-epic implementation story without separate human direction.

## Branch / PR requirements

- Branch name: `story/STORY-QA-012-epic-009-playtest-closeout-review`.
- PR title: `STORY-QA-012 EPIC-009 playtest and closeout review`.
- Required linked story ID: `STORY-QA-012`.
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
- [x] Human approval has been recorded.

## DONE gate

- [ ] Review/implementation matches approved story scope.
- [ ] Acceptance criteria pass.
- [ ] Required evidence exists or sufficient inherited evidence is documented.
- [ ] Required tests/CI pass or human-approved exceptions are documented.
- [ ] Closeout verdict is recorded.
- [ ] PR/code review is complete if a Unity branch is opened.
- [ ] Required docs were updated in the correct source-of-truth layer.

## Verdict

READY / approved for implementation. Use `production/sprints/codex-story-qa-012.prompt.txt`; branch `story/STORY-QA-012-epic-009-playtest-closeout-review`; PR title `STORY-QA-012 EPIC-009 playtest and closeout review`.
