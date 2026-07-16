---
title: STORY-PROOF-QA-001 Human Proof-Build Playtest and Capture Gate
type: story
status: ready-candidate
phase: production
owner: human
created: 2026-07-16
updated: 2026-07-16
approval: pending
related: [production/epics/epic-016-accelerated-playable-product-foundation, production/stories/story-proof-scenario-001-month-one-route-pressure-feed-and-capture-flow, production/planning/month-one-proof-scenario-and-capture-plan]
---

# STORY-PROOF-QA-001 Human Proof-Build Playtest and Capture Gate

## Status

READY-candidate / approval pending. Prepared after Unity PR #158 merged. Human decision on 2026-07-16 explicitly deferred this gate; do not schedule the playtest, record video, run Codex, or treat this packet as current work until the human approves it later.

## Purpose and player value

Validate that the merged EPIC-016 proof build works as a comprehensible game for a person rather than only as a green automated route: title entry, faction choice, exploration, base decision, army reading, tactical action, Feed consequence, and real resolution should be understandable without developer intervention.

## Gate protocol

When explicitly approved and scheduled:

1. Start from the normal title/player entry on a clean build of Unity `main`.
2. Choose HRC or QXZ without following an automated step list during play.
3. Play to a real objective victory or defeat using only normal player inputs.
4. Record real start/end timestamps, elapsed time, faction, route deviations, every failed unaided task, and points requiring explanation.
5. Target 20–30 minutes. Do not insert waits or infer human pacing from automated test duration.
6. If separately approved during the same gate, record the 30–60 second capability sequence using `production/evidence/STORY-PROOF-SCENARIO-001/capture-sequence.md`; video remains optional until that approval.

## Acceptance criteria

- [ ] The run starts at normal title entry and reaches a real objective resolution without developer intervention or direct state mutation.
- [ ] The written record contains faction, real start/end timestamps, elapsed time, route deviations, failed unaided tasks, and final result.
- [ ] The player can explain whose turn it is, the objective, resources, construction choice, army composition, legal tactical actions, and the Feed consequence.
- [ ] Any confusion or failure is preserved verbatim and converted into either an accepted limitation or one narrow READY-candidate repair story.
- [ ] If video is explicitly approved, the capture is 30–60 seconds of real gameplay, follows the checked-in sequence, and uses no camera-only mockup or direct runtime setup.

## In scope

- Human playtest protocol and written result.
- Optional later video only after explicit approval.
- Closeout verdict: PASS, ACCEPTED WITH LIMITATIONS, or ONE NARROW FOLLOW-UP.

## Out of scope

- Running now without human approval.
- Codex implementation, feature expansion, balance redesign, final art/audio, campaign work, or broad polish.
- Treating automated routes or inserted waits as human evidence.

## Evidence

When run later, store the written report under `production/evidence/STORY-PROOF-QA-001/`. Add video only if explicitly approved and produced. Link the tested Unity `main` commit and CI run.

## Verdict

READY-candidate / deferred. No current READY Unity implementation packet is created by this story.