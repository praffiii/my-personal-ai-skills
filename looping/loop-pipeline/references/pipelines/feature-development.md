# Pipeline: Feature Development

Use for building a feature from any source: direct user prompt, solo project idea, Linear ticket, GitHub issue, Figma, README/spec, TODO, or local notes.

## Stages

1. Intake
   - Actor: Claude.
   - Gather the source request and current repo context.
   - If Linear/GitHub/Figma is relevant, inspect only what is needed.
   - Output: concise goal, source pointers, unknowns.

2. Scope And Brainstorm
   - Actor: Claude + user.
   - Clarify behavior, UX, constraints, and non-goals.
   - Output: agreed scope and acceptance criteria.

3. Implementation Brief
   - Actor: Claude.
   - Produce a Codex-ready brief with goal, constraints, likely files/areas, acceptance criteria, verification commands, and what not to touch.
   - Output: brief stored in compact loop state or summarized there.

4. Agreement And Delegation Gate
   - Actor: user.
   - Ask for approval to delegate source-code implementation to Codex when required.
   - Output: approved, revised, or stopped.

5. Codex Execution
   - Actor: Codex.
   - Delegate implementation with the scoped brief.
   - Output: Codex job/session ID, final result pointer, changed working tree.

6. Claude First Review
   - Actor: Claude.
   - Review diff, correctness, security, design fit, and scope control.
   - Run or inspect verification when practical.
   - Output: pass/fail/block verdict and concrete issues.

7. Optional Codex Second Review
   - Actor: Codex.
   - Use when risk is non-trivial, change is broad, or Claude review is uncertain.
   - Output: independent findings.

8. Compare And Decide
   - Actor: Claude.
   - Compare Claude and Codex findings.
   - Classify: confirmed, Claude-only, Codex-only, false positive, needs user judgment.
   - Output: final next action.

9. Retry Or Done
   - Actor: Claude + user + Codex.
   - If fixes are needed, present the smallest next fix and ask for delegation approval.
   - Stop at done, blocked, or iteration limit.

10. Record
   - Actor: Claude.
   - Update compact state with final status, verification, remaining risks, and next action.

## Default Done Criteria

- Acceptance criteria are met.
- Claude review passes.
- Required verification has passed or unavailable verification is explicitly noted.
- User approval has been collected for subjective/product judgment.
