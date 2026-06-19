# Personal AI Skills

Reusable AI-agent skills and workflow protocols for Claude Code, Codex, and related coding-agent workflows.

## Included Skills

- [`looping/loop-pipeline`](looping/loop-pipeline) - Manual Claude Code + Codex loop pipelines for feature development, dual-review PR review, fix loops, and refactors.

## Prerequisite

For `loop-pipeline`, install a Claude Code Codex plugin first.

### Option 1: Official Plugin

Use the official OpenAI plugin if you want the upstream Claude Code + Codex integration:

```bash
/plugin marketplace add openai/codex-plugin-cc
/plugin install codex@openai-codex
/reload-plugins
/codex:setup
```

Repository: [openai/codex-plugin-cc](https://github.com/openai/codex-plugin-cc)

### Option 2: Praffi's Fork (Recommended)

Use this fork for the workflow this repo is designed around: Claude as orchestrator/reviewer and Codex as a visible executor or independent second reviewer.

```bash
/plugin marketplace add praffiii/codex-plugin-cc
/plugin install codex@openai-codex
/reload-plugins
/codex:setup
```

Repository: [praffiii/codex-plugin-cc](https://github.com/praffiii/codex-plugin-cc)

The fork keeps Codex work attached and visible inside Claude Code, which is useful for loop-pipeline workflows.

## Quick Install

Copy the skill into your Claude Code skills directory:

```bash
cp -R looping/loop-pipeline ~/.claude/skills/
```

Restart Claude Code or reload skills after copying.

## Usage

Call the skill in Claude Code:

```text
/loop-pipeline run feature-development for add dark mode to this app
```

```text
/loop-pipeline review this PR with dual review
```

For the full tutorial, see [`looping/README.md`](looping/README.md).

## What Loop Pipeline Does

`loop-pipeline` formalizes a human-in-the-loop workflow:

- Claude is the orchestrator, first reviewer, and final judge.
- Codex is the executor and independent second reviewer.
- The user is the approval gate.
- Loop state is private by default under `~/.claude/loop-runs/`.
