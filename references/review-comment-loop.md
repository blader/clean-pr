# Review Comment Loop

Use this file after the PR is open and review feedback starts arriving.

## Fast triage checklist
1. Pull current feedback from the PR.
2. For each thread, classify:
- `must-fix`: correctness, maintainability regression, missing test, broken style gate.
- `clarification`: reviewer needs rationale or location hints.
- `disagreement`: preference conflict; respond with evidence and ask for explicit direction.
3. Resolve `must-fix` first, then `clarification`, then `disagreement`.

## Suggested GitHub CLI commands
- View summary and comments:
```bash
gh pr view <pr-number> --comments
```
- View review threads via API:
```bash
gh api graphql -f query='query($owner:String!,$repo:String!,$number:Int!){repository(owner:$owner,name:$repo){pullRequest(number:$number){reviewThreads(first:100){nodes{isResolved comments(first:20){nodes{author{login} body path outdated}}}}}}}' -F owner=<owner> -F repo=<repo> -F number=<pr-number>
```

If `gh` is unavailable, use the web UI and continue the same triage flow.

## Response pattern per addressed comment
Use short, concrete replies:
- What changed.
- Where it changed (file/path).
- What verification was run.
- Keep replies scoped to changes visible in the BASE MERGE-to-PR diff; avoid commit-by-commit framing.

Example:
`Updated null-handling in parser init at webapp/src/parser.ts and added regression test in webapp/src/parser.test.ts. Ran pnpm test parser + pnpm lint.`

## Iteration loop
1. Batch related fixes into one push when practical.
2. Re-run affected formatting (Prettier or repo formatter), lint, and tests before pushing.
3. Push and respond on each resolved thread.
4. Re-check for new comments.
5. Exit only when no unresolved threads remain or user asks to stop.
