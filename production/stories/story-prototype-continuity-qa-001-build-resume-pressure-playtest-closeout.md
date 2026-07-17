---
title: STORY-PROTOTYPE-CONTINUITY-QA-001 Build Resume Pressure Playtest Closeout
type: story
status: ready-candidate
phase: production
owner: human
created: 2026-07-17
updated: 2026-07-17
approval: pending
related: [production/epics/epic-017-fully-playable-prototype-continuity-and-opponent-pressure, production/stories/story-save-001-prototype-strategic-save-and-resume, production/stories/story-ai-play-001-deterministic-opponent-pressure-after-resume, production/stories/story-proof-qa-001-human-proof-build-playtest-and-capture-gate, docs/architecture/prototype-strategic-save-resume-adr, docs/architecture/testing-strategy]
---

# STORY-PROTOTYPE-CONTINUITY-QA-001 Build Resume Pressure Playtest Closeout

## Status

READY-candidate / approval pending. This is the sole next EPIC-017 packet, but it is not implementation authority. Its guarded prompt must not run and the Unity pointer must remain inactive until human approval.

## Player value

As the owner and first playtester, I need a clean Windows prototype build to prove that a real strategic match can be played, saved, left, continued, and pressured by the opponent without continuity loss or misleading UI.

## Gate model

This is a human-owned closeout gate supported by automation. Automated evidence may prove build health, persistence equivalence, deterministic opponent behavior, and UI hygiene. It may not substitute for the human playing the build and recording an honest verdict.

## In scope

- Produce a clean Windows build from verified Unity `main`.
- Run the existing full Unity CI and focused save/Continue/opponent-pressure regressions.
- Execute one fresh-match route through meaningful strategic actions, save and return to title, Continue, then observe at least one deterministic opponent action after resume.
- Verify the resumed resources, armies, sites, facilities, objective/turn state, Feed consequences, and pending tactical state are plausible and continuous.
- Capture 1920x1080 normal-shell evidence before save, after Continue, and after the opponent action.
- Record build SHA, exact steps, expected/actual results, defects, evidence provenance, and a human verdict.
- If a blocker is found, create a narrow defect packet/PR; do not silently redesign gameplay inside this QA story.

## Out of scope

- New gameplay systems, balance passes, map topology, content expansion, save schema changes, tactical auto-resolution, or sophisticated AI.
- Claiming fun, clarity, or completion from automated tests or video alone.
- Replacing the separately deferred EPIC-016 `STORY-PROOF-QA-001` market/presentation closeout.
- Marking EPIC-017 DONE without explicit human playtest authority.

## Human playtest script

1. Launch the clean Windows build into the normal title shell.
2. Start the authored prototype scenario and complete at least two meaningful human strategic actions.
3. End a turn and observe one opponent action and its visible consequence.
4. Save and Return to Title from a stable strategic boundary.
5. Close/relaunch the build or otherwise prove a real title-level Continue boundary.
6. Continue and verify the recorded strategic state.
7. End/advance into the next opponent turn and verify readable deterministic pressure.
8. If tactical handoff occurs, confirm strategic turn completion pauses and the AI-controlled tactical side can act.
9. Record defects and classify each as blocker, follow-up, or accepted prototype limitation.
10. Give an explicit PASS, PASS WITH FOLLOW-UPS, or BLOCKED verdict.

## Acceptance criteria

- [ ] Build provenance binds the tested Windows executable to a verified `main` commit.
- [ ] Full configured EditMode, PlayMode, validator, and standalone checks pass for that commit.
- [ ] Real Save and Return -> title/relaunch -> Continue preserves the expected strategic state.
- [ ] The first relevant opponent choice after Continue matches the equivalent uninterrupted state or any difference is explained and approved.
- [ ] Opponent pressure is visible in the exact normal Feed and corresponds to an observable state consequence.
- [ ] Tactical handoff, when selected, pauses strategic completion and exposes a legal `CombatAI` step.
- [ ] Three truthful 1920x1080 captures exist with no raw IDs, local paths, debug panels, or hidden fixture assumptions.
- [ ] Human playtest notes record exact steps, defects, and explicit verdict.
- [ ] No blocker remains open; follow-ups are separately owned and do not overstate this gate.
- [ ] Design closeout records cite the tested build commit, evidence, verdict, and CI.

## Evidence package

- `production/evidence/STORY-PROTOTYPE-CONTINUITY-QA-001/README.md`
- `pre-save-1920x1080.png`
- `continued-state-1920x1080.png`
- `post-resume-opponent-pressure-1920x1080.png`
- human playtest report under the design repository's `production/playtests/`

Every image must identify provenance in the README, not in leaked on-screen paths. Any fixture/setup adjustment must be disclosed.

## Ambiguity check

Status: PASS for approval review. The gate, human authority, expected route, evidence, and no-redesign boundary are explicit. Exact build-distribution mechanics may use the existing CI artifact path or a locally built verified executable, but provenance is mandatory.

## Approval questions

1. Approve this exact human-owned QA gate and script?
2. Is a title-level Continue in the same process acceptable, or must the build be fully closed and relaunched? Recommended: full close/relaunch.
3. Is `PASS WITH FOLLOW-UPS` allowed when no continuity/player-blocking defect remains? Recommended: yes.

## Branch / PR requirements after approval

- Branch: `story/STORY-PROTOTYPE-CONTINUITY-QA-001-build-resume-pressure-playtest-closeout`
- PR title: `STORY-PROTOTYPE-CONTINUITY-QA-001 build resume pressure playtest closeout`
- Non-draft PR required for any Unity harness/evidence change.
- Human notes and design closeout remain design-repository authority.

## Verdict

READY-candidate / approval pending. Do not implement or activate the Unity pointer yet.
