# Pull Request

## Summary

## Linked task

Task ID:

## Change type

`feat` / `fix` / `security` / `test` / `docs` / `refactor` / `chore` / `ci` / `perf`

Risk level: `LOW` / `MEDIUM` / `HIGH` / `CRITICAL`

## What changed

## Why

## Architecture impact

- [ ] No architecture change
- [ ] Module boundary change
- [ ] New or changed contract
- [ ] New service boundary — ADR required
- ADR / spec links:

## Screenshots if UI

Attach before/after when the user-visible UI changed. Mark `N/A` if not UI.

## Testing performed

List commands that actually ran.

```text
```

## Test evidence

CI link, command output, or screenshots that exist. Do not claim unrun tests.

## Security impact

- [ ] None identified
- [ ] Authentication / authorization
- [ ] Tenant isolation
- [ ] Secrets
- [ ] Logging / data exposure
- Security review required? Yes / No
- Review link:

## Database impact

- [ ] None
- [ ] Schema
- [ ] Data backfill
- [ ] Index / performance

## Migration impact

- [ ] No migration
- [ ] Compatible expand/contract
- [ ] Requires downtime or lock
- [ ] Destructive — human approval required before production
- Rollback / roll-forward plan:

## Backward compatibility

- [ ] Compatible
- [ ] Breaking change, versioned and approved

## Observability

What operators can use to see success or failure.

## Deployment notes

Environments, feature flags, config, or order of operations.

## Rollback / recovery

How to undo or move forward if the change fails in production.

## Reviewer checklist

- [ ] Matches the linked task and no more
- [ ] Tests are meaningful and were executed
- [ ] Error handling is explicit
- [ ] No secrets committed
- [ ] Architecture remains modular-monolith-first unless an ADR exists
- [ ] QA verdict recorded when required
- [ ] Security verdict recorded when required
- [ ] Code Reviewer is not the sole implementer
- [ ] CI is evidence, not approval

Implementation agents MUST NOT be the sole approver of this PR.
