---
title: Core Fun Prototype — Contested Infrastructure Crisis
type: prototype-design
status: approved
phase: concept-validation
owner: shared
created: 2026-07-25
updated: 2026-07-25
approval: approved-by-human
related:
  - design/gdd/game-concept
  - design/gdd/game-pillars
  - design/gdd/strategic-map
  - design/gdd/intel-resource
  - production/playtests/playtest-journal
---

# Core Fun Prototype — Contested Infrastructure Crisis

## Approval Boundary

Approved on 2026-07-25: test a compact HoMM-like adventure-strategy loop in one tightly authored crisis scenario before expanding the current prototype.

This approves the **fun hypothesis and experiment**, not final map topology, final crisis fiction, permanent system architecture, final art, balance values, production implementation stories, or unreviewed player-facing terminology.

The 2026-07-26 owner replaytest specifically rejected `No reinforcements`, `No verified public account`, `stack capacity`, and the surrounding opening-choice presentation as confusing and not approved design language. The numerical implementation remains a bounded prototype fact while `STORY-CORE-FUN-002` repairs readability; these rejected phrases are not canon or reusable UX authority.

## Product Spine

A compact HoMM-like adventure strategy game where evidence, witnesses, and public belief form a second contested terrain.

Prototype form: one telegraphed approximately 20-minute infrastructure crisis. Preserve Heroes-style consequential journeys, compounding gains, Champion continuity, army preservation, town anticipation, and opponent-driven tempo. Do not copy its feature catalogue or dated friction.

## Core Sequence

**Claim → Investigate → Commit → Contest → Prove**

1. **Claim:** identify a contested infrastructure crisis or opportunity.
2. **Investigate:** learn relevant threats, stakeholders, rival intent, uncertainty, and possible collateral consequences.
3. **Commit:** sacrifice movement, preparedness, force, or time by choosing one response rather than taking everything.
4. **Contest:** resolve a concrete struggle over access, control, safety, or operation.
5. **Prove:** establish an attributable account that changes local authority or access.

Evidence/Proof must change material play—for example route access, local cooperation, recruitment, operating permission, guard posture, or restoration cost. It must not be only a score or ending paragraph.

## Intel Boundary

Intel is **not** the currency for Investigate or Prove.

Intel is the scarce Alchemical Dust-style progression resource used to:

- upgrade artifact-equivalent Champion Assets;
- unlock highest-tier units; or
- unlock/build the facilities that produce those units.

Investigation uses readable uncertainty, source information, actions, access, and Evidence/Proof state. Routine scouting, proof, Signal actions, legitimacy, and ordinary abilities do not spend Intel.

A crisis may reward rare Intel, but that reward feeds the slower apex-progression layer rather than purchasing the crisis decision itself.

## Selected Crisis

### Multi-Service Relay Failure and Disputed Sabotage

Selected on 2026-07-25 under delegated best-judgment authority after the owner approved the experiment but did not select among the crisis options. This is the prototype premise, not permanent world canon.

A central emergency relay serving navigation beacons, emergency communications, local clinic/port coordination, and White Sky telemetry is failing during Blue Monday. The player and rival both have plausible reasons to secure it, but physical possession alone does not establish safe operation or accepted authority.

The experiment must make three layers distinct:

1. **Physical control:** who can enter, secure, and defend the relay.
2. **Operational restoration:** which essential services are restored, how safely, and at what opportunity cost.
3. **Accepted account:** what caused the failure, what each side did, and which operator relevant local stakeholders will recognize.

The authored truth may involve sabotage, negligent maintenance, a cascading technical fault, or mixed responsibility. The player must receive source-tagged evidence sufficient to reason; ambiguity must not conceal basic rules.

This crisis is preferred because it reuses the current central-objective concept, makes rival intent legible, supports several approaches and immediate map consequences, and tests control/restoration/proof without requiring Echo ontology or a large civilian simulation.

Intel remains separate. Recovering a rare technical archive may award Intel as an apex-progression reward, but Intel is neither evidence of responsibility nor the price of investigation or public acceptance.

## Smallest Coherent Experiment

Include only:

- one small, spatially readable map;
- one infrastructure crisis;
- one player Champion and one visible rival;
- clear rival intent;
- three mutually exclusive response postures represented as scenario choices rather than final universal systems;
- two or three approaches with different time, danger, and information;
- one compact confrontation resolution;
- physical control, operational restoration, and local acceptance;
- immediate, attributable map consequences.

The first implementation used these exact mutually exclusive numerical scenario effects. The 2026-07-26 owner replaytest rejected the original labels/sacrifice copy; preserve the numbers for the bounded repair but do not preserve the rejected language:

### Mobility — `ARRIVE FIRST`

- On selection, the active faction's starting Champion gains `+2` maximum movement and `+2` current movement.
- The increase persists for the scenario and refreshes through the existing turn system as an `8`-point maximum.
- No unit or accepted-account benefit is granted.
- Player-facing sacrifice: `No reinforcements. No verified public account.`

### Force — `ARRIVE READY`

- On selection, the first stack in the active faction's starting Champion army gains `+4` current count and `+4` maximum count.
- Exact live-fixture results are HRC `5/5 -> 9/9` and QXZ `7/7 -> 11/11`.
- No movement or accepted-account benefit is granted.
- Player-facing sacrifice: `No mobility boost. No verified public account.`

### Verification — `VERIFY THE FAILURE`

- On selection, the faction gains a scenario-specific verified public account. This is Evidence/Proof state, never Intel.
- If that faction controls the Central Relay, its required own-turn hold checks are `3` rather than `5`.
- If control changes to a faction without Verification, the requirement returns to `5` and hold progress resets through existing contest rules.
- The rival direction text also identifies the rival's committed objective as the Central Relay.
- No movement or unit benefit is granted.
- Player-facing sacrifice: `No mobility boost. No reinforcements.`

Before normal map, base, or End Turn input, the local human chooses exactly one posture. Selection is free, immediate, saved, and irreversible. Re-selection fails without mutation. Mobility fails closed without an active Champion; Force fails closed without a valid army stack; Verification never spends or creates Intel. Save/resume preserves the selection and never reapplies its numerical grant. Legacy saves without a posture reopen the choice and preserve their existing state until selection.

These are functional experiment contracts, not approved building names, Assets, Operations, permanent base modules, or a generalized posture architecture.

## Explicitly Deferred

- final graph-versus-grid architecture;
- final isometric art;
- complete base-building system;
- faction-specific full rosters;
- general Minor/Major Command architecture;
- Champion progression trees;
- procedural exploration;
- global legitimacy simulation;
- broad misinformation simulation;
- multiple crisis types;
- campaign progression.

Existing tactical combat remains part of the intended game, but the first experiment may use the cheapest honest confrontation resolution needed to isolate the strategic fun hypothesis. Re-expanding tactical content must not obscure whether the crisis decisions work.

## Map-Substrate Experiment

Do not assume that either a graph or a square grid creates exploration.

After the decision loop works in the cheapest readable representation, compare:

- a regional graph with loops, alternate approaches, guarded shortcuts, interception, and route-specific consequences;
- hidden square-cell movement with terrain costs, sight, guard zones, and off-route spatial agency.

The repaired graph carries the burden of proof because the current sparse spoke/corridor map was human-rejected. Choose the simpler substrate only if unaided players experience consequential spatial agency rather than movement between points.

## Time-Scale Acceptance

### First 30 seconds

- Player identifies the crisis.
- Player sees the rival or a clear, attributable rival intent.
- Player notices at least two tempting responses.
- Player understands that all responses cannot be taken.

### First 5 minutes

- Player commits to a posture and approach.
- Player can explain what was sacrificed.
- Investigation reveals actionable information rather than required tutorial facts or lore text.
- Rival behavior can change the player's plan.

### By approximately 20 minutes

- The crisis reaches a concrete outcome.
- Player understands why control was or was not locally accepted.
- Earlier preparation visibly changes the resolution.
- An alternative posture plausibly supports a meaningfully different replay.
- Player can recount intention, discovery, adaptation, and consequence.

## Kill Criteria

Reject or redesign the hypothesis if:

- one opening is consistently dominant;
- investigation merely reveals basic rules required to act;
- Evidence/Proof changes only a meter or ending paragraph;
- the rival follows a track without provoking adaptation;
- physical control always dominates restoration or acceptance;
- players cannot attribute outcomes to earlier choices;
- players describe the scenario as moving to points and filling bars;
- alternate postures produce substantially the same journey;
- the scenario requires progression systems or tactical spectacle before the strategic decision becomes interesting.

## Open Design Packets

1. Define the three response postures as exact scenario contracts.
2. Define three rival intentions and how they are communicated.
3. Define physical control, operational restoration, and local acceptance as implementation-testable relay rules.
4. Define three materially different outcomes.
5. Select the cheapest honest first confrontation resolution.
6. Only after the loop passes, run the map-substrate comparison.
