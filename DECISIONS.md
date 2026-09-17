# DECISIONS.md
Version: 0.1-bootstrap

## D-001 — Multi-agent studio
Use a controlled multi-agent operating model with Codex and Claude Code sharing one repository through isolated branches/worktrees and PR review.

## D-002 — Source of truth
`MASTER.md` is authoritative during bootstrap. Frozen specs become authoritative after SPEC FREEZE.

## D-003 — Integration flow
Workers do not push directly to `main` or `integration`; work lands through PRs and validation.

## D-004 — Skill acquisition
Missing skills/tools are discovered, audited, sandbox-tested, and installed only after explicit human approval.

## D-005 — Vertical slice first
The first implementation milestone must prove an end-to-end playable vertical slice before broad feature expansion.

## D-006 — Simulation boundary
LLMs may narrate/explain grounded outcomes; they do not decide match winners or fabricate football facts.

## D-007 — Current mode
Project remains in DESIGN / BOOTSTRAP. No production game implementation is authorized yet.
