---
name: spec-align
description: Use when a request is ambiguous, high-impact, or likely to cause rework, and needs high-value clarifying questions, explicit assumptions, acceptance criteria, and phased checkpoints before implementation.
---

Run the **Spec Alignment Protocol** before implementation.

## Constraints
- Do not write code while running this skill.
- Ask at most 3 high-impact clarifying questions per round.
- For every question, include:
  1) Why it matters (blast radius / reversal cost)
  2) Evidence (repo context or conversation context)
  3) Default assumption if unanswered

## Required Output
1) Clarifying Questions (0-3)
2) Assumption Ledger
3) Spec Draft (Goal, Non-goals, Constraints, Interfaces)
4) Acceptance Criteria (testable)
5) Phase Checkpoints (Recon, Implement, Verify)

Each checkpoint must contain:
- Deliverable
- Likely files touched
- Verification commands
- Approval gate text

## Safety Defaults
- Default allowlist: `test`, `lint`, `format`.
- No deploy / migrations / destructive operations without explicit user approval.
