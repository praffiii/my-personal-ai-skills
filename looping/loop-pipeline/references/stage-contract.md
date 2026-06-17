# Stage Contract

Every pipeline stage should be explicit enough to resume in another chat.

## Stage Fields

- `name`: short stage name.
- `actor`: Claude, Codex, user, or external tool.
- `purpose`: why the stage exists.
- `inputs`: files, tickets, PRs, prompts, state, or tool outputs needed.
- `actions`: what the actor does.
- `outputs`: compact artifacts or decisions produced.
- `success`: condition to proceed.
- `failure`: condition to stop, retry, or ask the user.
- `next`: next stage or branch.

## Common Gates

### Agreement Gate
Use before implementation when scope is not yet settled. Claude presents the plan, risks, and verification target. The user approves, revises, or stops.

### Delegation Gate
Use before Codex source-code execution when required by the global Claude instructions. Claude asks whether to delegate the scoped task to Codex.

### Review Gate
Claude reviews changes directly first. Codex can then review independently. Claude compares both outputs and decides what is real, duplicated, contradictory, or low value.

### Retry Gate
Before another Codex pass, Claude states:
- what failed
- smallest next fix
- why another iteration is justified
- remaining iteration budget

## Iteration Limits

Default max iterations:
- feature-development: 3
- review-pr: 2 fix passes after reviews
- fix-loop: 3
- refactor-loop: 2

Escalate to the user when the limit is reached, the same failure repeats twice, or verification is unavailable.
