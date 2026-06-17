# Looping Skills

Skills for manual loop engineering workflows.

## Included

- `loop-pipeline`: feature development, dual-review PR review, fix loop, and refactor loop pipelines.

## Prerequisite

Install the official Claude Code Codex plugin before using `loop-pipeline`:
[openai/codex-plugin-cc](https://github.com/openai/codex-plugin-cc).

## Install

From the repo root:

```bash
cp -R looping/loop-pipeline ~/.claude/skills/
```

Restart Claude Code or reload skills after copying.

## How To Use

In Claude Code, call the skill with `/loop-pipeline`:

```text
/loop-pipeline run feature-development for add dark mode to this app
```

```text
/loop-pipeline review this PR with dual review
```

```text
/loop-pipeline start fix-loop for the failing tests
```

```text
/loop-pipeline run refactor-loop for auth service cleanup
```

You can also use natural language:

```text
Use loop-pipeline to continue the latest loop for this repo.
```

## Pipelines

### Feature Development

Use when building a feature from a direct prompt, Linear ticket, GitHub issue, Figma design, README/spec, TODO, or solo project idea.

```text
/loop-pipeline run feature-development for Linear ABC-123
```

Claude clarifies scope with you, creates a Codex-ready implementation brief, asks for approval, delegates implementation to Codex, reviews the result, and loops if fixes are needed.

### Review PR

Use when reviewing a PR, branch, or working tree.

```text
/loop-pipeline review PR 42 with dual review
```

Claude reviews first. Codex reviews independently second. Claude compares both review streams, decides which findings are real, asks which fixes you approve, and delegates approved fixes to Codex.

### Fix Loop

Use for bugs, failing tests, regressions, CI failures, review findings, or follow-up fixes.

```text
/loop-pipeline start fix-loop for npm test failing on auth.spec.ts
```

Claude grounds the failure, writes the smallest safe fix brief, asks for approval, delegates to Codex, verifies, and retries only when useful.

### Refactor Loop

Use for behavior-preserving cleanup or architecture restructuring.

```text
/loop-pipeline run refactor-loop for simplifying the billing service
```

Claude records protected behavior and verification first, then delegates a scoped refactor to Codex and reviews for accidental behavior changes.

## Continuing A Loop

Loop state is private by default:

```text
~/.claude/loop-runs/<repo-id>/<loop-id>.md
```

This lets you change Claude Code chats without losing the workflow.

Continue later with:

```text
/loop-pipeline continue latest loop for this repo
```

or:

```text
/loop-pipeline continue 2026-06-17-feature-dark-mode
```

## Repo Cleanliness

The skill does not write loop state into your project repo by default. Repo-local state such as `.ai/loops/` is opt-in only.
