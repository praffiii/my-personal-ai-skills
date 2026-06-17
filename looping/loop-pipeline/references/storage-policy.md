# Storage Policy

Loop state is memory and control, not a report. Keep it private and compact by default.

## Default: Global Private State

Store loop state under:

```text
~/.claude/loop-runs/<repo-id>/<loop-id>.md
```

Use this for company repos, collaboration repos, and any repo without an explicit local convention.

Recommended repo ID:
- Prefer a stable short hash of the absolute repo root.
- Include a readable repo name prefix when convenient, e.g. `portus-a1b2c3d4`.

Recommended loop ID:
- `<YYYY-MM-DD>-<pipeline>-<short-topic>`
- Examples: `2026-06-17-feature-dark-mode`, `2026-06-17-review-pr-42`.

## Optional: Repo-Local State

Only use repo-local state when the user explicitly approves it:

```text
<repo>/.ai/loops/<loop-id>.md
```

Before using repo-local state in a shared repo, ask whether to:
- keep it untracked and add `.ai/loops/` to `.gitignore`
- use a team-approved path
- avoid repo-local state

Do not edit `.gitignore` without approval.

## What To Store

Store:
- pipeline, status, current stage, iteration count
- repo path, branch, PR/ticket/design/source pointers
- goal and acceptance criteria
- Codex job/session IDs when available
- short Claude review verdict
- short Codex review verdict
- next action and approval requirement

Do not store:
- secrets
- full transcripts
- full diffs
- full command logs
- large pasted design specs
- raw Figma data
- long Codex outputs

Use pointers to those artifacts instead.
