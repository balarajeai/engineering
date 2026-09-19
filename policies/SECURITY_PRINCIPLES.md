# Security Principles

Security is a release gate when applicable, not a cleanup phase.

These principles apply to every product that adopts this engineering operating system. They do not claim any certification or regulatory compliance status.

When this policy conflicts with another engineering document, this policy and [AGENTS.md](../AGENTS.md) take precedence over convenience, schedule, or agent preference.

---

## Position in the Lifecycle

Security review is mandatory for HIGH and CRITICAL changes and for any change that affects authentication, authorization, tenant isolation, secrets, payments, or security controls.

The Chief of Staff MUST NOT waive required Security review.

Unresolved CRITICAL or HIGH findings MUST block release unless the human authority explicitly accepts the residual risk under the documented exception process in [AI_AGENT_POLICY.md](AI_AGENT_POLICY.md).

---

## Defense in Depth

No single control is sufficient.

Agents SHOULD assume that one control will fail and design the next control to limit blast radius.

Examples include independent authentication and authorization checks, server-side tenant enforcement, input validation, and least-privilege credentials.

---

## Least Privilege

Identities, services, agents, and humans MUST receive only the access required for the task.

General coding agents MUST NOT have unrestricted production credentials.

Database and infrastructure operations SHOULD use task-scoped credentials.

---

## Zero-Trust Assumptions

Internal network location is not proof of trust.

Client input, browser state, queued messages, webhooks, and service calls MUST be authenticated and authorized according to the product's trust model.

A client-provided tenant identifier MUST NEVER be trusted as authorization.

---

## Secure Defaults

New features MUST ship with secure defaults enabled.

Agents MUST NOT leave authentication, authorization, TLS, or tenant checks disabled for convenience, even in staging, unless the exception is documented and time-bounded.

Security controls MUST fail safely. A control failure MUST deny access rather than allow it.

---

## Secrets Management

Secrets MUST NOT be committed to source control, written to logs, embedded in images, or pasted into handoffs.

Production secret-management changes are CRITICAL and require human approval.

Credentials MUST be stored and transmitted securely.

If a secret may have been exposed, agents MUST stop, report, and escalate. They MUST NOT silently rotate or ignore the exposure.

---

## Encryption

Data in transit MUST use TLS for networked production and staging communication.

Encryption at rest SHOULD be used where the data classification or hosting design makes it appropriate.

Agents MUST NOT invent a custom cryptosystem. Use maintained platform and library primitives.

---

## Authentication

Authentication MUST be explicit for non-public actions.

Agents MUST NOT bypass authentication for convenience.

Session, JWT, OAuth 2.0, and OpenID Connect designs MUST be reviewed by Security when introduced or materially changed.

---

## Authorization and RBAC

Authorization MUST be enforced server-side.

Role-based access control, when used, MUST be checked on the server for every sensitive action. UI hiding is not authorization.

Agents MUST NOT bypass authorization for convenience.

Changes to authorization foundations are CRITICAL.

---

## Tenant Isolation

Multi-tenant systems MUST enforce tenant isolation server-side.

Every query, mutation, file access, job, and export that touches tenant data MUST be constrained by a trusted tenant context.

Tenant isolation failures are CRITICAL.

---

## Input Validation and Output Encoding

Treat all external input as untrusted.

Validate at trust boundaries. Encode output for the destination context to prevent injection and XSS.

APIs MUST reject unexpected types, oversized payloads, and out-of-range values rather than coercing them into dangerous behavior.

---

## Injection and Request Forgery

Designs MUST consider:

- SQL injection
- NoSQL injection
- command injection
- XSS
- CSRF
- SSRF
- path traversal
- template injection

Parameterized queries and safe APIs are required. String-concatenated queries are defects.

---

## API Security

APIs SHOULD apply:

- authentication
- authorization
- tenant checks
- input validation
- explicit error contracts
- rate limiting where abuse is plausible
- versioning for breaking changes

Service-to-service calls, when they exist, MUST authenticate. Network location is not sufficient.

---

## Dependency and Supply-Chain Security

Dependency changes SHOULD be reviewed for known vulnerabilities, unexpected maintainers, and unnecessary privilege.

Agents MUST NOT add a dependency to avoid writing a small amount of straightforward code when the dependency expands attack surface without clear benefit.

---

## Auditability and Secure Logging

Sensitive operations SHOULD be auditable where appropriate.

Logs MUST NOT contain secrets, raw credentials, session tokens, or unnecessary personal data.

Audit records, when required, MUST be attributable and tamper-evident to the degree the product design specifies.

---

## Data Minimization

Collect, persist, log, and retain only the data needed for the product requirement.

Exports, debug endpoints, and admin tools are high-risk features and require Security review.

---

## Backups and Recovery

Production data changes require backup and recovery consideration.

Destructive production database operations require explicit human approval.

Restore procedures SHOULD be verified periodically in product operations. This repository does not claim those restores have occurred.

---

## Incident Response

Suspected incidents MUST be escalated immediately to the Chief of Staff and the human authority.

Agents MUST preserve evidence, stop widening access, and avoid destructive "cleanup" unless directed.

After stabilization, emergency changes MUST still be documented.

---

## Threat Modeling

Threat modeling SHOULD be performed for HIGH and CRITICAL changes and for new trust boundaries.

Use [../skills/threat-model/SKILL.md](../skills/threat-model/SKILL.md). STRIDE MAY be used where useful. The process MUST stay practical.

---

## OWASP Considerations

Reviews MUST consider the current OWASP Top 10 and OWASP API Security Top 10 as a checklist of common failures, not as a certification claim.

---

## Service-to-Service Authentication

When a product has multiple trust domains or services, service-to-service calls MUST authenticate and authorize.

Agents MUST NOT treat private networks, Docker networks, or "internal" DNS names as equivalent to authentication.

---

## Docker and Hosting

Container images SHOULD run as non-root when practical, ship only required artifacts, and avoid baked-in secrets.

Company-wide policy stays provider-neutral. Provider-specific hardening belongs in product or infrastructure repositories.

---

## Security Review Triggers

Security review is required when a change includes any of the following:

- authentication or authorization
- session, JWT, OAuth, or OIDC handling
- RBAC or permission models
- tenant isolation or cross-tenant data access
- payments or sensitive financial operations
- secret management
- encryption
- public exposure of a new endpoint or admin capability
- database migrations affecting sensitive data
- dependency or supply-chain changes with security impact
- infrastructure, network, or TLS changes
- disabling or weakening a security control
- HIGH or CRITICAL risk classification

Use [../skills/security-review/SKILL.md](../skills/security-review/SKILL.md) and [../templates/security-review.md](../templates/security-review.md).

---

## Findings Standard

Security findings MUST include:

- ID
- title
- severity
- affected component
- attack path
- reproduction
- impact
- recommended remediation
- verification method

The Security Engineer MUST NOT silently fix a material finding and then independently approve that finding.

---

## Failure Modes

If a security control cannot be evaluated, the review result is not `PASS`.

If evidence is missing, the reviewer MUST return `FAIL` or `NEEDS REVIEW` and list the missing evidence.

If a human asks to skip a required security gate, agents MUST refuse and escalate.
