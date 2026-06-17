# Pipeline: Fix Loop

Use for bugs, failing tests, regressions, review findings, CI failures, broken behavior, or follow-up fixes after a feature/review pipeline.

## Stages

1. Intake Failure
   - Actor: Claude.
   - Capture the symptom, failing command, review finding, user report, or CI/log pointer.
   - Output: concise problem statement.

2. Reproduce Or Ground
   - Actor: Claude.
   - Reproduce locally when practical, or inspect the most relevant logs/tests/diff.
   - Avoid guessing without evidence.
   - Output: observed failure or explanation why reproduction is unavailable.

3. Root-Cause Brief
   - Actor: Claude.
   - Identify likely cause, affected area, smallest safe fix, and verification command.
   - Output: Codex-ready fix brief.

4. Delegation Gate
   - Actor: user.
   - Ask for approval before delegating source-code fixes to Codex when required.
   - Output: approved, revised, or stopped.

5. Codex Fix Execution
   - Actor: Codex.
   - Apply the smallest fix that addresses the grounded issue.
   - Output: Codex job/session ID and changed working tree.

6. Claude Review And Verify
   - Actor: Claude.
   - Review the patch, rerun targeted verification when practical, and inspect regression risk.
   - Output: pass/fail/block verdict.

7. Optional Codex Review
   - Actor: Codex.
   - Use for non-trivial fixes, repeated failures, security-sensitive changes, or broad diffs.
   - Output: independent review findings.

8. Retry Or Escalate
   - Actor: Claude + user.
   - If still failing, explain what remains and ask whether to continue.
   - Stop when the same failure repeats twice without new evidence or max iterations is reached.

9. Record
   - Actor: Claude.
   - Update state with failure, fix, verification, and next action.

## Default Done Criteria

- Original failure is fixed or explicitly unreproducible.
- Targeted verification passes where available.
- Claude review passes.
- Remaining risk is recorded.
