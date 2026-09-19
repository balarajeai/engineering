# Skill Name

Task Orchestration

# Purpose

Give the Chief of Staff a repeatable way to move work through the engineering pipeline without waiving mandatory gates.

# When to Use

Use this skill whenever work is created, assigned, blocked, rejected, reworked, or prepared for release.

Primary user: Chief of Staff / Engineering Manager.

# Required Inputs

- Product Owner priority or problem statement
- Product name
- Task type: feature, bug, security fix, infrastructure, or release
- Known dependencies
- Available agent roles

# Preconditions

- The work belongs to a product repository, not this operating-system repository, unless the work is about this operating system.
- [../../AGENTS.md](../../AGENTS.md) and [../../policies/DEFINITION_OF_DONE.md](../../policies/DEFINITION_OF_DONE.md) are in force.
- A task record can be created from [../../templates/feature-task.md](../../templates/feature-task.md) or [../../templates/bug-task.md](../../templates/bug-task.md).

# Procedure

## Lifecycle

```text
BACKLOG
→ READY
→ IN PROGRESS
→ QA
→ SECURITY (when required)
→ REVIEW
→ RELEASE READY
→ RELEASED
```

Additional states: `BLOCKED`, `REJECTED`, `CANCELLED`.

## Assignment

1. Capture the problem and business priority.
2. Ensure acceptance criteria exist. If they do not, keep the task in `BACKLOG`.
3. Classify risk as `LOW`, `MEDIUM`, `HIGH`, or `CRITICAL`.
4. If risk is unclear, use the higher plausible level.
5. Select gates from the risk table in [../../policies/DEFINITION_OF_DONE.md](../../policies/DEFINITION_OF_DONE.md).
6. Route architecture questions to the Architect before implementation when architecture is required.
7. Assign implementation only after the task is `READY`.
8. Allow Backend and Frontend to proceed in parallel only when contracts exist.

## Gate Selection

Mandatory gates cannot be removed because a date is near or an agent is confident.

- LOW code changes require Code Review. Security is added if a trigger appears.
- MEDIUM requires QA and Code Review. Security is added for trust-boundary, auth-adjacent, or data-exposure work.
- HIGH requires QA, Security, and Code Review. Architect involvement is required when design or boundaries change.
- CRITICAL requires the HIGH set plus explicit human approval before production execution.
- A pure production operations change with no product-behavior delta MAY replace product QA with a dedicated operational checklist. That exception MUST be recorded and MUST NOT be used for application feature or bug work.

Production deployment always requires human approval after `RELEASE READY`.

## Dependencies

Record blockers as task IDs, not informal memory.

A dependent task MUST NOT enter `IN PROGRESS` if a required contract, migration, or decision does not exist.

## Blockers

Move a task to `BLOCKED` when evidence, permissions, environments, or decisions are missing.

The handoff MUST name the missing item and the owner.

Do not keep a blocked task in `IN PROGRESS`.

## Rejection and Rework

If QA, Security, or Code Review fails, set `REJECTED` or return to `IN PROGRESS` with the failing gate named.

Rework MUST re-enter the failed gate and any later gate whose result is now stale.

A security remediator MUST NOT be the only approver of a material finding.

## Status Reporting

Use:

```text
PRODUCT
MILESTONE
OVERALL STATUS
COMPLETED
IN PROGRESS
BLOCKED
QA
SECURITY
REVIEW
RELEASE READY
RISKS
NEXT ACTIONS
```

Do not invent percentages.

## Release Readiness

A task may move to `RELEASE READY` only when required gates have artifacts.

A product may be called release ready only when the [../../templates/release-checklist.md](../../templates/release-checklist.md) can be given to a human for approval.

# Validation

- Every `READY` task has acceptance criteria, risk, and gates.
- Every `RELEASE READY` task has the required verdicts.
- No task skipped a mandatory gate.
- Status reports match tracker state.

# Failure Conditions

- Gates waived
- Status marked complete without evidence
- Architecture owned or overridden by the Chief of Staff
- Production declared approved without a human record
- Percent-complete invented

# Required Evidence

- Task record
- Risk and gate list
- Links to PR, QA, Security, and review artifacts when those gates apply
- Status report

# Output / Handoff

Use the Chief of Staff handoff in [../../agents/chief-of-staff.md](../../agents/chief-of-staff.md).
