---
title: STORY-STANDALONE-ENTRY-001 Windows Player Entry and Launch Smoke
type: story
status: done
phase: production
owner: shared
created: 2026-07-17
updated: 2026-07-17
approval: approved
related: [production/epics/epic-018-physical-adventure-map-and-player-entry-recovery, production/stories/story-prototype-continuity-qa-001-build-resume-pressure-playtest-closeout, docs/architecture/unity-technical-scheme, docs/architecture/testing-strategy, docs/architecture/ci-build-automation, docs/architecture/control-manifest]
---

# STORY-STANDALONE-ENTRY-001 Windows Player Entry and Launch Smoke

## Status

DONE / merged and post-merge verified on 2026-07-17. Historical packet; do not rerun.

## Story type

Integration / Test / narrow bug fix.

## Parent epic

- `production/epics/epic-018-physical-adventure-map-and-player-entry-recovery.md`

## User/player/system value

As a player, I need the Windows executable to reach the real title, scenario choice, and strategic map without Unity Editor intervention, so that the prototype can be tested as a game rather than as a manually assembled scene.

## Observed blocker

Human playtest on 2026-07-17:

- "The build did not launch successfully. After the Unity splashscreen, a gray window appeared and nothing further happened."
- The Editor path worked only after manually adding `Strategic Map Bootstrap` and pressing Play.

Repository preflight found that `ProjectSettings/EditorBuildSettings.asset` enables only `Assets/NeonChampions/Scenes/Foundation.unity`, which has no playable bootstrap, while `Assets/NeonChampions/Scenes/StrategicMap.unity` contains `Strategic Map Bootstrap` and is excluded from build settings. Codex must verify this on current `main` rather than assuming the diagnosis is complete.

## Source-authority matrix

| Path | Status / approval | Purpose | Disposition |
|---|---|---|---|
| `production/stories/story-standalone-entry-001-windows-player-entry-and-launch-smoke.md` | done / approved | exact implementation contract | historical authority |
| `production/epics/epic-018-physical-adventure-map-and-player-entry-recovery.md` | active / approved | sequence and scope boundary | required authority |
| `production/stories/story-prototype-continuity-qa-001-build-resume-pressure-playtest-closeout.md` | done / approved | human failure evidence | required context; no old implementation authority |
| `docs/architecture/unity-technical-scheme.md` | approved / approved | scene/presentation/application boundaries | required authority |
| `docs/architecture/testing-strategy.md` | approved / approved | PlayMode, smoke, TDD, evidence | required authority |
| `docs/architecture/ci-build-automation.md` | approved / approved | build and CI gate | required authority |
| `docs/architecture/control-manifest.md` | approved / approved | agent/project controls | required authority |
| `design/research/physical-adventure-map-direction-2026-07-17.md` | approved / approved | next visual direction | non-authoritative for this fix; map work excluded |

## In scope

- Reproduce and diagnose the current standalone entry failure on current Unity `main`.
- Correct the smallest reliable scene/build/startup configuration so a clean Windows build reaches the existing normal title shell.
- Preserve current title -> New Scenario -> Play HRC/QXZ -> strategic-map behavior.
- Remove the requirement to drag/add `Strategic Map Bootstrap` manually in the Editor.
- Add automated coverage that fails when the configured player entry lacks a playable bootstrap/load path.
- Add an actual built-player launch smoke that starts the Windows executable, proves the title/player shell appears through a production-visible signal or truthful capture, and exits cleanly.
- Record exact build commit, commands, logs, screenshots, process result, and any limitations under `production/evidence/STORY-STANDALONE-ENTRY-001/`.

The implementation may either make the existing playable scene the correct first player scene or make `Foundation.unity` an explicit minimal loader, choosing the smallest solution that preserves existing architecture. It must not introduce a general scene framework.

## Out of scope

- Strategic-map visual redesign, polygon/node removal, text/layout fixes, Champion army UI, base interaction redesign, onboarding, balance, content, AI, save schema, tactical combat, or topology changes.
- Claiming the rejected continuity playtest now passes.
- Fixing the gray window by adding a debug-only bootstrap, test fixture, direct state mutation, or Editor-only setup.
- New packages, render pipeline changes, broad scene architecture, or final loading-screen design.

## Allowed stubs, mocks, placeholders, or temporary data

- Existing title/scenario/map placeholder presentation may remain unchanged in this narrow story.
- Test-only observation hooks are allowed only if they observe the same production entry path and do not become required runtime setup.
- No fake player screenshot or reconstructed UI is allowed.

## Dependencies

- Unity `main` must contain merged `STORY-AI-PLAY-001` and the current pointer activation commit.
- Existing Windows standalone build command must remain available.
- Human map/playability blockers remain owned by later EPIC-018 packets.

## Acceptance criteria

- [x] Given a clean checkout at the story head, the configured Windows build succeeds.
- [x] Launching the built executable without Unity Editor intervention reaches the existing normal title shell rather than a gray/empty window.
- [x] From that same executable, `New Scenario` -> `Play HRC` reaches the current strategic map.
- [x] Repeating the launch from a closed process produces the same playable entry.
- [x] No manual scene object insertion, Inspector wiring, debug toggle, test fixture, or direct state mutation is required.
- [x] An automated check fails if the enabled first-player scene has neither the playable bootstrap nor an explicit valid loader path.
- [x] A built-player smoke records process launch, observed title/player entry, clean exit/termination, logs, and exact executable/build SHA.
- [x] Existing configured EditMode, PlayMode, validator, and standalone checks remain green.
- [x] The diff contains no strategic-map redesign or unrelated gameplay/content changes.

## Verification requirements

- TDD: required. Capture the failing entry/configuration test before the fix and its passing result after.
- EditMode: configuration/scene-entry validation where practical.
- PlayMode: production scene/player-shell boot path.
- Standalone: actual Windows executable launch smoke, not only build-file existence.
- Manual: launch the exact built executable twice; record title and HRC strategic-map captures at 1920x1080 if the environment supports truthful capture.
- Evidence: `production/evidence/STORY-STANDALONE-ENTRY-001/README.md`, logs, and captures.
- Performance: N/A beyond avoiding a hang or indefinite gray window; no new loading/performance system is authorized.
- CI: all configured exact-head checks must pass before merge.

## Ambiguity Check

Status: PASS.

- The player-visible expected path is exact.
- The likely build-settings cause is evidence, not a mandated patch; Codex must reproduce and choose only the smallest architecture-preserving correction.
- The human-approved physical-map direction is explicitly excluded from this first repair.
- Human-approved exception: none.

## Branch / PR requirements

- Branch: `story/STORY-STANDALONE-ENTRY-001-windows-player-entry-launch-smoke`
- PR title: `STORY-STANDALONE-ENTRY-001 Windows player entry and launch smoke`
- Non-draft PR required.
- PR must link this story and list the reproduced cause, exact fix, RED/GREEN evidence, built-player smoke, CI URLs, changed files, and all omissions/deferred work.
- Codex must commit and push the actual branch, create or update the PR, and print local/remote SHA and PR URL.

## Story readiness gate

- [x] Stable story ID, title, type, owner, parent, status, and approval.
- [x] Exact approved source matrix.
- [x] Concrete in-scope and explicit out-of-scope work.
- [x] Observable acceptance criteria.
- [x] Correct evidence layers and TDD requirement.
- [x] Branch/PR/CI contract.
- [x] Ambiguity Check PASS.
- [x] Human approval recorded.

## Activation evidence

- Design approval/control commit: `2cfd08c80e11e90923489d069348df81bf844bcf`.
- Design publish CI: <https://github.com/myriwe-bot/neon-champions-game-design/actions/runs/29588556157> — passed.
- Unity pointer PR: <https://github.com/myriwe-bot/neon-champions-unity/pull/168>.
- Pointer exact head: `9bf14d0aa063f35d678df04c07289853fed51f03`.
- Pointer exact-head CI: <https://github.com/myriwe-bot/neon-champions-unity/actions/runs/29588736112> — Compile/Standalone, EditMode, PlayMode, and Placeholder Validator passed.
- Pointer merge commit: `ce5465476b9d06839f9fd4d11684e2e3e31f66e8`.
- Post-merge Unity `main` CI: <https://github.com/myriwe-bot/neon-champions-unity/actions/runs/29589301841> — all four configured jobs passed.

## Implementation and closeout evidence

- Unity implementation PR: <https://github.com/myriwe-bot/neon-champions-unity/pull/170>.
- Final exact head: `7b753ec462096769e1898d78e5d907361001095b`.
- Exact-head push CI: <https://github.com/myriwe-bot/neon-champions-unity/actions/runs/29608756396> — Compile/Standalone plus state-bound built-player launch, EditMode, PlayMode, and Placeholder Validator passed.
- Exact-head PR CI: <https://github.com/myriwe-bot/neon-champions-unity/actions/runs/29608759836> — the same four jobs passed.
- Merge commit: `439e8fe05f4a65ce33d512e78bceb86eaa550b2f`.
- Post-merge Unity `main` CI: <https://github.com/myriwe-bot/neon-champions-unity/actions/runs/29609782110> — all four jobs passed, including built-player `Title|faction_1` -> `FactionChoice|faction_1` -> `StrategicMap|faction_1` and exit-code-zero enforcement.
- Checked-in evidence: `production/evidence/STORY-STANDALONE-ENTRY-001/` in the Unity repository.
- Review fixes closed before merge: nonzero exits now fail; fixed clicks cannot pass without actual stage/faction observations; exact-head CI runs the built player; evidence whitespace passes the full PR-range check; the implementation SHA and build-size quote match the reviewable commit/log.
- This closes only player entry. It does not claim that the rejected continuity playtest, physical-map readability, Champion/army discovery, or base interaction now passes.

## Verdict

DONE / merged and post-merge verified. `production/sprints/codex-story-standalone-entry-001.prompt.txt` is historical and must not be rerun.
