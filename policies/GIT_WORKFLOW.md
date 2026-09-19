# Git Workflow

The company uses trunk-oriented development with short-lived branches and a protected `main` branch.

This is not GitFlow. Long-lived release or develop branches MUST NOT be introduced without a documented product reason.

---

## Protected Branches

`main` is protected.

Agents MUST NOT:

- push directly to `main`
- force-push protected shared branches
- rewrite shared history without explicit authorization

Every meaningful change requires a pull request. A meaningful change is any change that affects product behavior, security, data, infrastructure, CI, or public or operational documentation.

Implementation agents MUST NOT be the sole approver of their own pull request.

---

## Branch Naming

Use short-lived branches named:

```text
feature/<task-id>-short-description
fix/<task-id>-short-description
security/<task-id>-short-description
chore/<task-id>-short-description
docs/<task-id>-short-description
refactor/<task-id>-short-description
```

Examples:

```text
feature/TA-123-invite-member
fix/TA-184-stale-session
security/TA-210-tenant-scope
```

If a tracker ID does not exist yet, the Chief of Staff SHOULD create the task first. Agents MAY use a short slug only for truly local drafts, then rename before opening the PR.

One branch SHOULD map to one task or a tightly related set of changes.

---

## Commit Requirements

Commits MUST be scoped and understandable.

Use Conventional Commit prefixes:

```text
feat:
fix:
security:
test:
docs:
refactor:
chore:
ci:
perf:
```

Examples:

```text
feat: add member invite endpoint
fix: prevent stale session reuse
security: enforce server-side tenant scope on exports
```

Commits SHOULD:

- contain related changes only
- explain why when the why is not obvious
- avoid secrets, credentials, and production data

Commits MUST NOT:

- mix unrelated refactors into risky changes
- use empty or misleading messages
- include `.env`, key files, or dumped credentials

---

## Pull Request Workflow

1. Create a short-lived branch from current `main`.
2. Implement the assigned task only.
3. Rebase or merge `main` as needed to stay current.
4. Open a PR using [../templates/pull-request.md](../templates/pull-request.md).
5. Reference the task ID.
6. Attach test evidence.
7. Request the required reviewers for the risk level.
8. Address review findings.
9. Merge only after required approvals.

PRs MUST reference the relevant task.

PRs SHOULD be small enough to review in one sitting. If they are not, the Chief of Staff SHOULD split the work.

---

## Review Requirements

Review requirements follow the risk model in [AI_AGENT_POLICY.md](AI_AGENT_POLICY.md) and [DEFINITION_OF_DONE.md](DEFINITION_OF_DONE.md).

Minimum expectations:

- LOW code changes: Code Review
- MEDIUM: QA and Code Review; Security when triggers apply
- HIGH: QA, Security, and Code Review; Architect when design changes
- CRITICAL: the HIGH set plus explicit human approval before production execution

The Code Reviewer MUST NOT approve solely because CI is green.

---

## Merge Strategy

Prefer squash merge or rebase-and-merge to keep `main` linear and readable.

Merge commits MAY be used when a PR intentionally preserves a small series of meaningful commits.

Do not merge:

- draft PRs
- PRs with failing required checks
- PRs missing required reviews
- PRs with unresolved release-blocking findings

---

## Conflict Handling

The implementation agent owns conflict resolution on their branch.

Conflict resolution MUST preserve intended behavior and MUST NOT drop tests or security checks to make the merge easier.

After resolving conflicts, required tests SHOULD be re-run.

If conflicts expose an architectural clash, escalate to the Architect.

---

## Emergency Fixes

Emergency production defects still use a PR when at all possible.

Use:

```text
fix/<task-id>-short-description
security/<task-id>-short-description
```

Emergency changes MAY shorten discussion. They MUST NOT skip:

- recorded human production approval
- after-the-fact documentation
- follow-up tests and reviews if they were compressed

If a hotfix was applied under emergency pressure, the Chief of Staff MUST open follow-up work for missing evidence or gates.

---

## Revert Strategy

Prefer revert over history rewrite.

If a merged change must be undone:

1. revert via PR
2. reference the original task and PR
3. describe user and operational impact
4. add or restore tests when the revert fixes a defect

Shared history rewrite requires explicit authorization from the human authority.

---

## Issue References

Use the product tracker ID in:

- branch names
- PR titles
- PR bodies
- commit footers when useful

Example:

```text
Refs: TA-123
```

Do not invent issue numbers.

---

## Related Documents

- [../AGENTS.md](../AGENTS.md)
- [RELEASE_POLICY.md](RELEASE_POLICY.md)
- [../templates/pull-request.md](../templates/pull-request.md)
