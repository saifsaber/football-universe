# PROD-001 — Player Career: Design and Agent Execution Blueprint
Version: 0.1-proposed
Date: 2026-09-25
Task: #6
Authority: MASTER.md first, then repository authority chain and owner-approved amendments.
Status: DESIGN PROPOSAL. Not a frozen specification, implementation authorization, playable build, or completed game.

## 1. Owner direction and product promise
The owner approved planning a polished football player-career game: create a protagonist, play football directly, develop a recognizable style, and experience a complete beginning-to-ending journey. This document proposes a narrower direction for review; it does not silently replace existing authority files or declare any gate passed.

Begin on a local pitch, win opportunities, build relationships, and finish a season with a professional trial. The main activity is playing through one character. Career decisions make matches meaningful.

Opening flow: create player → playable warm-up → local match → understandable performance feedback → training/relationship choice → next fixture.

## 2. Proposed complete v1
All quantities and controls below are hypotheses awaiting validation:
- Single-player, offline-first, one controlled outfield player.
- Initial 3v3 means one goalkeeper and two outfield players per team; the user controls one outfield player. Keeper and other players are AI-controlled.
- One season, initially 10–12 fixtures and a final trial; four fictional opponent teams and three pitches.
- A small recurring cast: coach, teammate, rival, scout.
- Creator, dribbler and finisher playstyles; capabilities change play rather than merely increase numbers.
- Matches initially 4–6 minutes; short branching events reconverge on common fixtures.
- Multiple ending outcomes; replay the season with a different style.
- Tutorial, pause/settings, accessibility, save/resume, recovery, credits and clear ending.
- Keyboard is the proposed first control target. Platform selection must confirm this; gamepad/touch are evaluated and separately scoped.
- 5v5, 11v11, online multiplayer, open world, extensive transfers, live services and additional seasons are outside v1.

Fictional club names, logos and kits; user-created protagonist. Existing real-football requirements need an explicit design decision at G4: which real-player identities appear, in what role, with what verified data. Do not silently fabricate real people or silently discard existing real-football requirements. No legal determination is made here.

## 3. Systems and design rules
### Football and match rules
Movement, first touch, aim, pass/request pass, shot, sprint/stamina, interception and simple tackle. Prototype must specify pitch dimensions, boundaries, goals, possession, collision, restarts, fouls or their explicit omission, full time and draws. Avoid skill-move proliferation before passing feels good. Control assists must be understandable.

### Team and opponent AI
Maintain space, offer passing options, support possession, track threats and recover on turnover. Keepers need readable positioning, save/rebound and restart states. Use inspectable tactical behaviors rather than hidden stat boosts. Team/player identities are stable across simulation and saves.

### Career and progression
Reward support, defensive actions and positioning as well as goals. Define selection, fatigue, training and ability unlocks. Prevent easy reward farming, mandatory repetitive grinding and unrecoverable progression dead ends. Initial numerical balance is a test hypothesis.

### Narrative and season
Fixture graph, standings, selection/trial eligibility, relationship events and ending conditions must be explicit. Story consumes verified match outcomes: never narrate a goal, injury or selection that the game did not establish. Failure should provide continuation or a clearly explained ending.

### Economy
Bounded earned training resources; no shop, advertising SDK, paid currency, gambling mechanics or real-money purchases.

### Presentation
Angled 2D view, readable characters/team markers, visible ball, responsive first-touch/kick animation, short celebrations and meaningful sound feedback. Prioritize contact, goal, whistle and crowd sounds over extensive commentary. Asset provenance/permissions and original club identity are recorded.

### UX and accessibility
Playable onboarding, creation, career hub, fixture, results, training/events, endings and settings. Remapping, readable text, subtitles, reduced motion, separate audio sliders, color-independent markers and adjustable timing assistance. Do not communicate essential state only through color or sound.

### Saves, robustness and privacy
Versioned local saves, safe autosave checkpoints, previous-save recovery and validated loaded data. A failed save must be visible. Specify interruption behavior, resume position, migration and corrupt-save fallback. No credentials or telemetry by default.

## 4. Platform and technology decision
P03 compares a browser approach and a dedicated 2D engine such as Godot against available tools, deployment friction, input support, animation workflow, debugging, storage reliability and maintainability. No engine is selected by this document.
First do documentary evaluation; no installs, dependencies, paid services or downloads requiring approval are authorized.
Record target device/browser or native platform, frame-rate/memory/loading targets and evidence before setting performance acceptance thresholds. Do not claim measured performance before testing.

## 5. Sequential agent work packages
These are role assignments and PROPOSED packages, not READY tasks. Expand each into a complete approved task contract before claiming. One package can require several bounded checkpoints. One writer owns each path; only one task worker runs at a time.

| ID / role | Required input and dependency | Procedure and output | Acceptance / stop |
|---|---|---|---|
| P01 Product and research | Authority, owner direction, existing evidence | Compare player-career and small-sided mechanics; audience/needs evidence register; risks and scope proposal | Sources/date/confidence attached; distinguish evidence from opinion; insufficient coverage blocks G0 |
| P02 Gameplay designer | Approved P01 and G1 | Define concept, controls, full match state/rules, keeper role, tutorial and intended decisions | No undefined restart/result states; owner concept approval G2 |
| P03 Technical architect | P02 draft, verified repo/tool inventory | Compare platform/engine; propose modules/input/simulation/render/save boundaries; later finalize after G6 | Decision record with trade-offs and test plan; no installs; draft is not G7 approval |
| P04 Experimental prototype worker | Approved P02/P03 prototype contract and explicit DESIGN prototype permission | Greybox 3v3: move/pass/shoot, support/keeper AI, score/restarts | Reproducible complete match; no career/content scope; experiment is not production implementation |
| P05 Human playtest and QA | P04 build, test script and actual consenting testers | Observe onboarding/control/AI; log failures and replay interest; recommend go/revise/stop | Human observations required; AI self-test cannot establish fun |
| P06 Career/season designer | P05 pass and approved direction | Specify progression, selection, fixture/event graph, economy and ending conditions | Complete win/lose journeys, no farming/dead ends; core loop approval G3 |
| P12 Football data designer | G3, real-football requirement, owner identity decision | Identity/attribute/source schemas, provenance/verification and fictional/real separation | G4 approval; real facts sourced, identity scope explicit |
| P13 Simulation and AI architect | G4, prototype measurements, P02 rules | Match state machine, AI behaviors, seed/replay strategy, deterministic test boundaries | G5 approval; explainability and reproducible failure cases |
| P07 Art/audio/UX designer | G5, P06, platform proposal, approved asset constraints | Design sheet, screen journey, animations, sound list, accessibility and asset register | Gameplay-scale readability, all error states; owner direction approval G6 |
| P08 Slice specification then implementation worker | Specification after G7; implementation only after G10 | Define G8 slice scope; later build creation → match → result → event/training → save → next fixture | G8 scope approved separately; production slice validated only after G10 |
| P09 Content/integration worker | Validated production slice and approved content contracts | Fill one-season fixtures/events/opponents/assets, difficulty and endings | Every ending reachable; no broken references; full resume journey; no implicit merge authority |
| P10 Independent QA/security reviewer | RC candidate, changed commits, acceptance matrix | Gameplay, save corruption, accessibility, input/device/performance and scope tests; fresh critical review | BLOCKER/MAJOR resolved and rechecked; no self-approval |
| P11 Release agent | G12/G13 passed, explicit release authority | Package/instructions/known limits/recovery/credits; release checklist | Human G14 approval before publishing; credentials/deploy separately authorized |

### Exact gate order
Bootstrap blockers (including existing PRs) require their own authorized resolution. This plan does not merge them.
G0: P01 research coverage complete.
G1: owner approves product opportunity.
G2: P02 core concept approved.
P04/P05 may run only under a separately approved, scoped experimental DESIGN task where repository policy permits it. If that authority is absent, defer them until G10. An experimental label alone grants no permission; the prototype does not unlock production.
G3: P06 core loops/progression approved.
G4: P12 data strategy approved.
G5: P13 simulation architecture approved.
G6: P07 UX/design direction approved.
G7: P03 final technical architecture approved.
G8: P08 vertical-slice scope approved.
G9: fresh independent red-team review of the combined specification passed.
G10: explicit SPEC FREEZE v1.0 through authorized control process.
G11: P08/P09 production implementation.
G12: P10 applicable Player Experience Gate passed.
G13: validated release candidate.
G14: Human Release Approval, then authorized publication.

Drafting earlier architectural ideas is allowed as design work; marking their gate passed out of order is not.

P03-DRAFT is technology research; P03-FINAL is the G7 technical architecture deliverable. P08-SPEC is the G8 scope document; P08-BUILD is production after G10. These are separate deliverables requiring separate approved task contracts, avoiding circular dependencies.

Every gate record must contain: gate_id, required_artifacts, acceptance_criteria, authorized_approver, status, evidence_ref. Initial status for this proposed direction is NOT_PASSED and evidence_ref is null. The authorized control process determines approvers; Human approval is mandatory for product-direction, freeze and release decisions. Creating an artifact alone does not pass a gate.

## 6. Prototype fun gate and polish evidence
Proposed initial test: five testers, two short matches each. This is qualitative feedback, not a market-success claim.
Go only when testers can move/pass/shoot after onboarding, explain turnovers/goals, receive useful teammate support, avoid match soft-locks and identify enjoyable decisions/replay interest.
Record tester observations separately from machine tests. Rework if controls or AI consistently frustrate. Stop content expansion when focused iterations fail to establish enjoyable play.

Polish evidence for production: gameplay screenshots/replays, contact/goal feedback, readable UI at target resolution, no blocked camera view, consistent input timing, complete loading/pause/error states, audible/visual alternatives and testing on named target hardware. Owner acceptance of gameplay feel remains necessary.

## 7. Proposed interface packet (not frozen)
World coordinates: meters; time seconds; origin pitch center; +X length, +Y width. Projection belongs to rendering, not simulation.
Proposed fixed simulation step: 60Hz, validated against target hardware before freezing.
Input: move, aim, pass, shoot, sprint, tackle, request_pass, pause.
Domain events: MatchStarted, PossessionChanged, PassCompleted, ShotTaken, GoalScored, MatchEnded, TrainingCompleted, CareerChoiceCommitted.
Each event carries schema_version, simulation_tick, actor/entity IDs and validated payload.
Save: save_version, player_id, season/fixture position, progression, relationships, committed outcomes, settings and deterministic seed where relevant.
Match logic owns scores/results; career consumes results; UI does not mutate authoritative outcomes.
Separate display identity, gameplay attributes and asset references.
Specify event uniqueness/commit semantics to prevent duplicated rewards after reload.

## 8. Agent context and ownership
Every assignment receives: exact authority versions; approved task and gate evidence; only dependency outputs needed; file paths and base SHA; interface versions; acceptance tests; known failures; budget/checkpoint remaining; forbidden actions; reviewer and handoff destination. Missing required context blocks execution rather than encouraging guesses.

Proposed path ownership, to verify/authorize per task:
P01 reports/research/**; P02 specs/gameplay/**; P03 specs/technical/**; P04 design/prototypes/**; P05 reports/playtests/**; P06 specs/product/career/**; P12 specs/data/**; P13 specs/simulation/**; P07 design/** and specs/ux/** excluding prototype ownership; P08/P09 approved src/gameplay/**, src/career/**, src/persistence/**, src/ui/**, assets/** and corresponding tests/**; P10 reports/qa/**; P11 release documentation only unless deployment separately approved.
Shared code/interfaces have one explicitly named owner and conflict check. Only State Manager updates PROJECT_STATE.json. Planning PROD-001 writes ONLY this file.

### Reusable task contract
```yaml
task_id: <approved unique ID>
title: <specific result>
status: PROPOSED
priority: <assigned priority>
assigned_agent: codex
assigned_model_tier: <approved capability tier>
objective: <one measurable objective>
phase: <current authorized phase>
dependencies: [<completed task IDs>]
required_inputs: [<versioned files, decisions, gate evidence>]
allowed_read_paths: [<exact task scope>]
allowed_write_paths: [<exact task scope>]
forbidden_actions: [protected_writes, unauthorized_merge, installs, spending, secrets]
required_tools: [<already authorized tools>]
required_skills: [<approved applicable skills>]
validation_commands: [<actual reproducible commands or documented manual checks>]
review_required: true
reviewer: <fresh independent Codex context>
done_when: [<observable acceptance including applicable review/CI/merge>]
block_conditions: [<missing inputs, conflicts, gate failures, budget limits>]
```
Lifecycle: PROPOSED → APPROVED → READY → CLAIMED → RUNNING → REVIEW → VALIDATION → DONE; do not skip. Branch agent/codex/<TASK-ID>; PR into integration; no automatic critical merge. Record checkpoint and next action on the authorized task branch/issue. Review severity BLOCKER/MAJOR/MINOR/NOTE.

## 9. Validation and execution boundaries
Acceptance matrix must cover: match resets/full time; pass/shot edge cases; keeper recovery; stuck AI; event consistency; non-goal contribution; progression exploits; season/ending reachability; save/reload/corruption/migration/interruption; remapping; reduced motion/color/audio independence; target performance and device compatibility.
Do not write meaningless tests mirroring implementation. Name actual build/test commands only after choosing the stack. Critical review uses a fresh Codex context.

Quota mode currently FIXED_LIMITS_UNVERIFIED_QUOTA; session/daily/weekly/monthly/reset unavailable = null. No reserve protection claim. At most 15 minutes and 30 calls total per run, one task/checkpoint, reserve last 3 minutes/5 calls; no rollover or parallel task workers. Stop on real rate-limit/exhaustion signal. No installations, purchases, credits or emergency spend.
Engine, product positioning, platform, content quantities, real-player role and final fun acceptance remain explicit decisions. No calendar completion estimate is promised.

Immediate deliverable: this design blueprint and PR. Next eligible scope: authorize/assign bounded P01 evidence work and resolve bootstrap integration ownership. Later packages are not executable merely because they appear here.
