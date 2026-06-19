# Looping Skills

Skills for manual loop engineering workflows.

## Included

- `loop-pipeline`: feature development, dual-review PR review, fix loop, and refactor loop pipelines.

## Prerequisite

Install a Claude Code Codex plugin before using `loop-pipeline`.

### Option 1: Official Plugin

Use the official OpenAI plugin if you want the upstream Claude Code + Codex integration:

```bash
/plugin marketplace add openai/codex-plugin-cc
/plugin install codex@openai-codex
/reload-plugins
/codex:setup
```

Repository: [openai/codex-plugin-cc](https://github.com/openai/codex-plugin-cc)

### Option 2: Praffi's Fork (Recommended For Loop Pipeline)

Use this fork if you want the workflow `loop-pipeline` was designed around: Claude as orchestrator/reviewer and Codex as a visible executor or independent second reviewer.

```bash
/plugin marketplace add praffiii/codex-plugin-cc
/plugin install codex@openai-codex
/reload-plugins
/codex:setup
```

Repository: [praffiii/codex-plugin-cc](https://github.com/praffiii/codex-plugin-cc)

This fork keeps Codex work attached and visible inside Claude Code, instead of letting delegated work disappear into detached background execution. That makes it a better fit for loop workflows where Claude reviews the Codex result before the next step.

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
