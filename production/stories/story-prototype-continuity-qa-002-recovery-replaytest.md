---
title: STORY-PROTOTYPE-CONTINUITY-QA-002 Recovery Continuity Replaytest
type: story
status: draft
phase: production
owner: human
created: 2026-07-19
updated: 2026-07-19
approval: pending
related: [production/epics/epic-018-physical-adventure-map-and-player-entry-recovery, production/stories/story-prototype-continuity-qa-001-build-resume-pressure-playtest-closeout, production/stories/story-standalone-entry-001-windows-player-entry-and-launch-smoke, production/stories/story-map-visual-slice-001-physical-arctic-adventure-map-and-shell, production/stories/story-champion-army-interaction-001-discoverable-champion-army-and-selection-continuity, production/stories/story-map-physical-rollout-001-complete-duel-map-and-two-faction-interaction-parity]
---

# STORY-PROTOTYPE-CONTINUITY-QA-002 Recovery Continuity Replaytest

## Status

DRAFT prepared / inactive. This packet may not be called READY, executed as an authoritative playtest, or used to close EPIC-018 until the human owner explicitly approves activation.

## Why this gate exists

The 2026-07-17 continuity playtest closed as `BLOCKED — REJECT CLOSEOUT` because the standalone build stopped at a gray window and the Editor workaround exposed an unreadable, insufficiently interactive graph-like map. EPIC-018 has now completed its four recovery implementation packets:

1. standalone title/faction entry;
2. representative physical map and shell;
3. discoverable Champion army and clean Champion/base context continuity;
4. complete ten-node/twelve-route physical map with HRC/QXZ interaction parity.

Automation proves those repairs exist. It cannot prove that a human can now understand and complete the intended continuity route.

## Candidate build provenance

- Unity repository: `myriwe-bot/neon-champions-unity`.
- Candidate verified `main`: `c038d42d977eef9a9d71ad0b5c83bc4c6ba0016f`.
- Source implementation PR: #176; exact reviewed head `0e478487958c73dcc91c80425ac21b1f7095b9fc`.
- Post-merge Unity Foundation CI: `29699588200`; Compile/Standalone, EditMode, PlayMode, and Placeholder Validator passed.
- This provenance identifies a candidate only. The eventual human report must record the exact executable/archive hash actually tested; do not infer it from this document.

## Human authority

The human owner executes the build and supplies the verdict. Automation may prepare a clean build, checksums, script, and blank report template. Screenshots, video, test logs, or an agent walkthrough do not substitute for the human playtest.

Allowed verdicts:

- `PASS` — the complete route is understandable and no player-blocking or continuity blocker remains.
- `PASS WITH FOLLOW-UPS` — no player-blocking or continuity blocker remains; bounded follow-ups are explicitly recorded.
- `BLOCKED` — execution cannot complete or continuity/readability is not trustworthy.

## Preserved complaint authority

The replaytest must directly re-evaluate, not paraphrase away, the original complaints:

- “There seems to be no interactivity whatsoever.”
- “The readability on the map is horrible.”
- “I have no idea what do do.”
- “The map is very strange and text is unreadable, it is in general a mess.”
- The polygons did not communicate what they represented.
- The base could not be opened or upgraded through the discovered interaction path.
- Champion inventory and units/stacks could not be found.
- `Mobility support` was visible but unexplained.
- The visible node-map basis remained an explicit concern.

## In scope

- Launch a clean Windows build through the normal title shell without Editor intervention.
- Enter both Play HRC and Play QXZ paths and judge complete-map readability and interaction discovery.
- Find each faction’s Champion army and base/facility context through normal controls.
- On one fresh match, complete meaningful movement/site interaction, observe opponent pressure, Save and Return to Title, fully close and relaunch, Continue, and verify continuity.
- If tactical handoff occurs, verify the strategic pause and one legal AI-controlled tactical step.
- Record exact steps, expected/actual behavior, defects, build provenance, and an explicit human verdict.

## Out of scope

- New gameplay, balance, topology, content, save-schema, AI-policy, tactical, economy, art-production, or renderer work.
- Treating prototype limitations as fixed without human observation.
- Deferring a failed step while claiming the overall route passed.
- Activating an implementation packet from this draft. A defect found here requires a separately approved bounded packet.

## Human replaytest script

### A. Standalone and complete-map recovery

1. Verify the executable/archive checksum and record it in the report.
2. Launch the closed Windows executable into the normal title shell.
3. Choose `New Scenario` -> `Play HRC`.
4. Without debug UI or outside instructions, identify the HRC Champion, attached army, base, legal routes/sites, central objective, and available actions.
5. Move/interact through at least two meaningful strategic actions and inspect the resulting Feed/context.
6. Return to title or restart fresh, choose `New Scenario` -> `Play QXZ`, and repeat the Champion/army/base/action-discovery check.
7. Record whether the whole map reads as a physical place rather than a visible node/polygon graph.

### B. Save/relaunch/Continue continuity

1. In one fresh faction route, record cycle/turn, active faction, Champion location/movement/army, resources, controlled or visited sites, base facilities, objective state, Feed, and pending tactical state.
2. End a turn and observe at least one opponent action with a visible consequence.
3. Use Save and Return to Title from a stable strategic boundary.
4. Fully close the executable.
5. Relaunch the same executable and choose Continue.
6. Compare the resumed state with the recorded pre-close state.
7. Advance into the next relevant opponent turn and verify readable post-resume pressure.
8. If tactical handoff occurs, confirm strategic completion pauses and a legal `CombatAI` step is available.
9. Classify every defect as blocker, follow-up, or accepted prototype limitation.
10. Give an explicit `PASS`, `PASS WITH FOLLOW-UPS`, or `BLOCKED` verdict.

## Acceptance criteria

- [ ] Human activation approval is recorded before execution.
- [ ] Tested executable/archive checksum and exact Unity `main` commit are recorded.
- [ ] The standalone title -> HRC and title -> QXZ paths work without Editor intervention.
- [ ] The human can identify both Champions, attached armies, both bases/facility contexts, legal map interaction, and the central objective without debug UI.
- [ ] The complete map is judged against every preserved readability/interactivity complaint.
- [ ] At least two meaningful human strategic actions and one visible opponent consequence are completed.
- [ ] Save and Return -> full process close -> relaunch -> Continue preserves the recorded strategic state.
- [ ] Post-resume opponent pressure is visible and corresponds to an observable consequence.
- [ ] Tactical handoff, if reached, pauses strategic completion and exposes a legal AI-controlled step.
- [ ] Human notes record exact steps, expected/actual results, defects, and explicit verdict.
- [ ] No blocker is silently deferred or converted into `PASS WITH FOLLOW-UPS`.
- [ ] Closeout cites build checksum, Unity commit, CI, report, evidence, and verdict.

## Evidence package

Prepare only after activation:

- `production/evidence/STORY-PROTOTYPE-CONTINUITY-QA-002/README.md`
- `hrc-complete-map-and-army-1920x1080.png`
- `qxz-complete-map-and-base-1920x1080.png`
- `pre-save-1920x1080.png`
- `continued-state-1920x1080.png`
- `post-resume-opponent-pressure-1920x1080.png`
- human report: `production/playtests/story-prototype-continuity-qa-002-recovery-replaytest.md`

Images support the human notes; they do not replace them. Every artifact must record provenance and remain free of raw IDs, local paths, debug panels, or undisclosed setup.

## Activation gate

Before changing `status: draft` or `approval: pending`, ask the human owner to approve:

1. this exact script and verdict model;
2. the candidate build or a newer explicitly identified verified Unity `main`;
3. both-faction discovery plus one full save/relaunch/Continue route;
4. the rule that any unexecuted required step blocks closeout unless authority is explicitly amended before the verdict.

## Verdict

DRAFT prepared / inactive. No human replaytest result is claimed, no implementation work is activated, and EPIC-018 remains active pending explicit human approval and execution.