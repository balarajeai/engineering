# Bug Task

## Bug ID

<!-- Required. Do not invent IDs. -->

## Summary

## Product

## Environment

`development` / `test` / `staging` / `production` / unknown

Build or version:

## Severity

`LOW` / `MEDIUM` / `HIGH` / `CRITICAL`

Use `CRITICAL` when the defect is a destructive data issue, tenant-isolation failure, authorization bypass, or production security-control failure.

## Reproduction

1.
2.
3.

Frequency: always / intermittent / unknown

## Expected behavior

## Actual behavior

## Business / user impact

Who is affected and what they cannot do.

## Suspected area

Application area, module, API, UI, or data path. Do not present guesses as facts.

## Evidence

Commands, responses, traces, or issue links that exist.

## Logs / screenshots

Attach or link artifacts. Redact secrets.

## Regression test requirements

- [ ] Reproducing test exists or is required
- [ ] Related failure paths to cover

## Security impact

- [ ] None identified
- [ ] Authentication
- [ ] Authorization
- [ ] Tenant isolation
- [ ] Data exposure
- [ ] Injection
- Security review required? Yes / No

## Fix acceptance criteria

- [ ] Reported reproduction no longer occurs
- [ ] Expected behavior is restored
- [ ] Regression test executed where practical
- [ ] QA verified the fix and did not rely only on the implementer
- [ ] Code Review complete
- [ ] Security review complete if required
- [ ] No silent scope expansion

## Gates

| Gate | Required? | Status |
| --- | --- | --- |
| QA | Yes |  |
| Security |  |  |
| Code Review | Yes |  |
| Human production approval | Yes, before production |  |
