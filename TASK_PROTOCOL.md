# TASK_PROTOCOL.md — Multi-Agent Task Execution Protocol
Version: 0.1-bootstrap
Authority: MASTER.md

## 1. Purpose

This protocol defines exactly how work is created, assigned, claimed, executed, reviewed, merged, blocked, retried, and completed across Codex and Claude Code.

Agents do not choose arbitrary work.
Agents do not duplicate active work.
Agents do not silently expand scope.

---

## 2. Task lifecycle

Every task moves through this state machine:

PROPOSED
→ APPROVED
→ READY
→ CLAIMED
→ RUNNING
→ REVIEW
→ VALIDATION
→ DONE

Possible exception states:

BLOCKED
FAILED
CANCELLED
SUPERSEDED

No task may skip directly from READY to DONE.

---

## 3. Task identity

Every task must have a unique ID.

Recommended prefixes:

BOOT-###  Bootstrap / studio setup
RES-###   Research
PROD-###  Product
GAME-###  Game design
DATA-###  Football data
SIM-###   Simulation
UX-###    UX / UI
FE-###    Game client / frontend
BE-###    Backend
INFRA-### Infrastructure
SOC-###   Social / multiplayer
LIVE-###  Live football
QA-###    Quality
SEC-###   Security
AN-###    Analytics
SKILL-### Skill acquisition
CR-###    Change request

Example:
`BOOT-001`

---

## 4. Task contract

Each task must specify:

- task_id
- title
- status
- priority
- assigned_agent
- assigned_model_tier
- objective
- phase
- dependencies
- required_inputs
- allowed_read_paths
- allowed_write_paths
- forbidden_actions
- required_tools
- required_skills
- validation_commands
- review_required
- reviewer
- done_when
- block_conditions

Tasks missing required fields are INVALID.

---

## 5. Assignment policy

Valid workers:
- codex
- claude
- human
- unassigned

An autonomous worker may only claim a task when:

1. `status == READY`
2. `assigned_agent` matches that worker
3. all dependencies are DONE
4. the task has not been claimed by another worker
5. project phase allows the task
6. required inputs exist
7. required approved skills are available

If any condition fails:
do not start.

---

## 6. Claiming

When an agent claims a task:

1. mark state as CLAIMED
2. record:
   - agent
   - timestamp
   - base branch
   - work branch
3. create isolated branch/worktree
4. move to RUNNING only after environment validation

Branch naming:

Codex:
`agent/codex/<TASK-ID>`

Claude:
`agent/claude/<TASK-ID>`

---

## 7. Execution rules

During RUNNING:

- work only on objective
- use only allowed write paths
- do not modify frozen specs
- do not add unrelated refactors
- do not add dependencies without approval
- do not install unapproved skills
- do not modify another active agent's owned paths
- do not create speculative features
- keep tests close to implementation

If a hidden dependency is discovered:
BLOCK or create a TASK_PROPOSAL.

Do not silently expand scope.

---

## 8. Commit policy

Every commit must include task ID.

Examples:

`BOOT-001 create task schemas`
`UX-014 implement squad drag interaction`
`SIM-008 add deterministic replay test`

Avoid meaningless messages such as:
- update
- fix stuff
- changes

---

## 9. Review policy

Critical tasks require independent review.

Preferred:
- Codex implementation → Claude review
- Claude implementation → Codex review

Reviewer checks only:
- task correctness
- spec compliance
- security
- regressions
- scope discipline
- quality gates

Reviewer must classify findings:

BLOCKER
MAJOR
MINOR
NOTE

Only BLOCKER or MAJOR findings prevent merge unless the task says otherwise.

---

## 10. Validation

A task enters VALIDATION after review approval.

Validation may include:

- unit tests
- integration tests
- E2E
- schema validation
- lint
- type checking
- visual regression
- screenshot gate
- simulation calibration
- football QA
- performance tests
- security tests

All task-required validators must pass.

---

## 11. Completion

Task becomes DONE only when:

- objective completed
- review passed if required
- validation passed
- no forbidden paths changed
- PR merged into integration where applicable
- state updated
- outputs documented

"DONE" means complete, not "mostly complete".

---

## 12. Blocked tasks

Valid block reasons:

- missing_input
- missing_credential
- dependency_not_done
- required_skill_not_approved
- paid_service_approval_required
- legal_approval_required
- destructive_change_approval_required
- frozen_spec_conflict
- external_service_unavailable
- merge_conflict_requires_resolution
- security_risk
- no_valid_task

Every BLOCKED state must contain:
- reason
- evidence
- required unblock action
- owner of unblock action

---

## 13. Failed tasks

FAILED means execution was attempted and could not meet task requirements.

A failed task must record:
- what failed
- commands/tests
- logs or evidence
- files changed
- whether rollback occurred
- recommended retry path

Never hide failure by marking DONE.

---

## 14. Retry policy

Retries must not endlessly repeat the same failed approach.

Retry 1:
- fix direct error

Retry 2:
- reassess local implementation approach

Retry 3:
- escalate to reviewer / create TASK_PROPOSAL / CHANGE_REQUEST

After repeated failure:
BLOCK instead of looping.

---

## 15. Task proposals

Execution agents may propose work using TASK_PROPOSAL.

Required fields:
- proposed_id
- discovered_during
- problem
- evidence
- suggested_task
- urgency
- blocking
- expected_owner

A proposal is not executable until approved.

---

## 16. Merge ownership

Normal worker:
- opens PR
- does not directly merge critical work

Integration Agent:
- checks CI
- checks review
- checks conflicts
- merges to `integration`

Human or authorized Release Agent:
- approves promotion from `integration` to `main`

---

## 17. Conflict handling

If two branches touch the same logical ownership area:

1. stop automatic merge
2. identify owning task
3. keep earlier claimed task authoritative unless superseded
4. create explicit conflict-resolution task
5. rebase/reapply only after review

Never let agents "solve" conflicts by deleting unfamiliar code.

---

## 18. Event-driven operation

Preferred triggers:

task READY → assigned worker starts
PR opened → reviewer starts
review passed → validation starts
validation passed → integration starts
merge completed → dependent tasks become READY

Scheduled heartbeat is fallback only.

---

## 19. Heartbeat behavior

Every recurring heartbeat:

1. read MASTER.md
2. read PROJECT_STATE.json
3. inspect READY tasks
4. inspect stale RUNNING tasks
5. inspect failed CI
6. inspect open reviews
7. inspect merge conflicts
8. resume only approved work
9. never duplicate active work
10. never redesign product

---

## 20. Bootstrap restriction

Until bootstrap is completed:
- no production football game implementation
- no simulation core implementation
- no speculative UI implementation

Bootstrap the factory first.
