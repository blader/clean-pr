---
name: clean-pr
description: Pull request communication workflow focused on writing strong PR descriptions and driving code review comments to closure.
---

# Clean PR

Use this skill when the task is PR communication: write a PR description people can understand quickly, then close review comments with clear follow-through.

## Writing style target
- Sound like a strong teammate, not a template engine.
- Prioritize clarity over exhaustiveness. Include detail when it changes reviewer decisions.
- Write in plain, direct language that a new engineer can follow in one pass.
- Keep the tone professional but approachable.
- Tell a readable story: what was wrong, what changed, and why this is better now.
- Prefer natural transitions and short paragraphs over clipped, mechanical bullet dumps.
- Make the text pleasant to read without sacrificing technical precision.

## Non-negotiables
- Write for a busy reviewer: plain language, clear structure, and practical detail.
- Keep claims concrete and grounded in the actual diff.
- Explain intent, tradeoffs, and impact without noise.
- Make the narrative easy to scan: short paragraphs, useful headings, minimal filler.
- Prefer active voice and concrete verbs (`added`, `removed`, `fixed`, `kept`) over abstract phrasing.
- Avoid robotic wording and repetitive scaffolding (e.g., repeated "this PR" lead-ins).
- Resolve comments explicitly so reviewers never have to guess what changed.
- State uncertainty directly; do not speculate.
- Run `schematic` before drafting or updating PR description content.
- Use `schematic` as a synthesis aid (problem framing, solution framing, risks, rollout), but treat the BASE MERGE-to-head diff as final source of truth for PR claims.
- In PR description content, avoid local logistics: no local command snippets, local file-path callouts, local plan references, or internal scratch-notes.
- Push all intended local PR changes (staged and unstaged tracked edits) before writing PR text or handling review comments.
- Base PR content only on the aggregate diff from BASE MERGE (merge base with PR base branch) to PR head.
- Exception: for testing/validation evidence only, you may use session history and PR comment/commit history (including CI/check results tied to PR commits).
- Do not use session history or PR comment/commit history as sources for problem statement, scope, or change-summary claims.
- In PR descriptions, include validation only when there is concrete smoke/integration/e2e evidence that actually ran.
- Do not include routine lint, formatting, or unit-test output as PR validation evidence.
- When present, make smoke/integration/e2e validation sections procedure-driven: include context, high-level test procedure, baseline/comparison point (when relevant), pass criteria, and observed results.
- Do not run smoke/integration checks as part of this skill.
- Use existing evidence only (session history, CI/check results, and PR comment/commit history). If none exists, omit validation sections.
- Avoid commit-by-commit storytelling.
- Always run Prettier on all changed files before committing/pushing PR updates and before concluding this workflow. If Prettier reports issues, fix them and re-run until clean.

## Workflow

### 0) Run schematic first
1. Run `schematic` against the PR base branch and current head to generate/update the branch spec.
2. Extract draft inputs for PR writing: problem statement, solution approach, major change themes, testing/rollout notes, and risks.
3. If `schematic` output conflicts with the BASE MERGE-to-head diff, correct the notes and follow the diff.
4. Use the spec as drafting input only; do not paste full spec sections/tables into the PR description.

### 1) Push local changes first
1. Identify the PR head branch and switch to it (or a branch that pushes to that head).
2. Check local staged and unstaged tracked changes.
3. Run Prettier on all changed files and ensure the check passes.
4. Commit all intended PR changes locally (squash only if requested).
5. Push to the PR head branch.
6. Confirm remote head SHA is updated before continuing.

### 2) Define PR scope from merge base
1. Compute BASE MERGE against the PR base branch.
2. Read only the aggregate diff from BASE MERGE to PR head.
3. Build the PR narrative from that aggregate diff only.
4. Describe the original issue as pre-existing on base (`latest`), then state goal and non-goals.
5. Group changes into clear themes that are easy to scan.
6. Cross-check those themes against the `schematic` output to ensure nothing reviewer-relevant is missing.

### 3) Write or update the PR description
1. Confirm remote head is up to date (from Step 1).
2. Create or update the PR.
3. Draft or update the PR description with `references/pr-description-template.md`.
4. Keep the description issue-first and solution-first:
   - Use `schematic` outputs as narrative scaffolding, then verify each claim against the BASE MERGE-to-PR diff.
   - Treat the BASE MERGE-to-PR diff as the only source of truth for every claim in the PR title/body/content.
   - Validation/testing sections may use evidence from session history and PR comment/commit history.
   - Describe the original issue as pre-existing on base branch, not introduced by this PR.
   - Explain issue, impact, goal, and non-goals in plain language.
   - Explain how the changes address the issue and why this approach was chosen.
   - Summarize high-level change groups with reasoning.
   - Keep discussion at concept/theme level; avoid file-by-file narration.
   - Quantify diff composition as percentages: code vs comments/documentation (sum = 100%).
   - Include a validation section only if smoke/integration/e2e evidence exists; otherwise omit validation sections entirely.
   - Never pad PR validation with lint/prettier/unit-test-only output.
   - In validation writeups, focus on what was tested and what happened; avoid command transcripts and local-path details.
   - Call out reviewer-relevant risks, caveats, and follow-ups.
5. Style pass before publishing:
   - Tighten phrasing: remove repetition, filler, and "status report" voice.
   - Replace jargon with concrete meaning where possible.
   - Make the prose feel human and easy to follow, not terse or robotic.
   - Ensure a reviewer can answer: What changed? Why this approach? How was it validated? What could still go wrong?
   - Keep what matters; trim what does not affect review decisions.
6. Template usage rule: include only sections that fit the actual diff; omit sections that are not relevant.
7. Do not mention the skill, pass numbers, or internal workflow mechanics.

### 4) Review-comment closure loop
1. Fetch review comments.
2. Classify each as `must-fix`, `clarification`, or `disagreement`.
3. Implement must-fix items with minimal additional churn.
4. Do not run smoke/integration checks; reuse existing valid evidence when needed for reviewer communication.
5. Run Prettier on all changed files and ensure the check passes.
6. Push updates as needed.
7. Reply to each addressed comment with exactly what changed and where.
8. Repeat until no unresolved comments remain or user says stop.

Use `references/review-comment-loop.md` for triage and response patterns.

## Output contract
Always include:
1. PR description highlights:
   - Original issue (pre-existing on base), goal, and fix summary.
   - How `schematic` findings were incorporated into the PR narrative.
   - High-level changes with reasoning.
   - Code vs comments/documentation percentages.
   - If smoke/integration/e2e evidence exists: validation summary with test context, high-level procedure, comparison point (if relevant), and specific measured outcomes.
   - If no qualifying smoke/integration/e2e evidence exists: explicit statement that validation section was intentionally omitted.
   - Any notable reviewer-facing risks, tradeoffs, or caveats.
2. Review-comment status:
   - What was addressed.
   - Any open items or disagreements still pending.
