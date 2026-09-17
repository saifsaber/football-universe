# CODEX_AUTONOMOUS_6H_BUDGETED.md
Version: 1.1
Project: `saifsaber/football-universe`
Primary worker: Codex only
Timezone: `Africa/Cairo`
Schedule: 00:00 / 06:00 / 12:00 / 18:00
Cadence: every 6 hours

Authority order:
1. `MASTER.md`
2. `PROJECT_STATE.json`
3. `AGENTS.md`
4. `TASK_PROTOCOL.md`
5. `PERMISSIONS.md`
6. Approved frozen specifications

---

# 1. PURPOSE

Run the football-universe project autonomously with Codex only, four times per day, while:

- maximizing useful progress,
- protecting daily/weekly/monthly model usage,
- never exhausting the weekly quota before future scheduled runs unless the Human Owner explicitly authorizes emergency spend,
- keeping enough reserve for later runs,
- prioritizing critical-path tasks,
- avoiding wasted reasoning,
- preserving QA, security, review, and approval gates.

Claude Code is not part of this repository execution unless the Human Owner explicitly changes this later.

---

# 2. SCHEDULE

Run at:

- 00:00 Africa/Cairo
- 06:00 Africa/Cairo
- 12:00 Africa/Cairo
- 18:00 Africa/Cairo

Equivalent:
`every 6 hours`

Do not intentionally wait for the next tick if safe approved work can continue inside the current run.

But never continue blindly if doing so risks consuming too much of the remaining usage budget.

---

# 3. USAGE / QUOTA CONTROL — MANDATORY

At the start of EVERY run:

1. Read any available Codex / ChatGPT usage indicators.
2. Detect, when available:
   - remaining per-session / per-run usage,
   - remaining daily usage,
   - remaining weekly usage,
   - remaining monthly usage,
   - reset timestamps,
   - current model/effort consumption characteristics.
3. If an exact quota value is not exposed:
   - do NOT invent one,
   - estimate conservatively from visible usage indicators and recent run history,
   - record the estimate and confidence.
4. Store usage observations in:
   `reports/usage/CODEX_USAGE_STATE.json`
   or the nearest approved equivalent.

Never hardcode product limits unless they are verified from the current account/runtime.

---

# 4. CORE BUDGET RULE

The weekly quota is the primary protection target.

The automation must preserve enough remaining weekly capacity for future scheduled runs.

Default rule:

- do not spend the entire weekly allowance early,
- do not allow one run to consume an outsized share of the week's remaining capacity,
- keep a reserve for later critical tasks,
- reduce effort before skipping future runs.

If remaining weekly quota is measurable, calculate:

`remaining_runs_this_week`

based on the next reset time and the 4-runs-per-day schedule.

Then compute a conservative run budget:

`safe_run_budget = (remaining_weekly_budget - protected_weekly_reserve) / remaining_runs_this_week`

Use this as an upper bound, not a target to fully spend.

---

# 5. PROTECTED WEEKLY RESERVE

Unless the Human Owner explicitly overrides it, preserve:

- minimum 20% of the weekly quota as protected reserve,
- preferably 25% when project state is uncertain,
- never intentionally drop below 15% before the final scheduled run preceding reset.

Reserve exists for:

- unexpected blockers,
- CI failures,
- integration problems,
- high-value debugging,
- human-requested urgent tasks,
- final review before reset.

If usage information is coarse rather than numeric, interpret the UI conservatively.

---

# 6. DAILY BUDGETING

Four runs happen per day.

Do not use the entire useful daily capacity in the first run.

Default behavior:

- 00:00 run: up to 20–25% of safe daily allocation
- 06:00 run: up to 20–25%
- 12:00 run: up to 20–25%
- 18:00 run: remaining safe allocation, while preserving weekly reserve

If a run finishes critical-path work using less, do NOT spend the rest just because budget remains.

Unused budget carries forward.

---

# 7. MONTHLY BUDGETING

If the product/account exposes a monthly quota:

1. detect remaining monthly usage,
2. detect reset date,
3. estimate remaining scheduled runs in the month,
4. reserve at least 15–20% of monthly capacity,
5. never let a short-term sprint consume so much that later weeks become unusable.

If no monthly quota is exposed:
- do not assume one exists,
- skip monthly enforcement,
- continue weekly/daily control.

---

# 8. RUN STOP THRESHOLDS

A run must stop or downshift when ANY of the following occurs:

- current run reaches its safe budget,
- weekly remaining usage approaches protected reserve,
- daily capacity becomes too low for later ticks,
- monthly capacity, if applicable, approaches protected reserve,
- task value is too low relative to expected model cost,
- only non-critical polish remains,
- additional work would require expensive high-effort reasoning with low expected payoff.

Before stopping:
- commit safe work,
- push branch,
- update PR,
- record next task,
- leave repository resumable.

---

# 9. USAGE-ADAPTIVE MODEL / EFFORT POLICY

Use the lowest-cost sufficient mode for each task.

## Low-cost / routine
Use fast / low reasoning where appropriate for:
- file discovery,
- formatting,
- mechanical refactors,
- schema updates,
- straightforward tests,
- simple documentation,
- repetitive extraction,
- status synchronization.

## Medium
Use medium reasoning for:
- normal implementation,
- integration,
- non-trivial debugging,
- data modeling,
- workflow design.

## High / frontier
Use high reasoning only for:
- difficult architecture,
- simulation design,
- security-critical work,
- complex debugging,
- ambiguous system design,
- major integration failures,
- critical review.

Do NOT use maximum reasoning by default.

Expensive reasoning must be justified by expected value.

---

# 10. TASK VALUE / COST RANKING

Before starting a task, classify it:

## Tier A — Critical
- unblocks many downstream tasks,
- fixes broken integration,
- closes a release/gate blocker,
- critical architecture/security/simulation issue.

## Tier B — High value
- important vertical-slice functionality,
- high-impact research,
- important QA/review,
- major UX issue.

## Tier C — Normal
- useful implementation,
- routine tests,
- documentation required for execution.

## Tier D — Low priority
- polish,
- optional refactor,
- speculative improvement,
- duplicate research.

When quota is constrained:
A > B > C > D

Tier D should be deferred first.

---

# 11. NO WASTED RUNS

Do not burn model usage on:

- repeatedly rereading unchanged large files,
- redoing accepted research,
- reconsidering frozen decisions,
- generating long progress prose,
- speculative redesign,
- duplicate validation,
- unnecessary brainstorming,
- low-value reports,
- reformatting without benefit.

Prefer:
- diff-based reads,
- targeted file reads,
- cached summaries,
- machine-readable state,
- focused validation.

---

# 12. MANDATORY STARTUP SEQUENCE

At every run:

1. sync repository,
2. read `PROJECT_STATE.json`,
3. read changed sections of source-of-truth files,
4. inspect open PRs,
5. inspect CI,
6. inspect READY/RUNNING/BLOCKED tasks,
7. inspect pending approvals,
8. inspect current usage/quota state,
9. calculate safe run budget,
10. select highest-value valid task.

Do NOT load the entire repository into context unless necessary.

---

# 13. TASK SELECTION ORDER

Priority order:

1. P0 blocker
2. failed CI / broken integration
3. resumable RUNNING task
4. READY task on critical path
5. task unlocking most dependencies
6. gate-closing task
7. required review/QA
8. state/document synchronization
9. lower-priority work only if safe budget remains

Never select:
- speculative tasks,
- future-gate tasks,
- duplicate work,
- unresolved dependency tasks,
- Claude-assigned tasks.

---

# 14. CONTINUE WITHIN THE SAME RUN

One run should NOT stop after a tiny task if:

- safe budget remains,
- there is another approved READY task,
- no human approval is required,
- no collision/conflict exists.

Continue with the next highest-value task.

But do NOT exceed safe usage budget merely to maximize task count.

---

# 15. PARALLELISM

Parallelize only independent work.

Each parallel worker must have:

- unique task ID,
- separate branch/worktree,
- exclusive write paths,
- bounded context,
- explicit validation.

Parallelism must reduce wall-clock time without multiplying model cost wastefully.

If two workers would need to read/reason over the same large context, prefer sequential execution unless parallel value is clear.

---

# 16. GIT POLICY

Never implement directly on:

- `main`
- `integration`

Use:

`agent/codex/<TASK-ID>`

Workflow:

1. branch from latest `integration`
2. implement
3. validate
4. commit with task ID
5. push
6. open PR to `integration`
7. review
8. validate
9. merge only under project policy

---

# 17. CODEX-ONLY REVIEW POLICY

Claude is not used for this repository right now.

For critical work:

- builder context != reviewer context,
- use a fresh independent Codex reviewer context,
- do not let the same reasoning context self-approve critical changes.

Review severity:

- BLOCKER
- MAJOR
- MINOR
- NOTE

BLOCKER / MAJOR must be resolved before merge unless Human Owner explicitly approves.

---

# 18. SKILL / TOOL DISCOVERY

If a missing tool, skill, MCP, plugin, test utility, browser tool, visual QA tool, library, or workflow could materially improve speed or quality:

1. identify the capability gap,
2. research trusted sources,
3. compare options,
4. inspect license,
5. inspect permissions,
6. inspect security,
7. inspect network/secrets,
8. estimate expected benefit,
9. create `SKILL_REQUEST`.

Do NOT install without Human Owner approval.

Never:
- blind `curl | bash`,
- unknown binaries,
- silent paid services,
- unpinned dependencies,
- unexplained secret access.

---

# 19. RESEARCH POLICY

For current or niche research:

- prefer primary/official sources,
- preserve URLs/provenance,
- date time-sensitive findings,
- separate fact from interpretation,
- never fabricate real football facts,
- never invent real players/clubs/managers/competitions/transfers/results.

Use lower-cost workers for extraction.
Reserve high reasoning for synthesis/decision support.

---

# 20. PLAYER EXPERIENCE POLICY

`SIMULATION != GAME`

Reject final player UI that looks like:

- admin dashboard,
- database viewer,
- JSON inspector,
- generic form,
- prototype,
- AI-generated card grid,
- placeholder-heavy screen.

For player-facing work require:
- approved design system,
- football-native interactions,
- responsive behavior,
- screenshot review,
- visual QA,
- E2E journey,
- football QA.

---

# 21. VERTICAL SLICE PRIORITY

Once gates permit implementation, prioritize the approved production-quality vertical slice:

Login
→ Choose Club / Starting Context
→ Home
→ Squad
→ Tactics
→ Training / Preparation
→ Matchday
→ Result
→ Table / Progression
→ News / Consequences
→ Next Action

Do not spread usage across dozens of unfinished systems.

---

# 22. FAILURE / RETRY

Retry 1:
fix direct error.

Retry 2:
change implementation approach.

Retry 3:
independent review / TASK_PROPOSAL / CHANGE_REQUEST.

After repeated failure:
BLOCK.

Do not consume large amounts of quota repeating the same failed strategy.

---

# 23. CHANGE CONTROL

If a frozen spec seems wrong:

Do not silently change it.

Create CHANGE_REQUEST with:

- affected spec
- problem
- evidence
- impact
- suggested change
- alternatives
- blocking yes/no

Continue unrelated safe work.

---

# 24. HUMAN APPROVAL GATES

Stop for approval when needed for:

- external skill/tool install,
- paid service,
- new secret scope,
- destructive action,
- legal/licensing commitment,
- post-freeze architecture change,
- production release,
- emergency quota overspend.

---

# 25. EMERGENCY QUOTA SPEND

Only exceed normal run/weekly budget when ALL are true:

1. issue is P0 / project-blocking,
2. fixing now materially avoids larger future cost,
3. protected reserve remains reasonable,
4. Human Owner explicitly approves emergency spend.

Without explicit approval:
do not exhaust weekly quota.

---

# 26. USAGE STATE RECORD

Maintain a machine-readable usage state when possible:

`reports/usage/CODEX_USAGE_STATE.json`

Suggested structure:

```json
{
  "observed_at": "",
  "timezone": "Africa/Cairo",
  "weekly_reset_at": "",
  "monthly_reset_at": null,
  "weekly_remaining": null,
  "daily_remaining": null,
  "monthly_remaining": null,
  "remaining_scheduled_runs_this_week": null,
  "protected_weekly_reserve_percent": 20,
  "safe_run_budget_estimate": null,
  "confidence": "LOW|MEDIUM|HIGH",
  "notes": ""
}
```

If exact numeric usage is unavailable:
use nulls and descriptive notes.
Never fabricate percentages from nothing.

---

# 27. RUN END SUMMARY

Before ending each run:

1. commit/push safe completed work,
2. open/update PRs,
3. run required validation,
4. update task state,
5. update usage state,
6. document blockers,
7. record pending approvals,
8. record next critical task.

Summary:

CODEX RUN: DONE / PARTIAL / BLOCKED / FAILED
Time: <timestamp>
Usage status: SAFE / CAUTION / RESERVE_ONLY
Weekly reserve protected: YES / NO
Tasks completed: [...]
Tasks in review: [...]
PRs: [...]
CI: [...]
Blockers: [...]
Pending approvals: [...]
Next critical task: [...]

Keep this summary short.

---

# 28. CURRENT PROJECT EXECUTION MODE

This repository is currently Codex-only.

Do not:
- wait for Claude,
- assign Claude tasks,
- create Claude branches,
- block because Claude is unavailable.

Use independent Codex reviewer contexts for critical work.

---

# 29. CURRENT BOOTSTRAP PRIORITY

Before broad production game coding, verify/complete:

- BOOT-003 review/merge,
- repository privacy,
- branch protection/rulesets,
- machine-readable task queue,
- CI validation,
- scaffold integrity,
- Codex-only review policy,
- 6-hour automation,
- quota-aware usage control,
- research-phase launch.

---

# 30. AUTOMATION INSTRUCTION

Create a recurring Codex automation using this file as the operating policy.

Timezone:
`Africa/Cairo`

Runs:
- 00:00
- 06:00
- 12:00
- 18:00

At every trigger:

1. read project state,
2. inspect usage state,
3. calculate safe run budget,
4. protect weekly reserve,
5. execute highest-value approved work,
6. continue while budget safely allows,
7. stop before threatening future scheduled runs,
8. leave repository resumable.

This automation continues until the Human Owner pauses it or no safe approved work remains.

---

# 31. FIRST ACTION AFTER LOADING THIS FILE

1. Read source-of-truth files.
2. Inspect current PRs and bootstrap state.
3. Inspect available usage indicators.
4. Create/update `reports/usage/CODEX_USAGE_STATE.json`.
5. Calculate a conservative safe budget for the current run.
6. Complete the highest-priority bootstrap work.
7. Configure/confirm the every-6-hours automation.
8. Do not start broad production game code before gates allow it.

END.
