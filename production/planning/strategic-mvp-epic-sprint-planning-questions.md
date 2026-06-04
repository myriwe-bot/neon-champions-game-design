---
title: Strategic MVP Epic/Sprint Planning Questions
type: planning
status: draft
phase: production
owner: shared
created: 2026-06-04
updated: 2026-06-04
source_lore: []
related:
  [
    design/gdd/strategic-map,
    production/epics/epic-strat-mvp-001-strategic-mvp-core-loop,
    production/stories/story-strat-004-site-interaction-and-guarded-battle-trigger,
    production/stories/story-strat-005-strategic-battle-result-application,
  ]
approval: pending
---

# Strategic MVP Epic/Sprint Planning Questions

## Current read

`EPIC-STRAT-MVP-001` has already delivered the foundation slice:

- scenario/map graph state;
- hotseat turns;
- Champion route movement;
- minimal strategic presentation/input/HUD;
- two-faction hotseat smoke;
- two QA/readability passes;
- battle setup/result DTO boundary.

The remaining approved placeholders in this epic are now drafted as:

1. `STORY-STRAT-004` — site interaction and guarded battle trigger.
2. `STORY-STRAT-005` — strategic battle result application.

Those two stories likely finish the current epic only if we define the epic goal as:

> Prove the strategic layer can move from map interaction to battle handoff to strategic consequence with deterministic domain tests.

They do not finish the broader playable MVP. The broader MVP still needs some combination of tactical battle execution/stub strategy, rewards/economy visibility, recruitment/reinforcement, central objective victory, and a more complete playtest loop.

## Proposed epic sizing rule

Use epics as capability slices that end in a demonstrable player/system behavior, not as huge feature categories.

Recommended size:

- 4-8 implementation stories plus optional QA/story-hardening stories.
- 1 clear playable or testable milestone.
- 1-3 weeks of agent execution at current cadence, depending on CI/review friction.
- Ends with a mergeable demo/checklist, not just architecture.

If an epic needs more than ~8 implementation stories, split it. If it cannot be demonstrated, it is probably a planning theme, not an epic.

## Candidate next epic shapes

### Option A — Finish Strategic Battle Consequence Loop

Goal: a guarded site can be selected, battle handoff generated, battle result applied, and visible strategic consequences appear.

Likely stories:

- STORY-STRAT-004 site interaction and guarded battle trigger.
- STORY-STRAT-005 strategic battle result application.
- STORY-LOOP-002 guarded-site loop smoke / evidence pass.
- STORY-QA-003 readability/feedback for battle handoff and result summary.

Best if the next milestone is: "the strategic map finally has consequence."

### Option B — Minimal Tactical Battle Execution

Goal: replace DTO-only handoff with the smallest tactical encounter that can produce a real `BattleResult`.

Likely stories:

- tactical encounter scene/minimal board setup;
- unit stack placement from `BattleSetup`;
- minimal combat resolver/AI or deterministic smoke battle;
- return `BattleResult` to strategy.

Best if the next milestone is: "I can enter a real fight, even if ugly."

### Option C — Strategic Economy + Recruitment Loop

Goal: make sites matter before/after battle through Credits/Materials/Intel and reinforcement choices.

Likely stories:

- resource stockpile visibility and deltas;
- one-time and/or recurring site rewards;
- recruitment/reinforcement offer contract;
- minimal reinforcement interaction smoke.

Best if the next milestone is: "the map has reasons to race and contest."

### Option D — Scenario Objective/Victory Loop

Goal: make the two-faction scenario end cleanly through central objective or Champion defeat.

Likely stories:

- central objective control/progress;
- Champion defeat scenario loss;
- victory HUD/summary;
- playtest checklist.

Best if the next milestone is: "a small match can be won or lost."

## Planning questions for human decision

1. What should the next sprint prove to you as a player/designer?
   - A: strategic battle consequence works;
   - B: a tiny tactical battle exists;
   - C: economy/recruitment makes map choices meaningful;
   - D: match victory/loss works;
   - or another goal.

2. Should `EPIC-STRAT-MVP-001` close after STORY-STRAT-004/005 plus a smoke/QA pass, or should it remain open until a full map-to-battle-to-result playable loop exists?

3. For guarded neutral sites, what feels better for first MVP?
   - Win battle = site immediately controlled and reward granted.
   - Win battle = guards cleared, then player must claim/collect separately.
   - Hybrid: immediate for simple resource sites, separate interaction for central/recruitment sites.

4. Should the next sprint stay domain/test-heavy, or should it include a visible Unity scene/UI path even if rough?

5. How large do you want sprints to be in practice?
   - 1 story + review/merge;
   - 2-3 tightly related stories;
   - a small vertical slice ending in one demo/QA packet.

6. What is your preferred epic promise format?
   - Player-facing promise: "A player can do X."
   - System-facing promise: "The architecture supports X safely."
   - Playtest-facing promise: "We can test whether X is fun."

7. What is the next meaningful demo you want to see before we build more infrastructure?

## Default recommendation if no other preference

Close `EPIC-STRAT-MVP-001` after:

1. STORY-STRAT-004;
2. STORY-STRAT-005;
3. STORY-LOOP-002 guarded-site consequence smoke;
4. STORY-QA-003 handoff/result readability pass if the smoke is hard to read.

Then open the next epic as either:

- `EPIC-TAC-MVP-001 Minimal Tactical Battle Execution`, if you want real battles next; or
- `EPIC-ECON-MVP-001 Strategic Rewards and Reinforcement`, if you want map incentives next.
