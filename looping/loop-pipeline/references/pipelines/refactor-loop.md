# Pipeline: Refactor Loop

Use for behavior-preserving restructuring, cleanup, simplification, module boundary improvement, or architecture cleanup.

## Stages

1. Intake Refactor Goal
   - Actor: Claude.
   - Capture what should improve and what behavior must not change.
   - Output: refactor goal, protected behavior, constraints.

2. Baseline Behavior
   - Actor: Claude.
   - Identify existing tests, type checks, builds, snapshots, or manual checks that protect behavior.
   - If coverage is weak, say so before delegating.
   - Output: verification baseline.

3. Refactor Plan
   - Actor: Claude.
   - Propose small, reversible refactor steps.
   - Avoid unrelated cleanup.
   - Output: scoped Codex brief and non-goals.

4. Agreement And Delegation Gate
   - Actor: user.
   - Ask for approval before delegating source-code changes when required.
   - Output: approved, revised, or stopped.

5. Codex Refactor Execution
   - Actor: Codex.
   - Apply scoped behavior-preserving changes.
   - Output: Codex job/session ID and changed working tree.

6. Claude Behavior Review
   - Actor: Claude.
   - Review diff for accidental behavior changes, overreach, API changes, and test gaps.
   - Run verification when practical.
   - Output: pass/fail/block verdict.

7. Codex Independent Review
   - Actor: Codex.
   - Use when refactor touches shared boundaries, public APIs, data models, or many files.
   - Output: independent risk findings.

8. Retry Or Done
   - Actor: Claude + user.
   - Retry only with a narrow follow-up brief.
   - Stop at max iterations or if behavior safety cannot be established.

9. Record
   - Actor: Claude.
   - Update state with final status and behavior verification.

## Default Done Criteria

- Intended structure improved.
- No intended behavior changed.
- Verification passes or coverage gaps are explicitly recorded.
- Claude review passes.
