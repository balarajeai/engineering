# Skill Name

Threat Model

# Purpose

Identify how a change can be abused and what mitigations are required, without creating ceremony for low-risk work.

# When to Use

Use this skill for HIGH and CRITICAL changes, new trust boundaries, new admin capabilities, multi-tenant data access, authentication or authorization changes, and new external integrations.

STRIDE MAY be used where useful. The process MUST stay practical.

# Required Inputs

- Task and proposed or existing design
- Data types involved
- Actors and entry points
- Deployment or network sketch if the change crosses a boundary

# Preconditions

- The problem and scope are known enough to name assets.
- The Architect or Security Engineer is involved for HIGH and CRITICAL design changes.

# Procedure

Identify:

- assets
- actors
- entry points
- trust boundaries
- threats
- mitigations
- residual risks

Suggested steps:

1. Name the assets: data, credentials, admin actions, tenant records, money movement, or audit integrity.
2. Name the actors: anonymous user, authenticated user, tenant admin, operator, attacker, internal service.
3. Name entry points: UI, API, jobs, webhooks, file uploads, admin tools, database access paths.
4. Draw trust boundaries. Client-to-server is always a boundary. Service-to-service is a boundary when more than one trust domain exists.
5. Enumerate threats. STRIDE MAY be used:

- Spoofing
- Tampering
- Repudiation
- Information disclosure
- Denial of service
- Elevation of privilege

Also consider BOLA/IDOR and tenant isolation failures.

6. Map each relevant threat to a mitigation that will exist in the product.
7. Record residual risks and whether they are acceptable only with human approval.

Do not produce a long document that restates the feature. Produce a short model that a reviewer can attack.

# Validation

- Assets and actors are named
- Trust boundaries are explicit
- At least the obvious tenant, authz, injection, and secret threats were considered when relevant
- Residual risks are written down

# Failure Conditions

- Model used as decoration after implementation with no design effect
- Client-provided tenant IDs treated as trusted
- Internal network treated as authenticated
- Residual CRITICAL risk left implicit

# Required Evidence

- Short threat-model note in the task, ADR, or security review
- List of mitigations that implementation and QA can test
- Residual risk list

# Output / Handoff

```text
STATUS:
COMPLETED / BLOCKED / REJECTED / NEEDS REVIEW

TASK:
Task identifier

SUMMARY:
What was modeled and the highest residual risk.

FILES:
Threat-model note or ADR.

DECISIONS:
Mitigations required before implementation or release.

TESTS:
Threats that QA or Security MUST attempt to verify.

RISKS:
Residual risks.

SECURITY:
Boundaries and required Security review.

BLOCKERS:
Missing design facts.

NEXT:
Architect, implementation agents, or Security.

EVIDENCE:
The written model that exists.
```
