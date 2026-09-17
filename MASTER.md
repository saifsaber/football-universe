# MASTER.md — AI Football Game Studio Operating System
Version: 0.1-bootstrap
Status: PRE-SPEC / RESEARCH & ARCHITECTURE
Owner: Human Owner
Purpose: Build a production-quality football game/product from research to release using multiple AI coding/research agents without letting agents redesign the project during execution.

---

## 0. PRIME DIRECTIVE

This repository is not a prompt playground.

It is a controlled AI-operated game studio.

The final output must be a **real player-facing game/product**, not:
- a simulation-only demo,
- an admin dashboard,
- a collection of forms,
- a database viewer,
- a mockup,
- a prototype presented as a finished game.

### Fundamental equation

GAME =
Football World
+ Simulation
+ Player Decisions
+ Presentation
+ Interaction
+ Progression
+ Feedback
+ Emotion
+ UI/UX
+ Motion
+ Audio Hooks
+ Social Systems
+ Content
+ Quality Assurance

**SIMULATION != GAME**

---

# 1. HUMAN AUTHORITY

The Human Owner is the final authority for:
- product direction,
- legal/licensing commitments,
- paid services,
- installation of new external skills/tools/MCPs,
- destructive changes,
- architecture changes after spec freeze,
- release approval.

Agents may propose.
Agents may not silently change frozen decisions.

---

# 2. OPERATING MODES

The studio has only two operating modes.

## MODE A — DESIGN / RESEARCH MODE

Allowed:
- market research,
- competitor analysis,
- player-needs research,
- concept generation,
- product architecture,
- game design,
- UX research,
- data architecture,
- technical architecture,
- red-team review,
- prototyping.

Not allowed:
- claiming the product is production-ready,
- silently locking architectural decisions,
- uncontrolled feature implementation.

## MODE B — EXECUTION MODE

Begins only after SPEC FREEZE.

In execution mode:
- the product is already defined,
- agents execute approved tasks,
- agents do not redesign the product,
- agents do not add speculative features,
- agents do not replace approved architecture,
- agents do not create work for themselves,
- all changes outside task scope become CHANGE_REQUESTs.

---

# 3. SPEC FREEZE GATES

The project must pass these gates in order:

G0 — Research coverage complete  
G1 — Product opportunity approved  
G2 — Core game concept approved  
G3 — Core loops and progression approved  
G4 — Football data strategy approved  
G5 — Simulation architecture approved  
G6 — UX / design direction approved  
G7 — Technical architecture approved  
G8 — Vertical slice scope approved  
G9 — Red-team review passed  
G10 — SPEC FREEZE v1.0  
G11 — Implementation  
G12 — Player Experience Gate  
G13 — Release Candidate  
G14 — Human Release Approval

No builder may skip a gate.

---

# 4. SOURCE OF TRUTH

The following files become authoritative once created:

/MASTER.md  
/GAME_CONSTITUTION.md  
/PRODUCT_SPEC.md  
/GAME_RULES.md  
/ARCHITECTURE.md  
/DATA_MODEL.md  
/SIMULATION_SPEC.md  
/API_CONTRACTS.md  
/DESIGN.md  
/BRAND.md  
/ROADMAP.md  
/DECISIONS.md  
/PROJECT_STATE.json

After SPEC FREEZE:
- builders may READ these files,
- builders may NOT change them,
- changes require a formal CHANGE_REQUEST.

---

# 5. REQUIRED REPOSITORY STRUCTURE

Create:

/
├── MASTER.md
├── AGENTS.md
├── CLAUDE.md
├── GAME_CONSTITUTION.md
├── PROJECT_STATE.json
├── DECISIONS.md
├── ROADMAP.md
│
├── agents/
│   ├── control/
│   ├── research/
│   ├── product/
│   ├── football/
│   ├── simulation/
│   ├── experience/
│   ├── engineering/
│   ├── content/
│   ├── analytics/
│   ├── skills/
│   └── quality/
│
├── specs/
│   ├── product/
│   ├── gameplay/
│   ├── football/
│   ├── simulation/
│   ├── data/
│   ├── ux/
│   └── technical/
│
├── design/
│   ├── references/
│   ├── screens/
│   └── prototypes/
│
├── schemas/
├── workflows/
├── tasks/
│   ├── backlog/
│   ├── ready/
│   ├── running/
│   ├── review/
│   ├── blocked/
│   └── done/
│
├── gates/
├── policies/
├── permissions/
├── skills/
│   ├── registry/
│   └── approved/
├── evals/
├── reports/
├── scripts/
├── tests/
└── src/

---

# 6. CONTROL PLANE

The Control Plane manages the studio.

## Required control agents

### 6.1 Master Orchestrator
Mission:
- read project state,
- identify next legal task,
- route it to the correct agent,
- enforce dependencies,
- never invent product direction.

### 6.2 State Manager
Owns:
- PROJECT_STATE.json
- current phase
- task status
- blocked items
- open change requests
- spec version

### 6.3 Task Scheduler
May:
- assign existing approved tasks.

May not:
- invent product features,
- silently create new implementation scope.

### 6.4 Context Compiler
Builds the smallest possible context packet for each agent.

Rule:
**No agent receives the whole repository unless its task truly requires it.**

### 6.5 Permission Controller
Enforces:
- allowed read paths,
- allowed write paths,
- allowed tools,
- forbidden files.

### 6.6 Change Controller
Receives CHANGE_REQUEST documents.
No direct architectural mutation is permitted.

### 6.7 Model Router
Chooses model tier based on task difficulty.

### 6.8 Audit Logger
Records:
- task,
- model,
- tools,
- files changed,
- tests,
- validation result,
- reviewer,
- merge result.

---

# 7. MARKET INTELLIGENCE LAB

Purpose:
Understand the market before deciding the final product.

Research categories must include:

## Direct football management / strategy competitors
- Football Manager
- Top Eleven
- OSM
- Soccer Manager
- 38-0
- Modareb / "أنت المدرب"
- Hattrick
- Football Chairman
- other active football manager games

## Adjacent football products
- EA Sports FC Career
- Ultimate Team
- Fantasy Premier League
- Sorare
- Dream League Soccer
- eFootball
- World Soccer Champs
- prediction games
- football card games
- football social/community products

## Cross-genre inspiration
Study mechanics, not branding, from:
- strategy games,
- tycoon games,
- collection games,
- social competitive games,
- RPG progression systems,
- dynasty/legacy systems,
- asynchronous multiplayer products.

## Research agents
- Market Research Director
- Competitor Discovery Agent
- Competitor Reverse-Engineering Agent
- Player Review Miner
- Reddit / Community Miner
- Steam Review Miner
- App Store Review Miner
- YouTube / Creator Insight Agent
- Cross-Genre Mechanics Scout
- Trend Watcher
- Monetization Researcher
- Audience Segmentation Agent
- Jobs-To-Be-Done Analyst
- Retention Analyst
- Evidence Auditor

## Mandatory competitor schema

Every competitor must be stored using the same fields:

- audience
- platforms
- core fantasy
- first 60 seconds
- core loop
- meta loop
- session length
- progression
- career
- tactics
- transfers
- collection
- social
- PvP
- multiplayer
- live content
- monetization
- retention loop
- virality
- strengths
- weaknesses
- user praise
- user complaints
- requested features
- UI patterns
- visual identity
- switching barrier
- moat
- evidence links
- confidence

Research agents produce evidence.
They do NOT decide the product.

---

# 8. PLAYER INTELLIGENCE LAB

Classify player signals into:

LOVE  
HATE  
WISH  
BOREDOM  
ADDICTION  
RAGE  
CONFUSION  
CHURN  
SHARING  
COMPETITION  
REALISM  
TACTICS  
TRANSFERS  
CAREER  
COLLECTION  
SOCIAL  
PAY-TO-WIN  
ONBOARDING  
UI  
MATCHDAY

Create player segments such as:
- hardcore manager player
- casual football fan
- historical football fan
- social multiplayer player
- mobile-first player
- football data nerd
- collection-driven player
- career/story-driven player
- local-market football fan
- competitive player

AI-created personas are hypothesis tools only.
They never replace real-player validation.

---

# 9. OPPORTUNITY ENGINE

Input:
- competitor dataset,
- player-needs dataset,
- market trends,
- cross-genre mechanics.

Agents:
- White-Space Analyst
- Opportunity Analyst
- Differentiation Analyst
- Moat Analyst
- Risk Analyst
- Product Red-Team Agent

Output:
- opportunity map,
- unmet needs,
- candidate product concepts,
- reasons each concept may fail,
- evidence supporting each concept.

No concept advances without red-team review.

---

# 10. GAME DIRECTION LAB

Required roles:
- Creative Director
- Game Director
- Product Director
- Core Loop Designer
- Meta Loop Designer
- Progression Designer
- Career Designer
- Economy Designer
- Retention Designer
- Multiplayer Designer
- Social Designer
- Challenge / Event Designer
- Narrative Designer
- Onboarding Designer

The Game Director evaluates:
- fun,
- pacing,
- tension,
- emotional feedback,
- player agency,
- reward timing,
- replayability,
- fantasy fulfillment.

A feature is not complete because an API returns data.

---

# 11. GAME CONSTITUTION — NON-NEGOTIABLE RULES

The project must eventually formalize these in GAME_CONSTITUTION.md:

1. REAL FOOTBALL FIRST.
2. SIMULATION != GAME.
3. OFFICIAL MODES MUST NOT INVENT REAL PLAYERS, CLUBS, MANAGERS OR COMPETITIONS.
4. PLAYER-FACING GAMEPLAY MUST NOT DEGRADE INTO ADMIN FORMS.
5. NO PAY-TO-WIN COMPETITIVE ADVANTAGE.
6. PLAYER DECISIONS MUST HAVE LEGIBLE CONSEQUENCES.
7. SHORT SESSIONS AND DEEP SESSIONS SHOULD BOTH BE SUPPORTED WHERE PRODUCT RESEARCH JUSTIFIES IT.
8. PROGRESSION MUST CREATE OWNERSHIP AND LEGACY.
9. SOCIAL SYSTEMS MUST CREATE MEANINGFUL RIVALRY, COOPERATION OR SHARING.
10. AI-GENERATED TEXT MAY PRESENT FOOTBALL FACTS, BUT MAY NOT INVENT THEM.
11. PRODUCTION UI MUST HAVE AN APPROVED DESIGN SYSTEM.
12. NO PROTOTYPE LEAKAGE INTO PLAYER-FACING PRODUCTION SCREENS.

---

# 12. FOOTBALL DATA LAB

Required agents:
- Football Data Director
- Source Registry Agent
- Licensing / Rights Agent
- Data Ingestion Agent
- Entity Resolution Agent
- Player Agent
- PlayerSeason Agent
- Club Agent
- ClubSeason Agent
- Manager Agent
- Competition Agent
- Historical Data Agent
- Transfer Data Agent
- Match Data Agent
- Rating Agent
- Data QA Agent

## Canonical entity rule

Every real football entity requires:
- canonical ID
- canonical name
- aliases
- provenance
- verification status

Real player names may not be invented.

## Temporal model

The system must distinguish:
Player
from
PlayerSeason

and:
Club
from
ClubSeason

Example:
Mohamed Salah 2017/18 is not the same performance profile as Mohamed Salah 2024/25.

---

# 13. RIGHTS & LICENSING LAB

Must evaluate separately:
- player names,
- player images,
- likeness,
- club names,
- club logos,
- kits,
- competition branding,
- historical media,
- match data,
- photographs.

No agent may assume that publicly visible data/assets are automatically commercially usable.

---

# 14. FOOTBALL INTELLIGENCE

Build structured football intelligence for:
- player technical profile
- physical profile
- mental profile
- tactical profile
- position behavior
- roles
- consistency
- leadership
- big-match profile
- weak foot
- set pieces
- pressing
- defensive behavior
- movement
- creativity
- passing profile

Also build:
- Manager DNA
- Club DNA
- Tactical DNA

Ratings must be explainable and versioned.

---

# 15. SIMULATION LAB

Required agents:
- Simulation Director
- Match Engine Architect
- Tactical Model Agent
- Player Behavior Agent
- Possession Model Agent
- Out-of-Possession Agent
- Space / Positioning Agent
- Chemistry Agent
- Fitness Agent
- Morale Agent
- Injury Agent
- Referee Agent
- Context / Weather Agent
- Manager AI Agent
- Opponent AI Agent
- Match Narrative Interpreter
- Monte-Carlo Calibration Agent
- Meta Exploit Finder
- Simulation QA Agent
- Football QA Agent

## Determinism

Simulations must support deterministic reproduction by seed where practical.

A result must be debuggable.

---

# 16. WORLD ENGINE

Must eventually support approved scope for:
- competitions
- seasons
- fixtures
- promotion / relegation
- transfers
- contracts
- finances
- manager market
- youth academy
- player development
- aging
- injuries
- reputation
- club objectives
- board confidence
- fans
- media
- awards
- rankings
- world history

The world should continue evolving beyond the user's current team when the approved product concept requires it.

---

# 17. GAME MODES

The architecture should support multiple modes on shared core systems.

Possible examples, subject to research and approval:
- quick draft
- historical draft
- career
- manager career
- club legacy
- nations
- era wars
- what-if
- live challenges
- daily XI
- friend leagues
- live draft
- knockout competitions
- historical replay
- creator/community challenges

Do not implement all modes in the first release.

---

# 18. GAME EXPERIENCE DIVISION

Required agents:
- Experience Director
- UX Research Agent
- Navigation Architect
- Game UX Designer
- UI Art Director
- Design-System Architect
- Interaction Designer
- Motion Designer
- Matchday Presentation Designer
- Data Visualization Designer
- Audio Experience Designer
- Responsive UX Engineer
- Accessibility Specialist
- Onboarding UX Agent
- Visual Critic

## Rule

ADMIN UI != PLAYER UI

Forms, tables and raw data screens belong in:
- admin tools,
- debug tools,
- internal operations.

They must not replace game interactions.

---

# 19. DESIGN INTELLIGENCE WORKFLOW

Before production UI:

Product requirements
+
UX research
+
real product references
+
sports/broadcast references
+
brand direction
↓
DESIGN.md
↓
UI implementation

Approved reference systems may include:
- Refero
- Refero Styles
- Mobbin
- 21st.dev
- Transitions.dev
- real sports products
- real broadcast interfaces
- real analytics interfaces

Rules:
- study patterns,
- do not clone a competitor,
- convert references into an original design system,
- keep provenance for references.

---

# 20. ANTI-AI-LOOK QA

The Anti-AI Design Agent must flag:
- random purple gradients,
- generic rounded-card dashboards,
- default browser form controls,
- emojis used as final product icons,
- meaningless glassmorphism,
- giant empty sections,
- fake charts,
- repetitive card grids,
- generic landing-page styling inside game screens,
- developer/debug vocabulary shown to users,
- admin-table gameplay,
- unapproved typography,
- arbitrary animation.

---

# 21. PLAYER-FACING TACTICS / SQUAD RULE

A player-facing football screen should prefer direct manipulation and visual football metaphors when appropriate.

Example:
- pitch layout,
- player cards,
- drag/drop,
- roles,
- fitness,
- chemistry,
- contextual instructions.

Do not reduce the primary game experience to:
"Formation dropdown + player dropdown + submit button."

---

# 22. MATCHDAY EXPERIENCE TEAM

Matchday requires:
- match simulation
- pitch visualization
- match presentation
- commentary
- stats
- tactical feedback
- live decisions
- motion
- crowd/audio hooks
- post-match story
- player consequence feedback

A numeric score alone is not a finished matchday feature.

---

# 23. GAME CLIENT ENGINEERING

Required agents:
- Game Client Director
- Web/PWA Client Agent
- Mobile Architecture Agent
- Rendering Agent
- Pitch Renderer Agent
- UI Component Agent
- Client State Agent
- Realtime Client Agent
- Offline / Cache Agent
- Animation Runtime Agent
- Audio Runtime Agent
- Client Performance Agent

Game client engineers implement approved design.
They do not invent a new design system during implementation.

---

# 24. PLATFORM ENGINEERING

Required agents:
- Platform Architect
- Backend Agent
- API Agent
- Database Agent
- Cache Agent
- Queue Agent
- Realtime Agent
- Auth Agent
- Authorization Agent
- Notification Agent
- Search Agent
- Asset Storage Agent
- Analytics Agent
- Feature Flag Agent
- Admin Tool Agent
- Observability Agent
- Infrastructure / DevOps Agent
- Security Agent

---

# 25. SOCIAL / MULTIPLAYER

Possible approved systems:
- profiles
- friends
- following
- rivals
- private leagues
- public leagues
- live drafts
- asynchronous competitions
- groups/clubs
- creator challenges
- sharing
- records
- achievements
- chat
- moderation
- anti-cheat

All social systems require abuse/moderation consideration.

---

# 26. LIVE FOOTBALL LAYER

Potential pipeline:

Real football events
↓
verified data
↓
form/intelligence layer
↓
live game content
↓
challenges/events
↓
community interaction

Never let generative AI invent real-world football events.

---

# 27. CONTENT FACTORY

Content agents may produce:
- daily challenges
- weekly events
- historical scenarios
- what-if scenarios
- news presentation
- career narratives
- milestones
- rivalries
- achievements

Facts come from verified data.
AI controls presentation, not factual truth.

---

# 28. ANALYTICS LAB

Instrument approved events such as:
- onboarding completion
- time to first fun
- session duration
- D1 / D7 / D30 retention
- mode usage
- abandonment
- rage quit proxies
- transfer engagement
- social invites
- share rate
- challenge completion
- return triggers
- churn indicators

Analytics does not justify dark patterns.

---

# 29. EXPERIMENT LAB

Use:

Hypothesis
↓
Experiment
↓
Control/Treatment
↓
Metric
↓
Decision

No random UX mutation in production.

---

# 30. QUALITY FACTORY

Required:
- Code QA
- Integration QA
- E2E QA
- Database QA
- Data QA
- Simulation QA
- Football QA
- Game UX QA
- Visual QA
- Visual Regression QA
- Accessibility QA
- Performance QA
- Load QA
- Realtime QA
- Security QA
- Anti-Cheat QA
- Device QA
- Release QA

Builder != Reviewer whenever practical.

Cross-model review is preferred for critical work.

---

# 31. PLAYER EXPERIENCE GATE

A player-facing feature is not DONE until all applicable checks pass:

- backend
- game logic
- player UI
- interaction
- feedback
- responsive behavior
- loading state
- empty state
- error state
- accessibility
- analytics
- visual QA
- football QA
- E2E user journey

---

# 32. SCREENSHOT GATE

Every major player-facing screen must be captured and reviewed.

Reviewer asks:

"If this screenshot were shown beside a polished commercial game/product, would it look like:
- an AI-generated prototype,
- an admin dashboard,
- a developer tool,
- or an unfinished demo?"

If yes:
FAIL.

---

# 33. VERTICAL SLICE FIRST

Do NOT build backend-only for weeks before proving the player experience.

First production-quality vertical slice should cover something similar to:

Login
→ Choose club / starting context
→ Home
→ Squad
→ Tactics
→ Training or preparation decision
→ Matchday
→ Result
→ Table / progression
→ News / consequence
→ Next action

Exact scope is decided after research.

The slice must be playable end-to-end.

---

# 34. AGENT CONTRACT STANDARD

Every agent file must contain:

IDENTITY  
MISSION  
INPUTS  
ALLOWED READ PATHS  
ALLOWED WRITE PATHS  
TOOLS  
EXACT PROCEDURE  
FORBIDDEN ACTIONS  
OUTPUT SCHEMA  
VALIDATION  
DEFINITION OF DONE  
BLOCK CONDITIONS

Avoid vague instructions like:
"You are a world-class expert."

Professionalism comes from procedure, constraints, evidence and validation.

---

# 35. TASK CONTRACT STANDARD

Every implementation task must be structured.

Example:

task_id: UX-043
agent: squad-ui-engineer
objective: Implement approved squad interaction.

inputs:
- GAME_UX.md#squad
- DESIGN.md
- API_CONTRACTS.md#squad

allowed_read:
- /src/client/**
- /specs/ux/**
- /design/**

allowed_write:
- /src/client/squad/**
- /tests/client/squad/**

forbidden:
- redesign API
- change database schema
- change frozen product rules
- add dependency without approval
- edit unrelated files

done_when:
- implementation passes tests
- visual QA passes
- responsive QA passes
- E2E journey passes
- no files outside allowed_write changed

---

# 36. PROJECT STATE

PROJECT_STATE.json should track:

{
  "spec_version": "0.1-bootstrap",
  "mode": "DESIGN",
  "phase": "BOOTSTRAP",
  "active_tasks": [],
  "completed_tasks": [],
  "blocked_tasks": [],
  "change_requests": [],
  "approved_skills": [],
  "release_status": "NOT_READY"
}

Only the State Manager updates this file.

---

# 37. TASK CREATION RULE

Execution agents may NOT create tasks for themselves.

They may create:
TASK_PROPOSAL

A Planner / Scheduler may later convert an approved proposal into a task.

---

# 38. CHANGE REQUEST RULE

If an agent discovers a design/architecture problem after freeze:

Do NOT silently fix the architecture.

Create:

CHANGE_REQUEST
- id
- affected spec
- problem
- evidence
- impact
- suggested change
- blocking: true/false

Continue unrelated work if safe.

---

# 39. CONTEXT ISOLATION

Each task receives the minimum required context.

Examples:

UI task:
- DESIGN.md
- exact screen spec
- relevant API contract
- approved components

Simulation task:
- SIMULATION_SPEC
- relevant data schemas
- calibration datasets
- tests

Do not dump the whole repository into every agent.

---

# 40. AGENT COMMUNICATION

Allowed status:
RUNNING
BLOCKED
FAILED
DONE

Agents should not send conversational progress chatter during autonomous execution.

BLOCKED is valid only for predefined reasons such as:
- missing required file
- credential required
- legal approval required
- external paid purchase required
- destructive action approval required
- skill install approval required
- frozen-spec contradiction

---

# 41. SKILL & TOOL ACQUISITION PLANE

Agents are not assumed to possess every useful skill/tool.

If a capability is missing:

TASK
↓
Capability available?
├─ YES → execute
└─ NO
   ↓
Skill Gap Detector
   ↓
Skill Discovery Agent
   ↓
Search trusted sources
   ↓
Security / provenance audit
   ↓
Compatibility check
   ↓
Sandbox test
   ↓
HUMAN APPROVAL
   ↓
Install and pin exact version/commit
   ↓
Register skill
   ↓
Resume task

## Discovery sources may include
- official product documentation
- official skill/plugin marketplaces
- trusted MCP registries
- GitHub repositories
- established open-source libraries

## Mandatory installation rules

NO:
- blind curl | bash
- unknown binaries
- unpinned dependencies
- unexplained network permissions
- unexplained secret access
- auto-install from untrusted repositories
- silent paid subscription activation

Every installed skill must have:
- name
- source
- exact version or commit
- purpose
- requested permissions
- security notes
- compatibility notes
- approved_by
- approved_date
- consuming agents

Store registry in:
/skills/registry/

---

# 42. GITHUB MULTI-AGENT OPERATING MODEL

Both Codex and Claude Code may work on the same repository.

They must NOT edit the same branch concurrently.

Protected branches:
- main
- integration

Agent branches follow:

agent/codex/<TASK-ID>
agent/claude/<TASK-ID>

No direct push to main.
No direct push to integration unless explicitly performed by the Integration Agent.

Workflow:

Task
↓
isolated branch/worktree
↓
implementation
↓
tests
↓
push
↓
PR
↓
independent review
↓
CI
↓
integration
↓
release gates
↓
main

---

# 43. TASK CLAIMING

Recommended GitHub labels:

status:ready
status:running
status:review
status:blocked
status:done

agent:codex
agent:claude

type:research
type:frontend
type:backend
type:simulation
type:data
type:design
type:qa

priority:P0
priority:P1
priority:P2

An agent only claims:
- tasks assigned to its agent label,
- status:ready,
- with all dependencies satisfied.

---

# 44. CROSS-MODEL REVIEW

Preferred rule:

Codex-built critical feature
→ Claude review

Claude-built critical feature
→ Codex review

Critical systems should not rely only on self-review.

---

# 45. MODEL ROUTING POLICY

Do not hard-code a permanent model name into the architecture.

Model availability changes.

Route by capability tier:

## Tier A — Frontier reasoning / coding
Use for:
- product architecture
- technical architecture
- simulation architecture
- critical integration
- difficult debugging
- security-sensitive logic
- final review

## Tier B — Strong independent reviewer
Use for:
- architecture challenge
- code review
- red-team analysis
- spec contradiction detection

## Tier C — Fast worker
Use for:
- research batches
- review mining
- extraction
- normalization
- repetitive tests
- low-risk migrations
- localization
- documentation
- bulk transformations

Default operating strategy:
Frontier Lead
+ Parallel Fast Workers
+ Independent Frontier Reviewer

Optimize wall-clock time, not just number of active agents.

---

# 46. AUTOMATION / HEARTBEAT POLICY

Primary execution should be EVENT-DRIVEN.

Examples:
- task completed → schedule next task immediately
- PR opened → reviewer starts immediately
- CI passes → integration begins immediately

A recurring heartbeat may run every few hours only as a recovery mechanism:

Heartbeat:
1. read MASTER.md
2. read PROJECT_STATE.json
3. detect stalled tasks
4. detect failed CI
5. detect unreviewed PRs
6. detect merge conflicts
7. detect idle workers with ready tasks
8. resume/assign safe work
9. do not redesign product
10. do not duplicate an active task

Do not wait for the heartbeat if an event can trigger the next action immediately.

---

# 47. SECURITY / SECRET POLICY

Never commit:
- API keys
- tokens
- private credentials
- paid service secrets
- SSH private keys

Use environment secrets.

External services require explicit configuration.

Agents may not exfiltrate repository data.

---

# 48. BOOT SEQUENCE

When an AI environment is attached to this repository, it must perform:

1. Read MASTER.md.
2. Read PROJECT_STATE.json.
3. Confirm current operating mode.
4. Validate repository structure.
5. Validate Git state.
6. Validate required tools.
7. Load only allowed task context.
8. Check dependencies.
9. Check permissions.
10. Check whether a missing skill requires discovery.
11. Execute current approved task.
12. Run required validation.
13. Open/update PR if applicable.
14. Update task status through authorized control process.
15. Stop or claim next approved task.

Do NOT begin by asking:
"What should I build?"

The state and task queue define what to build.

---

# 49. FIRST BOOTSTRAP MILESTONE

The first milestone is NOT "build the football game."

The first milestone is:

**BOOTSTRAP THE FACTORY CORRECTLY.**

Required output:

- repository structure created
- main/integration branch policy defined
- AGENTS.md adapter created
- CLAUDE.md adapter created
- PROJECT_STATE.json initialized
- task schema created
- change-request schema created
- skill registry created
- permissions policy created
- research workflow created
- initial competitor research backlog created
- CI skeleton created
- no production game code yet

After bootstrap:
start Research Phase.

---

# 50. BOOTSTRAP DEFINITION OF DONE

Bootstrap is DONE only when:

- both Codex and Claude Code can read the same source-of-truth repository,
- they cannot write directly to protected production branches,
- each can work on isolated branches/worktrees,
- task claiming is explicit,
- conflict ownership rules exist,
- skill installation requires approval,
- project state is machine-readable,
- review flow is defined,
- no agent can silently rewrite the frozen product,
- no production implementation has begun before research architecture gates.

---

# 51. FINAL PRODUCT DEFINITION

The project is finished only when a real player can:

- enter the product,
- understand what to do,
- make meaningful football decisions,
- experience game feedback,
- progress,
- save/resume,
- use polished player-facing UI,
- complete the intended core loop,
- encounter tested failure/error states,
- use the product on supported targets,
- and pass release-quality QA.

A working simulation API is not completion.

A working database is not completion.

A polished screenshot is not completion.

A production game is the completion condition.

---

# 52. INITIAL HUMAN ACTION — DO THIS FIRST

Before connecting any agent:

1. Create a new PRIVATE GitHub repository.
2. Name it something temporary, e.g.:
   `football-universe`
3. Create or protect:
   `main`
   `integration`
4. Put this file at:
   `/MASTER.md`
5. Add:
   `/AGENTS.md`
   `/CLAUDE.md`
   `/PROJECT_STATE.json`
   as the next bootstrap files.
6. Do not add production game code yet.
7. Connect Codex to the repository.
8. Clone the same repository locally for Claude Code.
9. Test each system with one harmless bootstrap task on a separate branch.
10. Only after both workflows pass, enable recurring/parallel execution.

END OF MASTER.md
