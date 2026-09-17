# PERMISSIONS.md — Agent Permission & Ownership Policy
Version: 0.1-bootstrap
Authority: MASTER.md

## 1. Principle

Default permission is DENY.

Agents receive only the minimum permissions required for their task.

No agent owns the whole repository by default.

---

## 2. Protected files

The following are protected source-of-truth files:

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

During DESIGN mode:
authorized planning tasks may modify approved spec files.

After SPEC FREEZE:
all builder agents receive READ ONLY access to frozen source-of-truth files.

Changes require CHANGE_REQUEST approval.

---

## 3. Protected branches

`main`
`integration`

Default autonomous worker permission:

READ: yes
DIRECT PUSH: no

Workers must use isolated branches/worktrees.

---

## 4. Default agent permissions

### Codex worker

Allowed:
- read task-relevant files
- create `agent/codex/<TASK-ID>`
- modify approved task paths
- run local tests
- push own branch
- open PR

Denied by default:
- main/integration direct push
- secrets
- billing
- production deploy
- destructive database operation
- external tool install
- frozen spec mutation

### Claude worker

Allowed:
- read task-relevant files
- create `agent/claude/<TASK-ID>`
- modify approved task paths
- run local tests
- push own branch
- open PR

Denied by default:
- main/integration direct push
- secrets
- billing
- production deploy
- destructive database operation
- external tool install
- frozen spec mutation

---

## 5. Path ownership

Tasks must define their own allowed read/write paths.

Example:

Task: UX-021
WRITE:
- /src/client/squad/**
- /tests/client/squad/**

READ:
- /DESIGN.md
- /specs/ux/squad/**
- /API_CONTRACTS.md
- /src/client/shared/**

Everything else:
DENY WRITE

---

## 6. Shared path locking

High-conflict paths may be temporarily locked.

Examples:
/src/shared/**
/src/types/**
/src/database/migrations/**
/src/config/**
/package.json
/package-lock.json
/pnpm-lock.yaml

Editing a locked/shared path requires:
- explicit task permission
- ownership check
- conflict check

---

## 7. Dependency permission

Adding or upgrading a dependency requires explicit permission if it:

- changes lockfiles
- adds native binaries
- adds network access
- requires secrets
- adds paid service dependency
- changes build tooling
- changes runtime architecture

Small already-approved dependency changes may be permitted by task contract.

---

## 8. Skill / MCP permission

Discovery:
allowed only for tasks with discovery permission.

Installation:
requires recorded human approval.

Every approved external skill/tool must be registered.

---

## 9. Network access

Default:
restricted.

Allowed when task requires:
- research
- approved package registry
- approved docs
- approved API
- approved skill discovery

Prefer allowlisted domains.

Do not upload repository contents to external services without approval.

---

## 10. Secret access

Secrets are granted per task.

Never:
- print secrets
- commit secrets
- copy secrets into logs
- expose secrets to unrelated tools
- persist credentials in task artifacts

---

## 11. Destructive operations

Always require explicit human approval:

- delete production data
- force push protected branches
- rotate/remove credentials
- drop databases/tables
- irreversible migrations
- production deploy with destructive changes
- delete repositories/resources

---

## 12. Paid services

Agents may recommend paid services.

They may NOT:
- subscribe,
- purchase,
- activate billing,
- increase spend limits

without explicit human approval.

---

## 13. Legal / licensing

Agents may research licensing.

They may NOT:
- agree to licenses
- accept contractual terms
- purchase commercial rights
- represent the owner legally

without human approval.

---

## 14. Production deploy

Production release requires:
- release task
- release QA
- security checks
- integration green
- human approval

No autonomous production deploy during bootstrap/design.

---

## 15. Violation handling

If a task requires forbidden permission:

1. stop before action
2. report BLOCKED_PERMISSION
3. specify exact permission needed
4. explain why
5. wait for approval

Never work around permission controls.
