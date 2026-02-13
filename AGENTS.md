# AGENTS.md

## Working agreement (must follow)
- Use `spec-align` first for any non-trivial engineering task.
- Do not modify code until:
  1) critical clarifying questions are answered, or
  2) assumptions and implementation plan are explicitly approved.
- Every checkpoint output must include:
  - What changed
  - Files touched
  - Commands run + result
  - Risks / tradeoffs
  - Next step + approval needed

## Interaction knobs
- MAX_CLARIFY_QUESTIONS_PER_ROUND = 3
- CHECKPOINT_GRANULARITY = phase
- COMMAND_ALLOWLIST = test,lint,format

## Safety
- Never read secrets (`.env`, credentials) unless explicitly required and approved.
- Never deploy, migrate data, or rotate keys automatically.
- Prefer small and review-friendly diffs.
