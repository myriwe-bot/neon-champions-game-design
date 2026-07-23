---
title: STORY-STANDALONE-LAUNCH-CONTEXT-001 Working-Directory-Independent Windows Launch
type: story
status: ready
phase: production
owner: shared
created: 2026-07-23
updated: 2026-07-23
approval: approved
related: [production/epics/epic-018-physical-adventure-map-and-player-entry-recovery, production/stories/story-standalone-display-001-safe-default-window-and-manual-launch-parity, production/stories/story-prototype-continuity-qa-002-recovery-replaytest, docs/architecture/testing-strategy]
---

# STORY-STANDALONE-LAUNCH-CONTEXT-001 Working-Directory-Independent Windows Launch

## Status

READY / approved on 2026-07-23. This is the sole runnable Unity implementation packet after pointer activation. The owner authorized preparation, activation, implementation through merge, and return only for final exact-machine double-click verification.

## Player blocker

The exact Windows player at Unity `main` `b0ea56ad2998421464baadee3bfbd32a16790ec0`, executable SHA-256 `E83058C236F35A720C27E465DC42D1549F13B25A8573DCE464438B855764E7AF`, still fails ordinary Explorer launch on the owner's 2560x1440 two-monitor machine:

> “Window color: grey originally, black when resized. Window visible. Window resizable.”

The same executable produces opposite outcomes solely from process working directory, with no `-screen-*` arguments:

- working directory `Builds\StandaloneWindows64` (the executable directory, matching normal Explorer context): splash then gray/black;
- working directory repository root: title opens;
- repository-root `-logFile` launch: title opens;
- repository-root `-logFile` plus `-standaloneSmokeSignal`: title opens and reports `Title|faction_1|846|632|0`.

CI currently starts the player without an explicit `-WorkingDirectory`, inheriting the repository-root shell context. It therefore proves the successful control, not normal installed/double-click behavior.

## Player value

A distributed Windows build launches and renders its title from Explorer, its own executable directory, the repository root, or any unrelated working directory. Players never need a source checkout or launch wrapper.

## Approved implementation contract

1. Reproduce RED with the exact built player launched with:
   - no `-screen-*` arguments;
   - `WorkingDirectory` set to the executable directory;
   - normal production title path;
   - proof of actual visible title pixels/window content, not only a state signal.
2. Preserve repository-root launch as the successful diagnostic control.
3. Identify and remove the production dependency on inherited current working directory. Do not merely change CI to a different convenient directory.
4. Prove the same fresh player from three explicit contexts:
   - executable directory;
   - repository root;
   - an unrelated temporary directory outside both repository and build tree.
5. All three routes must reach Title -> FactionChoice -> one playable strategic map through real OS pointer input, with HRC and QXZ coverage retained across the matrix.
6. Preserve the approved 1920x1080 windowed, non-native, resizable startup defaults and explicit command-line resolution overrides.
7. Make CI pass `-WorkingDirectory` explicitly for every built-player launch. No test may accidentally inherit the repository root.
8. Harden harness integrity: `-standaloneSmokeSignal` and faction transport may observe state and coordinates but may not create a different startup, force/rebuild layout earlier than production, repair rendering, or bypass production UI. The current coordinate path calls `Canvas.ForceUpdateCanvases()`; remove it, move any genuinely required layout readiness into the normal production lifecycle, or prove signal/no-signal parity with focused coverage.
9. Add a signal-free visible-title launch route. A state file alone cannot prove rendering.
10. After merge, require the owner to rebuild exact `main` and double-click the executable on the affected machine before continuity playtesting resumes.

## In scope

- Production startup, title canvas/layout lifecycle, resource/path resolution, or other narrow runtime code proven responsible for current-working-directory dependence.
- `ci/RunWindowsPlayerLaunchSmoke.ps1` and narrowly related Windows launch helpers/tests.
- Focused EditMode/PlayMode tests needed to prevent current-directory or smoke-signal coupling.
- Story-owned evidence under `production/evidence/STORY-STANDALONE-LAUNCH-CONTEXT-001/`.
- README current-task/evidence reconciliation.

## Out of scope

- Registry deletion or broad preference reset.
- D3D12, graphics API, renderer, render pipeline, shader, GPU-driver, package, or unrelated ProjectSettings changes.
- Gameplay, strategic map, scenario, save schema, AI, economy, balance, content, or assets.
- Shipping a repository-root launcher, batch file, shortcut, command-line screen arguments, or working-directory wrapper as the player workaround.
- Claiming the broader recovery continuity replaytest has passed.

## Required TDD and evidence sequence

1. Capture focused RED proving executable-directory no-screen launch is blank/gray or otherwise lacks visible title proof while repository-root control renders.
2. Add a deterministic automated regression that fails before the production fix. It must bind process working directory explicitly.
3. Implement the narrow root-cause repair.
4. Run focused GREEN for executable-directory, repository-root, and unrelated-temp working directories.
5. Prove at least one launch without `-standaloneSmokeSignal` has visible nonblank title evidence. Compare signal and signal-free production outcomes.
6. Preserve explicit 1600x900 override behavior and independent faction coverage.
7. Record source SHA, executable SHA-256, exact commands, working directories, process exits, window/client dimensions/mode, state transitions, screenshots or equivalent pixel evidence, and player logs.
8. Publish a remote draft checkpoint after focused GREEN before broad suites.
9. Run full EditMode, PlayMode, Placeholder Validator, Windows standalone build/launch smoke, and exact-head CI because runtime startup and CI launch semantics are high risk.
10. Record omissions truthfully. Human Explorer verification remains pending after merge.

## Acceptance criteria

- [ ] Focused RED reproduces executable-directory failure and repository-root success on the pre-fix player.
- [ ] Runtime root cause is documented; the repair does not depend on repository-root current directory.
- [ ] Executable-directory, repository-root, and unrelated-temp working-directory routes render a nonblank title and reach playable state.
- [ ] At least one signal-free built-player route proves visible title rendering.
- [ ] Smoke signal/faction arguments are behavior-neutral relative to production startup.
- [ ] CI sets every player process working directory explicitly.
- [ ] Real OS pointer input covers title/faction navigation and retains independent HRC/QXZ parity.
- [ ] Safe display defaults and explicit screen overrides remain green.
- [ ] No registry, renderer/GPU/API, gameplay, content, package, or unrelated settings changes occur.
- [ ] Full affected matrix and exact-head CI pass on the reviewed commit.
- [ ] Independent scope/spec and code-quality reviews pass on the final immutable head.
- [ ] Implementation PR merges and exact tree/post-merge verification is recorded.
- [ ] Human owner double-clicks the exact rebuilt merged executable and reports title success or splash-to-gray/black failure.

## Evidence package

- `production/evidence/STORY-STANDALONE-LAUNCH-CONTEXT-001/README.md`
- pre-fix RED logs/captures for executable-directory and repository-root controls;
- post-fix three-working-directory launch records;
- signal-free title capture and signal/no-signal parity record;
- executable SHA-256 and source SHA;
- focused/full test and CI results;
- explicit omissions statement.

## Ambiguity check

PASS. The exact human reproduction, immutable source/build provenance, only changed variable, three-context target matrix, signal-free visual proof, harness-neutrality requirement, scope exclusions, CI policy, merge contract, and final human gate are explicit. Implementers must stop if the root cause requires graphics API, renderer, package, registry, gameplay, or unrelated architecture changes.

## Branch and PR

- Branch: `story/STORY-STANDALONE-LAUNCH-CONTEXT-001-working-directory-independent-launch`
- PR title: `STORY-STANDALONE-LAUNCH-CONTEXT-001 Working-directory-independent Windows launch`
- Non-draft only after focused GREEN, remote checkpoint, complete evidence, and review readiness.

## Approval

Human-approved verbatim on 2026-07-23:

> “Approved: prepare and activate STORY-STANDALONE-LAUNCH-CONTEXT-001 exactly as proposed, fix it through merge, and return to me only for the final double-click verification.”

## Verdict

READY / APPROVED. Implementation may begin only after the Unity README pointer is merged and its required activation verification is recorded.