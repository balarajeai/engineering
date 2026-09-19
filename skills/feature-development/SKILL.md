# Skill Name

Feature Development

# Purpose

Implement a requested feature as the smallest correct change, with tests and a handoff that later gates can verify.

# When to Use

Use this skill for new product behavior assigned to Backend or Frontend implementation agents.

Do not use this skill to create architecture defaults, waive gates, or start a new product in this repository.

# Required Inputs

- Task ID and [../../templates/feature-task.md](../../templates/feature-task.md)
- Acceptance criteria
- Risk level and required gates
- Approved architecture or confirmation that architecture is not required
- Access to the product repository

# Preconditions

- The task is `READY`.
- Scope and non-goals are written.
- New service boundaries, if any, already have Architect approval and a documented reason.
- Secrets and production credentials are not required for implementation.

# Procedure

1. Understand the task. Restate acceptance criteria. Escalate invented or missing requirements.
2. Inspect the relevant system and code. Do not start from a blank design when the product already has a module for the problem.
3. Verify the acceptance criteria are testable. If they are not, return the task.
4. Identify architecture implications. Stop and consult the Architect when a new boundary, datastore, or consistency model appears.
5. Identify security implications. Treat authn, authz, tenant isolation, secrets, and injection as Security-review triggers.
6. Identify data implications. Use [../db-migration/SKILL.md](../db-migration/SKILL.md) when schema or data movement is required.
7. Implement the smallest correct change. Do not silently expand scope.
8. Add or update tests for meaningful success and failure paths.
9. Execute validation. Record commands that actually ran.
10. Update documentation, observability, and PR fields.
11. Produce the handoff and move the task to QA through the Chief of Staff.

Prefer a modular monolith module over a new microservice.

# Validation

- Acceptance criteria are implemented and no more
- Tests were added and executed
- Lint/type checks the product owns were run when available
- No new service was introduced without an ADR
- PR uses [../../templates/pull-request.md](../../templates/pull-request.md)
- Handoff distinguishes completed work from proposed follow-up

# Failure Conditions

- Requirements invented
- Tests not run
- Production deployment attempted
- Self-approval
- Secrets committed
- Migration assumed safe because it worked locally
- Scope expanded without approval

# Required Evidence

- PR link
- File list
- Test commands and results
- Screenshots for UI changes
- Migration notes when applicable
- Security notes

# Output / Handoff

```text
STATUS:
COMPLETED / BLOCKED / REJECTED / NEEDS REVIEW

TASK:
Task identifier

SUMMARY:
What was implemented.

FILES:
Files changed.

DECISIONS:
Implementation decisions.

TESTS:
Commands actually run and results.

RISKS:
Known risks.

SECURITY:
Authn/authz, tenant, secrets, injection, logging.

BLOCKERS:
Anything preventing QA.

NEXT:
QA, Security if required, or Chief of Staff.

EVIDENCE:
PR, test output, screenshots, migration notes that exist.
```
