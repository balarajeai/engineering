# Skill Name

Database Migration

# Purpose

Change schemas or data with an explicit compatibility, recovery, and validation plan.

# When to Use

Use this skill for schema changes, data backfills, index changes, and any production data movement.

This skill is product-independent. It MAY refer to Spring Boot, Flyway, or Liquibase when a product uses them. Those tools are not required for every product.

# Required Inputs

- Migration purpose
- Current and target data shape
- Product migration mechanism, if any
- Risk level
- Whether the change can run during a rolling deployment

# Preconditions

- Architecture guidance exists when the data model changes meaningfully.
- Production credentials are not embedded in the change.
- Destructive production intent has explicit human approval before execution.

# Procedure

1. State the migration purpose and the product behavior it enables.
2. Write the forward migration.
3. Analyze compatibility:

- Can old application versions read the new shape?
- Can new application versions read the old shape?
- Is a multi-step expand/migrate/contract sequence required?

4. Analyze data impact: row counts, backfill needs, nullability, and irreversible transforms.
5. Analyze performance impact: locks, table rewrites, index builds, and query plans.
6. Record backup and recovery consideration.
7. Choose rollback or roll-forward. Prefer roll-forward when down-migrations would destroy data.
8. Execute locally or in test.
9. Run integration validation against the migrated schema.
10. Validate in staging for HIGH and CRITICAL changes.
11. Obtain human approval before destructive production changes.
12. After production execution, record the result and verification.

Never assume a migration is safe because it succeeded locally.

When the product uses Spring Boot with Flyway or Liquibase:

- keep migration versions ordered and immutable once applied
- do not rewrite an applied migration; add a new one
- fail the application on migration mismatch rather than drifting
- keep application startup able to run pending safe migrations only under the product's approved release process

# Validation

- Purpose, forward plan, and recovery plan exist
- Compatibility is explicit
- Tests or queries prove the new shape
- Production destructive steps have a human approval record
- Credentials were not committed

# Failure Conditions

- Hotfix ALTER in production without a recorded migration
- Local success treated as production proof
- Missing backup consideration for data-changing production work
- Down-migration that silently destroys data
- New microservice created just to own a table

# Required Evidence

- Migration files
- Local/test execution record
- Staging record when required
- Backup-readiness note for production
- Human approval for destructive production changes

# Output / Handoff

```text
STATUS:
COMPLETED / BLOCKED / REJECTED / NEEDS REVIEW

TASK:
Task identifier

SUMMARY:
What will change in the data store.

FILES:
Migration and test files.

DECISIONS:
Compatibility strategy and rollback versus roll-forward.

TESTS:
Migration and integration commands actually run.

RISKS:
Lock, data-loss, and compatibility risks.

SECURITY:
Sensitive data exposure and privilege used.

BLOCKERS:
Missing approval, backups, or staging.

NEXT:
QA, Security if required, Platform/SRE, or Chief of Staff.

EVIDENCE:
Command output and approval records that exist.
```
