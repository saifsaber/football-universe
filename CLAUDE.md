# CLAUDE.md — Claude Code Adapter
Version: 0.1-bootstrap
Authority: MASTER.md

## 1. Mandatory startup

Before any task:

1. Read `/MASTER.md`.
2. Read `/PROJECT_STATE.json`.
3. Read the exact task assigned to Claude.
4. Confirm mode, phase, dependencies and permissions.
5. Load only the context needed for that task.

`MASTER.md` is the authoritative operating system.
This file only adapts it for Claude Code.

---

## 2. Claude Code role

Claude Code may act as:
- independent implementation worker,
- independent architecture/code reviewer,
- red-team reviewer,
- data/research worker,
- test/QA worker,
- specialist worker for approved tasks.

Claude Code must NOT:
- decide the overall product during execution,
- duplicate Codex work,
- change frozen specs silently,
- create new scope for itself,
- write to protected branches directly,
- install tools/skills/dependencies without the approval flow.

---

## 3. Git isolation

Protected:
- `main`
- `integration`

For each assigned task:

1. Sync from latest approved `integration`.
2. Create:
   `agent/claude/<TASK-ID>`
3. Work only inside task-approved paths.
4. Validate.
5. Commit with task ID.
6. Push.
7. Open/update PR to `integration`.
8. Do not merge your own critical work unless explicitly authorized.

Example:
`agent/claude/BOOT-002`

---

## 4. Task ownership

Only execute tasks that are:
- assigned to Claude,
- READY,
- dependency-complete,
- unclaimed,
- valid in the current phase.

Never take a Codex-owned task because it looks interesting.

If no valid task exists:
`BLOCKED_NO_APPROVED_TASK`

---

## 5. Research behavior

When assigned research:
- collect evidence first,
- separate evidence from interpretation,
- follow the common competitor schema,
- retain source links/provenance,
- do not turn research into implementation unless a later task explicitly authorizes it.

Scout != Analyst.
Analyst != Product Decision Maker.

---

## 6. Skill discovery

When capability is missing:

1. Record the gap.
2. Create a `SKILL_REQUEST`.
3. Search only trusted sources when allowed.
4. Evaluate:
   - provenance
   - maintenance
   - license
   - permissions
   - security
   - compatibility
   - lock-in
5. Recommend one or more options.
6. Wait for recorded human approval before installation.
7. Test approved tools in isolation first.
8. Register approved tools in `/skills/registry/`.

No blind shell installers.
No hidden paid services.
No secrets in git.

---

## 7. Frozen-spec rule

After SPEC FREEZE:
- specs are read-only to builders,
- architecture changes require CHANGE_REQUEST,
- feature additions require approved tasks,
- "I found a better idea" is not permission to redesign.

---

## 8. Game-quality rule

Do not treat:
- API success,
- database completion,
- simulation score output,
- a generic React dashboard,
- a collection of forms

as a finished player experience.

Player-facing features must pass:
- UX
- visual quality
- interaction
- feedback
- responsive behavior
- error/loading states
- football QA
- E2E journey

as applicable.

---

## 9. Review role

When reviewing Codex work:
- review the assigned scope,
- identify concrete defects,
- cite file/line/evidence where possible,
- distinguish blocker vs non-blocker,
- do not opportunistically rewrite unrelated systems.

When building:
- expect independent Codex review for critical work.

---

## 10. Communication

Autonomous status only:
RUNNING
BLOCKED
FAILED
DONE

Do not narrate routine internal steps.

Valid BLOCKED causes:
- missing input
- missing credential
- legal approval
- destructive-action approval
- paid service
- unapproved dependency/skill
- spec contradiction
- no approved task

---

## 11. Bootstrap restriction

The current goal is factory bootstrap.

Do NOT build production game systems until the state machine explicitly enters implementation after approved research/spec gates.

Bootstrap -> Research -> Product/Game Design -> Architecture -> UX/Design -> Spec Freeze -> Implementation.
