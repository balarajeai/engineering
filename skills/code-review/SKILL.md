# Skill Name

Code Review

# Purpose

Independently assess whether the change is correct, scoped, maintainable, and compliant with approved architecture.

# When to Use

Use this skill for every meaningful pull request. Lightweight review is allowed for LOW-risk code changes. HIGH and CRITICAL changes require thorough review.

# Required Inputs

- PR using [../../templates/pull-request.md](../../templates/pull-request.md)
- Linked task
- Architecture acceptance criteria when architecture was required
- Test evidence
- QA and Security verdicts when those gates already ran

# Preconditions

- The reviewer is not the sole approver of their own implementation.
- The PR is not a direct push to `main`.
- CI results, if present, are inspected as evidence rather than as approval.

# Procedure

Review against:

- requirements
- architecture
- correctness
- maintainability
- tests
- security
- performance
- error handling
- scope
- backwards compatibility
- unnecessary complexity

Procedure:

1. Read the task and PR summary before the diff.
2. Confirm the change type and risk level look right. Escalate under-classification.
3. Walk the diff for requirement match and hidden scope.
4. Check architecture compliance, including modular-monolith-first and no unapproved services.
5. Inspect tests for meaningful assertions and real execution evidence.
6. Inspect error handling, concurrency, and compatibility.
7. Note security issues even if Security review is also required.
8. Separate blocking comments from nits.
9. Issue `APPROVE`, `REQUEST CHANGES`, or `BLOCKED`.

Passing tests alone are not sufficient for approval.

# Validation

- Every blocking comment is actionable
- Approval is not based only on CI
- New microservices without ADRs are blocked
- Secrets in the diff cause `REQUEST CHANGES` or `BLOCKED`

# Failure Conditions

- Rubber-stamp review
- Self-approval as the only review
- Architecture drift ignored
- Missing tests ignored for new behavior
- Required Security gate treated as optional

# Required Evidence

- PR review record
- Verdict
- List of blocking issues
- Files reviewed

# Output / Handoff

```text
STATUS:
COMPLETED / BLOCKED / REJECTED / NEEDS REVIEW

TASK:
Task identifier

SUMMARY:
Review verdict.

FILES:
Files reviewed.

DECISIONS:
Blocking versus non-blocking comments.

TESTS:
Evidence inspected.

RISKS:
Residual maintainability or correctness risks.

SECURITY:
Issues to send to Security or the implementer.

BLOCKERS:
Missing artifacts.

NEXT:
Implementation agent, Chief of Staff, or Security.

EVIDENCE:
PR review link that exists.
```
