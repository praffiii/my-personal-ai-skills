# Pipeline: Review PR

Use for PR, branch, or working-tree review. This is a dual-review pipeline: Claude reviews first, Codex reviews independently second, then Claude compares both.

## Stages

1. Intake PR
   - Actor: Claude.
   - Identify target: PR number/URL, base branch, current branch, or working tree.
   - Inspect diff scope and risk level.
   - Output: review target and risk notes.

2. Claude First Review
   - Actor: Claude.
   - Review directly before reading Codex findings.
   - Focus on correctness, regression risk, security, architecture/design fit, tests, and suspicious scope creep.
   - Output: Claude findings with severity and file/line references where possible.

3. Codex Independent Review
   - Actor: Codex.
   - Run read-only Codex review.
   - Run adversarial review when risk is high, design is debatable, auth/data-loss/security is involved, or the user asks for stronger challenge.
   - Output: Codex findings.

4. Compare Reviews
   - Actor: Claude.
   - Compare Claude and Codex outputs.
   - Group findings as:
     - both reviewers agree
     - Claude-only
     - Codex-only
     - contradictory
     - likely false positive
   - Output: synthesized review decision.

5. User Approval Gate
   - Actor: user.
   - User chooses which fixes to apply or asks for more investigation.
   - Output: approved fix set.

6. Codex Fix Pass
   - Actor: Codex.
   - Delegate only approved fixes.
   - Output: Codex job/session ID and changed working tree.

7. Claude Re-review
   - Actor: Claude.
   - Verify selected fixes and check for regressions or new scope creep.
   - Output: pass/fail/block verdict.

8. Optional Codex Re-review
   - Actor: Codex.
   - Use if the fix pass is broad or risk remains.
   - Output: second independent post-fix review.

9. Mark Pass/Fail
   - Actor: Claude.
   - Record final status, remaining risks, and whether another loop is needed.

## Default Done Criteria

- Claude has completed first review.
- Codex has completed independent review unless unavailable.
- Claude has compared both review streams.
- User-approved fixes are applied or explicitly deferred.
- Final Claude re-review passes or residual risk is recorded.
