# Language Skills

Skills for language and communication modes.

## Included

- `bahasa-mode`: Indonesian conversation mode for brainstorming while keeping technical artifacts in English.

## Install

From the repo root:

```bash
cp -R language/bahasa-mode ~/.claude/skills/
```

Restart Claude Code or reload skills after copying.

## How To Use

In Claude Code, call the skill with `/bahasa-mode` before or during a brainstorming session:

```text
/bahasa-mode
```

You can also ask naturally:

```text
Pakai Bahasa Indonesia for this brainstorming session.
```

Then run the planning or brainstorming workflow you want:

```text
/brainstorming aku mau bikin fitur login
```

## Behavior

`bahasa-mode` is a language layer, not a full workflow by itself.

While active:

- user-facing brainstorming conversation is in Bahasa Indonesia
- technical terms stay in English
- specs, plans, code, commit messages, PR bodies, and other artifacts stay in English

It switches back to English when brainstorming ends, implementation starts, or the user says `off`, `selesai`, `english`, or `back to english`.
