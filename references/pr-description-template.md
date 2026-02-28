# PR Description Template

Use this template when updating or creating the PR.
Write for someone who is reviewing quickly: clear, direct, and easy to trust.

Rules:
- Run `schematic` first and use its output to draft the PR narrative backbone (problem, approach, change themes, risks).
- Base every claim only on the cumulative diff from BASE MERGE to PR head.
- If `schematic` output and the cumulative diff disagree, follow the cumulative diff.
- Exception: testing/validation evidence may also come from session history and PR comment/commit history (for example CI/check outputs tied to PR commits).
- Use those extra sources only in testing/validation sections, not in problem statement, scope, or change-summary sections.
- Do not mention the skill, pass numbers, or internal workflow steps.
- Do not use commit-by-commit narration unless explicitly requested.
- Include only sections that are relevant to this diff.
- Delete sections that do not apply; do not leave empty headings.

Recommended minimum:
- Problem statement and goal
- Fix summary
- High-level changes with reasoning
- Risk/tradeoff callouts surfaced from `schematic` when materially relevant

## Problem statement and goal (recommended)
- Original issue (must exist on base branch `latest` before this PR; not introduced by this PR):
- User/system impact:
- Goal of this PR:
- Non-goals (explicitly out of scope):

## Fix summary (recommended)
- How this PR fixes the issue:
- Why this approach is correct:
- Behavior compatibility guarantees:

## High-level changes with reasoning (recommended)
- Change area 1:
  - What changed:
  - Reasoning:
- Change area 2:
  - What changed:
  - Reasoning:
- Change area 3:
  - What changed:
  - Reasoning:

## Diff composition (%) (optional, include when composition is useful to reviewers)
- Logic/code-path changes: __%
- Tests: __%
- Comments/documentation: __%
- Total: 100%
- Estimation method:
  - Scope measured only from BASE MERGE to PR head.

## Benchmark, testing, and validation results (optional, include when validation signal matters)
When using evidence from session history or PR comment/commit history, label source and timestamp clearly.

Minimum detail checklist (include what applies):
- Procedure scope/hypothesis:
- Comparison point:
  - Baseline ref/SHA:
  - PR head ref/SHA:
- Environment:
  - OS/runner:
  - Runtime/toolchain versions:
  - Relevant env flags/config:
- Inputs:
  - Dataset/fixtures:
  - Seed/setup/migration steps:
- Pass/fail criteria:
  - Required threshold or invariant:

- Functional validation:
  - Command(s):
  - Assertion(s) checked:
  - Result:
  - Evidence source (local run / CI link / session note):
- Benchmark/performance checks:
  - Scenario and workload:
  - Command(s):
  - Runs/warmup:
  - Baseline metric(s):
  - PR metric(s):
  - Delta:
  - Variance/noise note:
  - Pass/fail vs threshold:
- Regression and safety checks:
  - Command(s):
  - What risk this check covers:
  - Result:
  - Evidence source:

Reproducibility note:
- Exact command block to re-run:
- Known limitations/caveats of these results:

## Test coverage changes (optional, include when tests changed or notable gaps remain)
- New tests:
- Updated tests:
- Behaviors covered:
- Not covered (and why):

## Lint/format checks (optional, include when checks were run or requested by team norms)
- Lint:
  - Command:
  - Result:
- Formatting (prettier or equivalent):
  - Command:
  - Result:

When code files changed, include both lint and formatting entries unless they were intentionally skipped (and explain why).

## Reviewer guide (optional, include for large or high-risk diffs)
- High-signal files to read first:
- Invariants to verify:
- Areas intentionally not changed:

## Risk assessment (optional, include when risk is non-trivial)
- Functional risk:
- Operational risk:
- Rollback plan:

## Follow-ups (optional)
- Deferred cleanup:
- Future tests:
