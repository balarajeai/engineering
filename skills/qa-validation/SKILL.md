# Skill Name

QA Validation

# Purpose

Verify accepted behavior with real execution and produce evidence that later gates can trust.

# When to Use

Use this skill whenever QA is a required gate, and whenever a bug fix or feature claims to be ready for verification.

# Required Inputs

- Task and acceptance criteria
- Implementation handoff and PR
- Risk level
- Access to the product's test tools and a non-production environment

# Preconditions

- Acceptance criteria exist.
- The implementation agent has handed off.
- QA is not being asked to approve on claims alone.

# Procedure

1. Map each acceptance criterion to a verification step.
2. Identify happy path, failure paths, and boundary cases.
3. Select the cheapest test type that actually proves the criterion:

- unit or component tests for isolated logic
- API or integration tests at service and database boundaries
- E2E tests for user-visible flows that cannot be proven cheaper
- database assertions when data changes
- concurrency tests when races are plausible

4. Execute the plan. Record commands, environment, and results.
5. Perform regression testing around the changed area.
6. File defects with reproduction when behavior is wrong.
7. Issue `PASS`, `FAIL`, or `BLOCKED`.

QA MUST NEVER delete failing tests, weaken assertions, approve untested criteria, or fabricate execution.

# Validation

- Every acceptance criterion has a result
- Evidence shows the tests ran
- Failures are attached to reproduction, not opinion
- Skipped tests have written justification

# Failure Conditions

- Approval based on developer claims
- Missing environment ignored
- Green CI treated as QA
- Tests not run
- Security or review waived by QA

# Required Evidence

- Criteria mapping
- Commands run
- Results
- Screenshots or logs when they exist and are needed
- Defect IDs for failures

# Output / Handoff

```text
STATUS:
COMPLETED / BLOCKED / REJECTED / NEEDS REVIEW

TASK:
Task identifier

SUMMARY:
QA verdict.

FILES:
Tests added or reviewed.

DECISIONS:
Scope and N/A items.

TESTS:
Actual execution record.

RISKS:
Untested areas.

SECURITY:
Security-relevant observations.

BLOCKERS:
Missing environments or criteria.

NEXT:
Security if required, Code Reviewer, implementation agent, or Chief of Staff.

EVIDENCE:
Existing logs, CI links, or screenshots.
```
