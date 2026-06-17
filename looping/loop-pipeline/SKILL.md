---
name: loop-pipeline
description: Use when the user asks to run, continue, design, or formalize a manual loop/pipeline workflow with Claude as orchestrator/reviewer and Codex as executor/independent reviewer. Triggers include loop engineering, pipeline design system, feature pipeline, PR review loop, dual-review PR review, fix loop, refactor loop, Linear/GitHub/Figma/direct-prompt feature work, or continuing a previous loop from compact state.
---

# Loop Pipeline

Run manual human-in-the-loop pipelines for Claude Code + Codex workflows.

Core roles:
- Claude: orchestrator, first reviewer, final judge.
- Codex: executor and independent second reviewer.
- User: product/quality validator and approval gate.
- State file: compact private checkpoint outside chat context.

## Start Here

1. Identify the pipeline:
   - Feature work: read `references/pipelines/feature-development.md`.
   - PR or branch review: read `references/pipelines/review-pr.md`.
   - Bug/test/regression/follow-up fix: read `references/pipelines/fix-loop.md`.
   - Behavior-preserving cleanup/refactor: read `references/pipelines/refactor-loop.md`.
2. Read `references/stage-contract.md` before executing a pipeline.
3. Read `references/storage-policy.md` before creating or updating state.
4. If the user asks to continue a prior loop, load the matching state first, then read only the referenced pipeline.

## Operating Rules

- Keep global context small. Load only the selected pipeline reference and any state file needed for the current run.
- Default state storage is private: `~/.claude/loop-runs/<repo-id>/<loop-id>.md`.
- Do not create repo-local `.ai/loops/` files unless the user explicitly approves for that repo.
- Keep state compact: store decisions, current stage, iteration count, job/session IDs, brief summaries, and pointers. Do not paste full diffs, transcripts, Figma dumps, or long command outputs.
- Respect the global delegation rule: before source-code edits are delegated or made, ask the user for approval when required by `~/.claude/CLAUDE.md`.
- Use Codex for execution via the installed Codex plugin when available. Use Codex review/adversarial review as the independent second reviewer in review gates.
- Claude must review Codex output before treating work as done. Do not blindly accept Codex implementation or review findings.
- Stop when the loop reaches done, blocked, max iterations, missing approvals, or unclear requirements that need the user.

## State Lookup

When continuing:
1. If the user provides a loop ID or path, load it.
2. Else compute the current repo identity and inspect `~/.claude/loop-runs/<repo-id>/` for active loops.
3. If exactly one active loop exists for the repo, load it.
4. If several active loops exist, list concise choices and ask which one.
5. If no state exists, start a new loop from the selected pipeline.

## Minimal Loop State Shape

Use Markdown with a small YAML-ish header and short sections:

```md
# Loop State: <loop-id>

pipeline: feature-development
status: claude-review
repo: /absolute/path
branch: feature/example
iteration: 1/3
last_codex_job: task-...
last_codex_session: optional

## Goal
One concise paragraph.

## Acceptance Criteria
- ...

## Current Decision
What Claude concluded and what is needed next.

## Next Action
One concrete next action and whether user approval is required.
```

## Output Style

For active loop runs, report:
- pipeline and current stage
- what was inspected or delegated
- current verdict
- next action and required approval

Avoid long process narration unless the user asks for a full audit.
