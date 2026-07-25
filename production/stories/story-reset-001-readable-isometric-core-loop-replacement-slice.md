---
title: STORY-RESET-001 Readable Isometric Core-Loop Replacement Slice
type: story
status: done
phase: production
owner: shared
created: 2026-07-24
updated: 2026-07-25
approval: approved
related: [production/epics/epic-020-human-rejected-prototype-design-and-isometric-reset, production/playtests/playtest-journal, design/gdd/product-constitution, design/gdd/strategic-map, design/ux/player-shell, docs/architecture/unity-technical-scheme, docs/architecture/testing-strategy, docs/architecture/control-manifest]
---

# STORY-RESET-001 Readable Isometric Core-Loop Replacement Slice

## Status

DONE / merged through Unity PR #190 as `af83b11a8d015647f567b2de014b47c3308643a1` / `BLOCKED — REJECT HUMAN PLAYABILITY CLOSEOUT` on 2026-07-25. The replacement materially improved readability but did not establish meaningful decisions, objective/rival/combat comprehension, or fun. Historical implementation authority only; do not rerun.

## Story type

Visual/Feel + UI + Integration + bounded presentation replacement.

## Parent epic

- `production/epics/epic-020-human-rejected-prototype-design-and-isometric-reset.md`

## Player value

As a new player, I need the game to look and behave like a readable isometric strategy/adventure game so I can understand where I am, open my base, make one building/recruitment choice, move my Champion to a visible destination, and understand why that choice matters without reading design documents or decoding a dashboard.

## Human rejection authority

Source: `production/playtests/playtest-journal.md#[2026-07-24]-post-launch-repair-unaided-owner-playtest`.

Exact acceptance drivers include:

- “The game does not look or feel like anything we have discussed, definitely not like the games that give it inspiration.”
- “Movement is complicated, art is hard to read, bases cant even be opened.”
- “The text and the ‘objectives’ are confusing, not simple in any way.”
- “We need to turn this into a normal isometric-type view game where even if art is preliminary, it is still understandable.”
- “Bases need to be accessible and haver clearly defined buildings.”
- “I do not understand at all what the game loops are supposed to be or where the fun should be.”
- “There are way too many buttons to click and options to choose.”
- “It is not fun AT ALL.”
- “A node and edge graph and very complicated.”

## Binding design contract

### First-session loop

1. Dedicated title.
2. Choose HRC or QXZ from a quiet faction-choice state.
3. Enter a map-dominant shallow-isometric Arctic scene.
4. Open the visible starting base through a normal click.
5. Understand one built income facility, one buildable resource facility, and one buildable recruitment facility.
6. Build or recruit through plain `purpose / cost / result` language.
7. Return to map, select the physical Champion, and click one visible reachable landmark.
8. See a restrained path/cost preview and receive one immediate plain-language consequence.
9. End turn and understand that the rival acts toward the same simple objective.

### Presentation hierarchy at 1920×1080

- Map/world: at least 75% of the strategic frame.
- Persistent top strip: faction, turn, Credits, Materials, objective progress only. Intel remains hidden from first-run HUD.
- Selected-Champion card: compact portrait/silhouette, movement, and two-line army summary.
- Context actions: no more than three visible primary actions for the selected context.
- End Turn: one stable prominent control.
- Feed: collapsed by default; only a short latest-result toast appears after a real action.
- Debug IDs/state: off by default and absent from acceptance captures.

### Dedicated title/faction states

- Title and faction choice must not render the live strategic map or gameplay HUD behind their panels.
- Primary actions are dominant and unambiguous.
- A clear Windowed/Fullscreen control or F11 shortcut must exist; the UI must remain usable after resizing.

### Isometric world

- Use a deliberate shallow-isometric camera and continuous terrain composition.
- Terrain, coast/water, roads/tracks, bases, guarded sites, resources, and the central objective must read through shape and value before labels.
- No permanent node circles, graph lines, route buttons, polygon bands, raw coordinates, or label carpets.
- Current node-route legality may remain as a hidden temporary substrate. It is not final movement authority.
- Reachable paths appear only after Champion selection and must be visually subordinate to terrain/landmarks.

### Bases and buildings

- Both starting bases are large persistent world landmarks and always accept normal pointer selection, whether or not the Champion occupies the base node.
- Base selection opens a dedicated base view/screen rather than adding cards over the strategic dashboard.
- The replacement slice shows only three functional facility roles from existing safe rules:
  1. built income/administration;
  2. buildable Materials/resource support;
  3. buildable recruitment/dwelling.
- Each facility shows: plain functional name, `Built` or `Available`, one-sentence effect, exact cost, prerequisite, and immediate result.
- Current unsupported or owner-rejected normal-play options are hidden: `Stratospheric Lab`, Intel-income facilities, discount suites/garages, advanced Operations/Lead controls, and vague `Starting-hub support` copy.
- Hidden content remains in data/domain for compatibility; this story does not delete save/schema/runtime systems.
- Existing safe recruitment offers may be used, but the UI must say unit name, stack count, stock, and exact cost. `specialists` alone is insufficient.

### Objective and copy

- First objective copy: `Control the Central Relay for 5 turns.` This is a replace-later functional label for the current `site_central_objective` / `holdRequiredCount: 5`, not new canon.
- First-turn guidance is exactly three plain steps: `Open your base`, `Recruit or build`, `Select your Champion and choose a destination`.
- Every result toast uses factual mechanical language. No generated atmospheric prose, `Verify Lead`, unexplained provenance text, or repeated `Action unavailable` feed spam appears in the first-run surface.

## In scope

- New bounded Presentation components/adapters for title, faction choice, isometric map composition, minimal HUD, base view, contextual results, and responsive/fullscreen behavior.
- Refactor `StrategicMapBootstrap` only enough to route normal play through the new boundary and stop building the rejected shell.
- Reuse existing Domain/Application/scenario/save/AI/tactical contracts where legal.
- Presentation aliases and replace-later procedural/primitive art are allowed for functional clarity.
- Focused EditMode and PlayMode tests plus built-player routes for HRC and QXZ.
- Fresh 1920×1080 evidence for title, HRC map, HRC base, Champion/path, and QXZ map/base.

## Out of scope

- Final art, final animation, audio production, final names/canon, campaign writing, balance redesign, new units/facilities/resources, tactical rules redesign, save schema, AI policy, scenario topology/content expansion, map editor, final grid/hex/freeform decision, free movement/pathfinding, and broad renderer/package changes.
- Implementing Intel Leads, Verify Lead, Operations, Feed depth, support discounts, full six-building catalogs, or every existing site interaction on the first-run HUD.
- Calling the whole game redesigned or complete.

## Allowed placeholders

- Deterministic code-built terrain, landmark, road, and building silhouettes marked replace-later.
- Functional labels `Central Relay`, `Administration`, `Resource Support`, and `Recruitment Hall` are replace-later UX labels, not canon.
- Existing faction/unit display names may appear only when resolved from current authored data.
- No fake gameplay results, unlabeled generated assets, or fabricated inventory.

## Architecture constraints

- Presentation does not mutate Domain state directly.
- Existing `StrategicMapInputSession` commands remain the gameplay command path.
- Application remains engine-free.
- New presentation code uses a bounded adapter/view-model boundary; do not add another monolithic block to `StrategicMapBootstrap`.
- Existing legacy shell may remain behind debug/test compatibility if needed, but normal production entry must use the replacement shell.
- Stop and amend if base access requires changing ownership/location rules, or if movement simplification requires a topology/rule rewrite.

## Acceptance criteria

- [ ] Explorer launch reaches a dedicated title with no map/gameplay HUD visible behind it.
- [ ] Title/faction controls remain readable after window resize; F11 or a visible control toggles fullscreen/windowed.
- [ ] HRC and QXZ enter the same map-dominant shallow-isometric presentation with distinct Champion/base silhouettes beyond hue.
- [ ] Normal strategic view contains no permanent node circles, graph-edge buttons, region bands, raw IDs, raw coordinates, or always-open Feed rail.
- [ ] A new player can identify own Champion, own base, rival direction, one reachable destination, and `Control the Central Relay for 5 turns` from the frame.
- [ ] Clicking either physical starting base always opens the dedicated base view, including after the Champion moves away.
- [ ] Base view shows exactly the three approved functional roles and hides the rejected/advanced facility options.
- [ ] Every visible building presents plain purpose, state, cost, prerequisite, and result; no `Starting-hub support` text appears.
- [ ] Recruitment presents actual unit name, count, stock, and costs before apply, then visibly updates the selected Champion army.
- [ ] Returning to the map, selecting the Champion, and clicking a reachable landmark executes through normal Input System/pointer and application command paths.
- [ ] Reachability/path/cost emphasis is contextual and recedes when the Champion is not selected.
- [ ] First-turn guidance has three steps and disappears/progresses truthfully as actions occur.
- [ ] Result feedback is concise and factual; continuous `Action unavailable`, `Verify Lead`, and atmospheric consequence prose are absent from normal first-run play.
- [ ] Current save/resume, AI turn, battle handoff, scenario data, resources, construction rules, and victory progress regressions remain green.
- [ ] Exact-head EditMode, PlayMode, validator, Windows build, and standalone HRC/QXZ routes pass.
- [ ] Fresh native captures are inspected by an independent visual review before merge.
- [ ] Final acceptance remains an unaided owner replaytest; automation cannot mark EPIC-020 complete.

## Verification requirements

- TDD: required for new presentation/view-model behavior where feasible.
- EditMode: adapter projection, hidden-content filter, plain facility/recruitment copy, objective copy, deterministic isometric anchors, responsive layout rules.
- PlayMode: dedicated title isolation; HRC/QXZ entry; real pointer Champion/base/destination paths; base access after movement; build/recruit result; resize/fullscreen; absence of rejected shell elements.
- Regression: full existing EditMode/PlayMode/validator/compile matrix.
- Built player: signal-free title plus independent title -> HRC -> base/map and title -> QXZ -> base/map routes.
- Evidence: fresh isolated 1920×1080 captures and README under `production/evidence/STORY-RESET-001/`.
- Human: no screenshot/video request to the owner during implementation; one fresh self-play build is handed off only after automated and independent gates pass.
- Performance: no per-frame UI/geometry rebuild; stable render/UI counts across repeated refresh.

## Ambiguity Check

Status: PASS for this bounded slice.

Human-approved decisions:

1. Radical reset is required; current build is rejected.
2. Use a normal readable isometric-type view.
3. Preliminary art is acceptable only if understandable.
4. Bases must be accessible with clearly defined buildings.
5. Return to design basics and implement immediately where feasible.
6. The proposed simple explore/build/recruit/move/encounter loop is accepted as the reset hypothesis.

Provisional, not final:

- Hidden graph legality may be reused only to accelerate this slice.
- Final movement topology, final facility names/content, final objective presentation, and final art remain open after replaytest.

Open questions: none that require invention for the bounded replacement slice.

## Branch / PR requirements

- Branch: `story/STORY-RESET-001-readable-isometric-core-loop`
- PR title: `STORY-RESET-001 Readable isometric core-loop replacement`
- Create from exact clean Unity `main` after design authority is published.
- Publish an early draft checkpoint after focused GREEN.
- Final head requires independent spec, architecture/code-quality, visual/UX, and exact-head CI review.
- Human replaytest happens after merge and fresh Windows build; implementation agents do not merge or claim fun acceptance.
- PR must list all hidden/deferred current systems and any legacy compatibility surface retained.

## Story readiness gate

- [x] Human rejection and exact complaints are recorded.
- [x] Product/core-loop reset direction is human-approved.
- [x] Scope is one bounded replacement slice, not a whole-game rewrite.
- [x] Temporary versus final movement/content/art decisions are explicit.
- [x] Architecture, input, tests, evidence, CI, and human gates are explicit.
- [x] Ambiguity Check PASS.
- [x] Immediate implementation approval recorded.

## Verdict

DONE / implemented and human-tested / `BLOCKED — REJECT HUMAN PLAYABILITY CLOSEOUT`. See `production/playtests/playtest-journal.md#[2026-07-25]-story-reset-001-unaided-owner-replaytest`.
