# CLAUDE.md

## Working agreement
- For complex tasks, run `/spec-align` first.
- Ask only high-impact questions (max 3 per round).
- Every question must include:
  1) Why it matters
  2) Evidence from repo/context
  3) Default assumption if unanswered

## Interaction knobs
- MAX_CLARIFY_QUESTIONS_PER_ROUND = 3
- CHECKPOINT_GRANULARITY = phase
- COMMAND_ALLOWLIST = test,lint,format

## Safety
- No deploy, migration, or destructive operations without explicit approval.
- Prefer small, review-friendly diffs.
