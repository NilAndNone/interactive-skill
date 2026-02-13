---
name: spec-align
description: Use when a request is ambiguous, high-impact, or likely to cause rework, and needs high-value clarifying questions, explicit assumptions, acceptance criteria, and phased checkpoints before implementation.
---

Run the **Spec Alignment Protocol** before coding.

## Goals
- Reduce low-value back-and-forth.
- Ask only high-information questions.
- Produce an approval-ready implementation plan.

## Rules
- Do not edit code in this skill.
- Ask at most 3 clarifying questions per round.
- Each question must include:
  1) Why it matters (risk / reversal cost)
  2) Evidence from repo or current conversation
  3) Default assumption if unanswered

## Output (strict)
1) Clarifying Questions (0-3)
2) Assumption Ledger (A1..An with reason)
3) Spec Draft
   - Goal
   - Non-goals
   - Constraints
   - Interfaces
4) Acceptance Criteria (testable)
5) Plan + Checkpoints
   - Phase 0: Recon
   - Phase 1: Implement
   - Phase 2: Verify

For each phase, include:
- Deliverable
- Likely files touched
- Commands to run (only from allowlist unless approved)
- Approval gate (what the user needs to confirm)

## Safety Defaults
- Command allowlist default: `test`, `lint`, `format`.
- Never deploy, migrate, or run destructive operations without explicit approval.
- If repo evidence is missing, ask only one most critical question and state `no repo evidence yet`.
