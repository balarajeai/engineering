# Release Policy

Releases move reviewed work from a product repository into a running environment.

There is no autonomous production deployment. Human approval is mandatory before production deployment.

This policy is product-independent and provider-neutral.

---

## Environments

| Environment | Purpose | Production data | Human approval |
| --- | --- | --- | --- |
| development | Local and ephemeral agent/developer work | MUST NOT use production data or production secrets | Not required |
| test | Automated and QA verification | MUST NOT use production secrets | Not required |
| staging | Release-candidate verification | Production-like configuration without production secrets where possible | SHOULD be used for HIGH and CRITICAL releases |
| production | Real users and real data | Production data and secrets | Required |

Agents MUST NOT promote a build by changing an environment label. Promotion is a recorded release action.

---

## Versioning

Use Semantic Versioning when the product publishes versions:

- `MAJOR` for incompatible API or data changes
- `MINOR` for backward-compatible features
- `PATCH` for backward-compatible fixes

Security fixes SHOULD be clearly identified in release notes even when the version bump is a patch.

Pre-release identifiers MAY be used for release candidates, for example `1.4.0-rc.1`.

Do not invent version numbers that the product does not track.

---

## Release Candidates

HIGH and CRITICAL releases SHOULD produce a release candidate and verify it in test and staging before production.

LOW and MEDIUM changes MAY be batched into a normal release train if the product uses one.

---

## Required Gates

A production release MUST have:

- CI passing
- required QA approval
- required Security approval when the risk level or security triggers apply
- Code Review approval for included meaningful changes
- Chief of Staff release-readiness check
- recorded human production approval
- deployment performed by Platform / SRE only after that approval

Failure at any mandatory gate returns the work to the appropriate earlier stage.

The Chief of Staff MUST NOT waive these gates.

---

## Release Checklist

Use [../templates/release-checklist.md](../templates/release-checklist.md).

The checklist MUST include:

- release version
- product
- included changes
- CI status
- QA status
- Security status
- code review status
- migration status
- backup readiness
- release notes
- monitoring readiness
- rollback plan
- human production approval
- deployment record
- smoke tests
- post-release monitoring
- final status

---

## CI Gates

CI SHOULD run, at minimum:

- build
- unit tests
- relevant integration tests
- lint/type checks the product already owns

CI MUST NOT be greened by deleting tests, weakening assertions, or skipping tests without documented justification.

Green CI is evidence for the Code Reviewer. It is not approval.

---

## QA, Security, and Review

QA MUST verify acceptance criteria with execution evidence.

Security MUST review when required by [SECURITY_PRINCIPLES.md](SECURITY_PRINCIPLES.md) or [AI_AGENT_POLICY.md](AI_AGENT_POLICY.md).

Unresolved CRITICAL or HIGH findings block release unless a human accepts them through the exception process.

The Code Reviewer MUST review the change, not only the pipeline.

---

## Database Migrations

Migrations follow [../skills/db-migration/SKILL.md](../skills/db-migration/SKILL.md).

Production migrations MUST consider:

- compatibility
- data impact
- performance impact
- backup or recovery
- rollback or roll-forward
- staging validation for HIGH and CRITICAL changes

Destructive production database operations require explicit human approval.

A migration is not safe because it succeeded locally.

---

## Backup Readiness

For releases that change production data or schema, Platform / SRE MUST confirm backup readiness or record why backups do not apply.

This policy does not claim that backups have been tested for any product.

---

## Deployment

Platform / SRE prepares and executes deployment.

Deployment to production MUST NOT start until human approval is recorded on the release checklist.

General coding agents MUST NOT deploy production.

Company-wide policy does not bind releases to a specific hosting vendor. Product runbooks MAY name a vendor. Engineering policy stays portable.

---

## Smoke Tests

After production deployment, Platform / SRE or QA MUST run the agreed smoke tests.

If smoke tests fail, treat the release as failed and execute the rollback or recovery plan unless the human authority explicitly directs a different response.

---

## Rollback and Recovery

Meaningful releases MUST have a rollback or recovery plan before production approval.

The plan SHOULD state:

- how to stop the bad change
- how to restore service
- whether data changes can be reversed or must be rolled forward
- who decides

Prefer reversibility. If the change is irreversible, the risk level is at least HIGH and often CRITICAL.

---

## Post-Release Verification

After smoke tests, check:

- error rates
- latency or health signals the product already emits
- audit or security signals when the release is security-sensitive
- a short confirmation that the intended change is visible

Record the result on the checklist.

---

## Monitoring

A release is not complete if nobody can tell whether it is failing.

If the product has no useful health signal for the changed area, the implementation is incomplete unless the gap is an accepted, recorded exception.

---

## Hotfix Process

1. Chief of Staff opens or updates a `fix/` or `security/` task.
2. Classify risk. Do not under-classify because the incident is urgent.
3. Implement the smallest correct fix.
4. Keep tests and evidence. Compress discussion, not proof.
5. Obtain the required reviews that time allows; record anything deferred.
6. Obtain human production approval.
7. Deploy, smoke test, and monitor.
8. After stabilization, complete missing documentation, tests, and follow-up reviews.

Emergency changes MUST still be documented after stabilization.

---

## Incident Escalation

Incidents escalate to the Chief of Staff and the human Product Owner.

Agents MUST:

- preserve evidence
- stop widening access
- avoid destructive cleanup unless directed
- document actions after stabilization

This policy does not create an on-call roster. Product operations MAY define one.

---

## Related Documents

- [DEFINITION_OF_DONE.md](DEFINITION_OF_DONE.md)
- [GIT_WORKFLOW.md](GIT_WORKFLOW.md)
- [../skills/release/SKILL.md](../skills/release/SKILL.md)
- [../agents/platform-engineer.md](../agents/platform-engineer.md)
- [../agents/chief-of-staff.md](../agents/chief-of-staff.md)
