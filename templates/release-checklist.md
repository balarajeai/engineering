# Release Checklist

## Release version

## Product

## Included changes

| Task ID | Title | Risk | PR |
| --- | --- | --- | --- |
|  |  |  |  |

## CI status

`PASS` / `FAIL` / `NOT RUN`

Evidence:

## QA status

`PASS` / `FAIL` / `NOT REQUIRED` / `BLOCKED`

Evidence:

## Security status

`PASS` / `FAIL` / `PASS WITH NON-BLOCKING FINDINGS` / `NOT REQUIRED` / `BLOCKED`

Evidence:

Unresolved HIGH or CRITICAL findings require a recorded human exception.

## Code review status

`APPROVE` / `REQUEST CHANGES` / `BLOCKED`

Evidence:

## Migration status

`NONE` / `READY` / `APPLIED IN STAGING` / `BLOCKED`

Notes:

## Backup readiness

`READY` / `NOT APPLICABLE` / `NOT READY`

Notes:

## Release notes

## Monitoring readiness

What will be watched after deploy.

## Rollback plan

## Human production approval

Production deployment MUST NOT proceed until this section is complete.

- Decision: `APPROVED` / `REJECTED` / `PENDING`
- Approving human:
- Date and time:
- Scope approved:
- Conditions or exceptions:

Agents MUST NOT infer approval from urgency or informal language.

## Deployment

- Environment: `staging` / `production`
- Deployer role: Platform / SRE
- Started:
- Finished:
- Result: `SUCCESS` / `FAILED` / `NOT STARTED`

Evidence:

## Smoke tests

Commands actually run and results.

## Post-release monitoring

What was checked and what was observed.

## Final status

`RELEASED` / `ROLLED BACK` / `BLOCKED` / `ABORTED`

Recorded by:

This release is not done because artifacts were built. See [../policies/DEFINITION_OF_DONE.md](../policies/DEFINITION_OF_DONE.md).
