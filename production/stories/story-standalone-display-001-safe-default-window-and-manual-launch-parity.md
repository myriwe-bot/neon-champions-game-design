---
title: STORY-STANDALONE-DISPLAY-001 Safe Default Window and Manual Launch Parity
type: story
status: ready
phase: production
owner: shared
created: 2026-07-20
updated: 2026-07-20
approval: approved
related: [production/epics/epic-018-physical-adventure-map-and-player-entry-recovery, production/stories/story-prototype-continuity-qa-002-recovery-replaytest, production/stories/story-standalone-entry-001-windows-player-entry-and-launch-smoke, docs/architecture/testing-strategy]
---

# STORY-STANDALONE-DISPLAY-001 Safe Default Window and Manual Launch Parity

## Status

READY / approved and pointer-activated on 2026-07-20. The exact safe-default display contract, no-screen-arguments launch proof, override compatibility, scope boundaries, and mandatory post-merge human double-click recheck are approved as written. Unity pointer PR #178 merged as `d36e4d03c47b78b3f25f7c68a9f8dd71b41fe234`; exact-head run `29753475424` and post-merge `main` run `29754166388` passed all four configured jobs.

## Activation evidence

- Design approval authority: `a02d15669b78d3e42f8b4c06860484f996cb9223`.
- Design publish: `29753310136` — passed.
- Unity pointer PR: #178.
- Pointer exact head: `9dce9eedeaa1b1717a8754ac79362739882c5f62`.
- Pointer exact-head CI: `29753475424` — passed.
- Pointer merge / implementation ancestor: `d36e4d03c47b78b3f25f7c68a9f8dd71b41fe234`.
- Pointer post-merge `main` CI: `29754166388` — passed.

## Player problem

On the owner’s high-resolution Windows display, ordinary double-click launch shows the Made with Unity splash and then a black window. The same executable reaches the game when CI-style arguments force a 1920x1080 window. A player build that works only through hidden command-line launch policy is not playable.

Exact complaint authority:

> “For some reason my machine does not open the build. It shows the made with unity splash but after that gives a black screen.”

> “The window properly pops open on the same machine when the tests run.”

## Verified diagnosis boundary

Current Unity `ProjectSettings/ProjectSettings.asset` records:

- `defaultScreenWidth: 1024`
- `defaultScreenHeight: 768`
- `defaultIsNativeResolution: 1`
- `resizableWindow: 0`
- `fullscreenMode: 1`

Current `ci/RunWindowsPlayerLaunchSmoke.ps1` always launches with:

- `-screen-fullscreen 0`
- `-screen-width 1920`
- `-screen-height 1080`

The human diagnostic launch with those same screen arguments succeeds. The supplied player log shows normal engine, D3D12, Mono, PhysX, and Input System initialization without a fatal error. This strongly localizes the defect to default/saved display startup policy or its interaction with a high-resolution desktop. It does not yet prove which individual Unity setting is causal, so implementation must use focused reproduction and tests rather than change unrelated rendering code.

## Player value

A normal Windows player can double-click the executable on a high-resolution display and reach the title at a safe, readable, resizable window size without knowing command-line arguments.

## In scope

- Define explicit safe Windows standalone defaults: initial 1920x1080 windowed mode, native-resolution startup disabled, and resizing enabled.
- Ensure ordinary launch without `-screen-*` arguments reaches the normal title shell.
- Preserve explicit command-line resolution overrides for CI and developer diagnosis.
- Extend built-player launch smoke so at least one fresh launch omits all `-screen-*` arguments and still proves title -> faction choice -> HRC map through production UI.
- Keep the existing independent HRC/QXZ explicit-resolution launches if still needed for interaction parity.
- Add project-settings validation covering the exact approved safe defaults.
- Capture player log, initial window dimensions/mode, source SHA, executable hash, and truthful title evidence for the no-resolution-arguments launch.
- Require a fresh human double-click replay on the owner’s high-resolution machine after merge before resuming the broader continuity route.

## Exact default contract

Unless a focused RED reproduction proves that one of these values is technically invalid in Unity 6000.4.8f1, the implementation target is:

- Windows initial width: 1920.
- Windows initial height: 1080.
- Initial mode: windowed, not exclusive or borderless native fullscreen.
- Native-resolution startup: disabled.
- Resizable window: enabled.
- User/CLI resolution changes after successful startup: preserved; do not force 1920x1080 every frame or overwrite a valid player choice on every launch.

If Unity serialization or platform-specific APIs cannot represent this exact contract, Codex must stop with the focused evidence and propose the narrow equivalent. It may not silently choose another display policy.

## Out of scope

- Strategic/tactical gameplay, map, content, save schema, AI, economy, balance, assets, renderer replacement, render pipeline, shader work, GPU-driver work, or general graphics settings UI.
- Treating `-screen-width 1920 -screen-height 1080` as the player-facing workaround.
- Disabling D3D12 or changing graphics APIs without a separately approved diagnosis.
- Deleting all user preferences indiscriminately.
- Forcing a resolution every frame or preventing later resolution/fullscreen settings work.
- Claiming the full recovery replaytest passes after this repair; only a fresh human replay may do that.

## Acceptance criteria

- [ ] Project settings encode the approved 1920x1080 windowed, non-native, resizable startup contract.
- [ ] An automated validator fails if those startup defaults drift.
- [ ] A freshly built Windows player launched with no `-screen-*` arguments reaches the normal title shell.
- [ ] That no-screen-arguments process then reaches faction choice and HRC strategic map through real production UI input and exits zero.
- [ ] Evidence records observed initial client/window dimensions and mode; a mere state-signal file is insufficient.
- [ ] Existing explicit 1920x1080 HRC and QXZ built-player routes remain green, or equivalent independent faction coverage remains green without weakening real OS-input proof.
- [ ] Command-line screen overrides still work and are not overwritten after startup.
- [ ] Full EditMode, PlayMode, Placeholder Validator, standalone build, exact-head CI, and post-merge CI pass.
- [ ] No gameplay, save, AI, map, content, package, unrelated project setting, graphics API, or prior evidence changes occur.
- [ ] Human owner double-clicks the exact repaired build on the same high-resolution machine and confirms the title appears without launch arguments before the continuity replaytest resumes.

## Evidence package

- `production/evidence/STORY-STANDALONE-DISPLAY-001/README.md`
- no-arguments player log
- no-arguments launch-state record
- initial window/client dimensions and display-mode record
- native title capture from the no-arguments launch
- executable SHA-256 and exact Unity source SHA
- focused and full test results
- exact-head and post-merge CI URLs
- explicit omissions statement

## Ambiguity check

PASS. Human approval is recorded. The observed failure, safe default values, no-arguments production launch proof, command-line override compatibility, scope boundary, and human recheck are explicit. Implementation may choose the narrow Unity API/serialization mechanism needed to encode the approved values, but it may not invent a different display policy or broaden into renderer/GPU work.

## Branch and PR

- Branch: `story/STORY-STANDALONE-DISPLAY-001-safe-default-window`
- PR title: `STORY-STANDALONE-DISPLAY-001 Safe default Windows launch`
- Non-draft PR only after focused GREEN and a remote checkpoint exist.

## Verdict

READY / approved / pointer-activated. Sole current Unity implementation packet. Run from clean Unity `main` at `d36e4d03c47b78b3f25f7c68a9f8dd71b41fe234` using `production/sprints/codex-story-standalone-display-001.prompt.txt`; the full recovery replaytest remains blocked until the repaired build receives human double-click verification.
