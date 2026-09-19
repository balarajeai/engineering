# Definition of Done

A task is not done because code exists.

Done means the required work, evidence, and gates for that change type are complete. Green CI is necessary when CI applies. It is not sufficient.

This policy applies to every product that adopts this engineering operating system.

---

## Universal Completion Criteria

A change is not complete unless the applicable items below are true:

- acceptance criteria are satisfied
- implementation is complete for the agreed scope
- tests were added or updated when behavior changed
- tests were executed
- executed tests passed
- lint and type checks passed when the product has them
- error handling was considered
- security considerations were addressed
- documentation was updated when behavior, operations, or contracts changed
- migrations were validated when data shape or data movement changed
- observability was added where operators would otherwise be blind
- backward compatibility was considered
- QA completed when required by risk level
- security review completed when required by risk level or trigger
- code review completed when required
- no unresolved release-blocking issues remain
- the pull request is complete
- release notes were added when the change is user-visible or operationally meaningful

Agents MUST NOT mark work complete when any required item is unknown.

If an item does not apply, the handoff MUST say `N/A` and why.

---

## Gate Requirements by Risk

| Risk | Architect | QA | Security | Code Review | Human production approval |
| --- | --- | --- | --- | --- | --- |
| LOW | Only if architecture changes | SHOULD verify no behavior change for code changes | Only if a security impact appears | Required for meaningful code changes | Required before production deployment |
| MEDIUM | If architecture or contracts change | Required | Required when trust boundaries, auth-adjacent behavior, or data exposure are involved | Required | Required before production deployment |
| HIGH | Required when design or boundaries change; SHOULD review otherwise | Required | Required | Required | Required before production deployment |
| CRITICAL | Required when system design is affected | Required for product behavior changes | Required | Required for code changes | Required before execution or production deployment |

The Chief of Staff MUST record the risk level and the selected gates. The Chief of Staff MUST NOT waive a mandatory gate.

A pure production operations change with no product-behavior delta MAY use a dedicated operational checklist plus Security, Platform / SRE, and human approval instead of product QA. That exception MUST be recorded. It MUST NOT be used for application feature or bug work.

---

## Feature Done

A feature is done when:

- the [feature task](../templates/feature-task.md) has clear acceptance criteria
- architecture impact was assessed and, if required, approved
- implementation matches the accepted scope and no more
- tests cover meaningful success and failure paths
- tests were executed and passed
- QA mapped and verified acceptance criteria
- security review passed or was not required
- code review approved the change
- documentation, observability, and migrations are complete when applicable
- the PR references the task and includes evidence
- unresolved HIGH or CRITICAL findings are either fixed or explicitly accepted by a human

A feature is not done when it is "mostly working" or waiting on unrun tests.

---

## Bug Done

A bug is done when:

- the [bug task](../templates/bug-task.md) records reproduction, expected behavior, and actual behavior
- the fix addresses the reported failure without silent scope expansion
- a regression test exists where practical
- the regression was executed and passed
- related failure paths were checked
- QA verified the fix and did not rely solely on the implementer's claim
- security impact was assessed and reviewed when required
- code review approved the change

Deleting or weakening the failing test is not a fix.

---

## Security Fix Done

A security fix is done when:

- the finding has an ID, severity, attack path, impact, and verification method
- the remediation matches the agreed fix
- tests or review steps prove the attack path is closed, or residual risk is explicitly accepted
- no secret material was introduced into logs, source, or artifacts
- independent verification occurred; the fixer is not the only approver of a material finding
- QA verified user-visible or behavioral impact when the fix changes behavior
- code review approved the change
- release notes or operational notes warn operators when needed

A silent patch without evidence is not done.

---

## Infrastructure Change Done

An infrastructure change is done when:

- the change has a recorded purpose, blast radius, and rollback or recovery plan
- secrets were not committed or logged
- least privilege was preserved
- CI and configuration checks appropriate to the change passed
- staging or equivalent verification occurred for HIGH and CRITICAL changes
- Security reviewed the change when it is HIGH or CRITICAL or when review triggers apply
- Platform / SRE prepared the change and did not deploy production without human approval
- monitoring and backup impact were considered
- the change is traceable to a task and PR or change record

Provider-specific work stays in the product or infrastructure repository. Company policy remains provider-neutral.

---

## Release Done

A release is done when:

- included changes are listed
- CI passed for the release candidate
- required QA, Security, and Code Review gates passed
- migration status is known
- backup readiness was considered for data-changing releases
- release notes exist
- rollback or recovery plan exists
- human production approval is recorded
- Platform / SRE deployed only after that approval
- smoke tests ran
- post-release monitoring was checked
- the final status is recorded on the [release checklist](../templates/release-checklist.md)

A release is not done because artifacts were built.

Production deployment without recorded human approval is never done. It is a policy violation.

---

## Incomplete Work

The following are not done:

- implementation without executed tests
- tests that were not run
- reviews based only on intent
- "works on my machine" without evidence
- skipped gates
- fabricated evidence
- unresolved release-blocking findings

Use `BLOCKED`, `REJECTED`, or `NEEDS REVIEW` instead of `COMPLETED` when done criteria are unmet.

---

## Related Documents

- [AI_AGENT_POLICY.md](AI_AGENT_POLICY.md)
- [RELEASE_POLICY.md](RELEASE_POLICY.md)
- [../skills/task-orchestration/SKILL.md](../skills/task-orchestration/SKILL.md)
- [../AGENTS.md](../AGENTS.md)
