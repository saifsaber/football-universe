# AGENTS.md — Codex Adapter
Version: 0.1-bootstrap
Authority: MASTER.md

## 1. Mandatory startup

Before doing any work:

1. Read `/MASTER.md`.
2. Read `/PROJECT_STATE.json`.
3. Confirm current project mode and phase.
4. Read only the task files assigned to Codex.
5. Check the task's allowed read/write paths.
6. Check dependencies and required skills.
7. Do not start production implementation if the project is still in BOOTSTRAP / DESIGN mode.

`MASTER.md` is authoritative.  
This file adapts the master operating system for Codex; it does not override it.

---

## 2. Codex role

### Human Owner operating-policy adoption (2026-09-17)

For scheduled work, read `CODEX_AUTONOMOUS_6H_BUDGETED.md` (version 1.1), adopted by the Human Owner. It supplements this adapter and preserves MASTER.md as the highest repository authority. Current execution is Codex-only: use a fresh independent Codex reviewer for critical work instead of the historical preferred Claude review below. Do not assign Claude work or block merely because Claude is unavailable. Other approval, task, phase, and merge gates remain applicable; do not silently change MASTER.md or PROJECT_STATE.json to resolve policy conflicts.

Run at 00:00, 06:00, 12:00, and 18:00 Africa/Cairo. Inspect fresh usage before substantive work; preserve the weekly reserve and record observations in `reports/usage/CODEX_USAGE_STATE.json` on an authorized task branch, or an approved local equivalent. Unknown limits remain null. The quota rules are agent stop rules, not a runtime-enforced spending cap. Follow the owner-approved policy from the adoption branch until its PR is merged, then use integration.

Codex acts as:
- integration lead when explicitly assigned,
- implementation worker for tasks labeled `agent:codex`,
- reviewer for Claude-built work when assigned,
- automation worker for scheduled/event-driven engineering tasks,
- bootstrap worker during repository setup.

Codex is NOT allowed to:
- redesign the product during implementation,
- change frozen specs without a CHANGE_REQUEST,
- claim Claude-assigned tasks,
- write directly to protected branches,
- invent new product features,
- silently install unapproved skills or dependencies.

---

## 3. Git rules

Protected branches:
- `main`
- `integration`

Never implement directly on those branches.

For every assigned task:

1. Start from the latest approved `integration`.
2. Create an isolated branch/worktree:
   `agent/codex/<TASK-ID>`
3. Modify only task-approved paths.
4. Run required validation.
5. Commit with the task ID.
6. Push the branch.
7. Open/update a PR into `integration`.
8. Do not merge your own critical PR unless the task explicitly grants integration authority.

Example:
`agent/codex/BOOT-001`

---

## 4. Task claiming

Only claim work that satisfies ALL conditions:
- assigned to Codex,
- status is READY,
- dependencies are complete,
- no other worker has claimed it,
- current project phase allows it.

If no valid task exists:
- do not invent work,
- report `BLOCKED_NO_APPROVED_TASK`,
- stop.

---

## 5. Context discipline

Load the minimum context required.

Do not read the entire repository by default.

Typical UI task context:
- relevant task contract
- `DESIGN.md`
- exact UX spec
- relevant API contract
- relevant existing components

Typical simulation task context:
- task contract
- simulation spec section
- relevant schemas
- calibration data
- tests

---

## 6. Skill / tool discovery

If required capability is missing:

1. Do not improvise a weak substitute.
2. Create a `SKILL_REQUEST`.
3. Search trusted sources only when the task allows web/tool discovery.
4. Record:
   - skill/tool name
   - source
   - exact version or commit
   - purpose
   - permissions
   - security concerns
   - alternatives
5. Do not install until human approval is recorded.
6. After approval:
   - install in sandbox/isolated environment first,
   - validate compatibility,
   - register it under `/skills/registry/`,
   - resume the original task.

Never use blind `curl | bash`.
Never expose secrets.

---

## 7. Change control

If approved architecture/spec is wrong:

Do not silently fix it.

Create a CHANGE_REQUEST containing:
- ID
- affected spec
- evidence
- problem
- impact
- proposed fix
- blocking yes/no

Continue unrelated safe work if possible.

---

## 8. Player-facing quality rule

Never substitute gameplay with:
- raw tables,
- JSON,
- default browser controls,
- admin forms,
- debug panels,
- generic dashboard cards.

A working API or simulation is not a finished game feature.

For every player-facing feature, satisfy the applicable Player Experience Gate in `MASTER.md`.

---

## 9. Review policy

For critical work:
- builder != reviewer whenever practical.

Preferred:
- Codex build -> Claude review
- Claude build -> Codex review

Review findings become explicit tasks or PR comments.
Do not rewrite unrelated areas during review.

---

## 10. Status output

During autonomous work use only:
- RUNNING
- BLOCKED
- FAILED
- DONE

Do not send conversational progress chatter.

Valid blocking reasons include:
- missing required file
- credential required
- legal approval required
- paid-service approval required
- destructive action approval required
- unapproved skill/dependency required
- frozen-spec contradiction
- no approved task

---

## 11. Bootstrap restriction

Current bootstrap objective is to build the factory, not the game.

Until `PROJECT_STATE.json` advances beyond BOOTSTRAP/DESIGN:
- do not build production game features,
- do not create speculative frontend/backend systems,
- do not start the football simulation engine.

Bootstrap first.
Research second.
Spec freeze later.
Implementation after approval.
