---
name: bahasa-mode
description: Use when the user invokes /bahasa-mode (or asks to brainstorm in Indonesian / Bahasa Indonesia) and wants the brainstorming conversation conducted in Indonesian while specs, code, and artifacts stay in English. A language layer over any brainstorming skill (brainstorming, office-hours, grill-with-me, spec, etc.).
---

# Bahasa Mode

## Overview

A thin **language layer** for brainstorming. It does NOT do the brainstorming itself — it wraps whatever brainstorming engine the user is already running (e.g. `brainstorming`, `office-hours`, `grill-with-me`, `spec` — any discussion/planning skill, not limited to these) and sets the **conversation language to Indonesian** for that session, then reverts to English.

**Core principle:** Reason in English, reply in Indonesian, write artifacts in English. This protects reasoning quality and token cost while making the back-and-forth comprehensible to an Indonesian speaker.

**Honest framing:** This is a _comprehension_ tool, not a cost optimizer. Indonesian output costs more tokens than English. The layer confines that premium to the conversational replies during brainstorming only — every reasoning-heavy and high-value output (specs, plans, code) stays in English.

## When to Use

- User runs `/bahasa-mode`, or asks to "brainstorm in Indonesian" / "pakai Bahasa Indonesia".
- User is about to start (or is in) a brainstorming / planning / office-hours / spec session and wants to discuss it in Indonesian.

**When NOT to use:**

- Pure implementation work with no discussion (just write English).
- The user is comfortable in English for this session.

## How It Works

This skill composes with a brainstorming skill — it does not replace it.

1. **Keep running the underlying brainstorming skill's actual process/logic unchanged.** If no brainstorming skill is active, invoke the appropriate one (e.g. `superpowers:brainstorming`) and apply this layer on top.
2. **Apply the language rules below to every user-facing message** during the session.

## Language Rules (while active)

| Rule                                | Behavior                                                                                                                                                                                                                                                                      |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Think in English**                | Do all internal reasoning in English. Only the final visible reply is rendered in Indonesian. Never "think in Indonesian."                                                                                                                                                    |
| **Reply in Indonesian**             | All conversational replies, questions, options, and explanations to the user are in Bahasa Indonesia.                                                                                                                                                                         |
| **Keep technical terms in English** | Do NOT translate technical vocabulary. Write them as-is inside Indonesian sentences. e.g. _"Kita pakai caching biar endpoint-nya lebih cepat, terus di-deploy ke staging dulu."_ Words like `cache`, `endpoint`, `deploy`, `commit`, `merge`, `bug`, `API`, etc stay English. |

## Revert to English (the off-switches)

Three independent conditions return output to English. ALL apply.

1. **Artifacts are ALWAYS English** — even while the chat is Indonesian. Any `.md` spec, plan, code, commit message, PR body, or file content is written in English. No exceptions: the content of a deliverable is never Indonesian.
2. **Auto-end on transition** — the moment brainstorming concludes or transitions to implementation (e.g. spec approved, invoking `writing-plans`, starting to write code), Indonesian mode ends and ALL further conversation returns to English.
3. **Manual off-switch** — the user can end Indonesian mode anytime by saying `off`, `selesai`, `english`, `back to english`, or re-invoking the skill. When this happens, immediately switch all output back to English.

## Quick Reference

| Situation                       | Language of reply               | Language of any file written |
| ------------------------------- | ------------------------------- | ---------------------------- |
| Brainstorming Q&A (mode active) | Indonesian (tech terms English) | English                      |
| Writing the spec `.md`          | Indonesian (chat)               | **English** (file content)   |
| Spec approved → writing-plans   | **English**                     | English                      |
| User says "selesai" / "off"     | **English**                     | English                      |

## Common Mistakes

- **Writing the spec file in Indonesian.** The chat can be Indonesian; the file content must be English. Always.
- **Translating technical terms.** Don't turn `caching` into `penyimpanan sementara`. Keep the English term.
- **Reasoning in Indonesian.** Reasoning stays English to preserve quality; only translate the surface reply.
- **Forgetting to revert after transition.** Once implementation starts or the user signals done, stop replying in Indonesian.

## Example

```
User: /bahasa-mode  (then) /brainstorming  — "aku mau bikin fitur login"

Agent (Indonesian chat, English artifacts):
  "Oke, kita mulai dari tujuannya dulu. Login-nya mau pakai email/password,
   atau juga OAuth (Google, GitHub)? Dan apakah perlu session/JWT untuk
   auth-nya?"

... (brainstorming continues in Indonesian) ...

[Spec approved → transition]
Agent (back to English):
  "Spec written to docs/.../login-design.md. Please review before we
   move to the implementation plan."
```
