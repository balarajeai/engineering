# Skill Name

Release

# Purpose

Ship reviewed work to a named environment with traceable approvals, verification, and recovery.

# When to Use

Use this skill for staging or production releases, hotfixes, and any promotion of a release candidate.

Primary users: Chief of Staff and Platform / SRE. Human production approval remains mandatory.

# Required Inputs

- [../../templates/release-checklist.md](../../templates/release-checklist.md)
- Version or release identifier
- Included changes and PRs
- CI status
- QA, Security, and Code Review verdicts
- Migration status
- Rollback or recovery plan

# Preconditions

- Required gates for included changes are complete.
- No unresolved release-blocking HIGH or CRITICAL findings remain unless a human exception exists.
- Production credentials are available only to the people or systems authorized to deploy.
- The Chief of Staff has not waived gates.

# Procedure

1. Confirm CI passing for the artifact to be released.
2. Confirm QA complete for included behavior changes.
3. Confirm Security complete when required.
4. Confirm Code Review complete for included meaningful changes.
5. Write or update release notes.
6. Confirm migration status and backup readiness for data-changing releases.
7. Publish the deployment plan and rollback or recovery plan.
8. Stop and obtain recorded human production approval. Do not infer it.
9. Platform / SRE deploys to the target environment.
10. Run smoke tests.
11. Check monitoring.
12. Perform post-release verification and record the final status.

If smoke tests fail, execute rollback or recovery unless the human authority explicitly directs otherwise.

Emergency releases follow the same steps with compressed discussion. Missing evidence MUST be followed up after stabilization.

# Validation

- Checklist fields are filled or explicitly `N/A`
- Human production approval is a name, time, and decision, not a guess
- Deployment and smoke-test evidence exist
- Version and included changes are traceable

# Failure Conditions

- Autonomous production deployment
- Deployment before approval
- Fabricated smoke tests
- Unknown migration status
- Hosting vendor treated as a substitute for a plan

# Required Evidence

- Completed release checklist
- CI record
- Approval record
- Deployment record
- Smoke-test results
- Monitoring notes

# Output / Handoff

```text
STATUS:
COMPLETED / BLOCKED / REJECTED / NEEDS REVIEW

TASK:
Release version

SUMMARY:
Where it shipped and whether it is healthy.

FILES:
Checklist, notes, and infra records.

DECISIONS:
Go/no-go and rollback decisions.

TESTS:
Smoke tests actually run.

RISKS:
Residual operational risks.

SECURITY:
Security gate status and exceptions.

BLOCKERS:
Missing approval or failed verification.

NEXT:
Chief of Staff, QA, Platform/SRE, or human Product Owner.

EVIDENCE:
Checklist and logs that exist.
```
