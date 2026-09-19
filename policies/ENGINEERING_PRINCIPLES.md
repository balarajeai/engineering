# Engineering Principles

These principles govern how the company designs and changes software.

They apply to every product that adopts this engineering operating system. They do not prescribe a product architecture.

When a principle conflicts with [AGENTS.md](../AGENTS.md) or [SECURITY_PRINCIPLES.md](SECURITY_PRINCIPLES.md), the constitution and security policy take precedence.

---

## Core Principles

### Simplicity

Prefer the smallest design that satisfies the current requirements.

Agents MUST NOT add layers, services, frameworks, or indirection without a concrete problem they solve.

Cleverness is not a goal. A future reader SHOULD be able to understand the change without tribal knowledge.

### Maintainability

Optimize for the next correct change, not for theoretical elegance.

Names, module boundaries, tests, and documentation SHOULD make ownership obvious.

Duplication MAY be tolerated briefly when a premature abstraction would be worse. Repeated duplication MUST be called out in review.

### Correctness

Behavior MUST match accepted requirements and documented contracts.

Agents MUST NOT invent requirements or silently expand scope.

If requirements are incomplete, agents MUST stop and escalate rather than guessing product behavior.

### Reliability

Systems SHOULD fail in a limited, observable, and recoverable way.

Retries, timeouts, and fallbacks MUST be intentional. Silent retries that hide data loss or duplicate side effects are defects.

### Observability

Meaningful changes SHOULD leave operators able to answer:

- is it working?
- what failed?
- whom did it affect?
- can we reconstruct what happened?

Logs MUST NOT contain secrets. Sensitive operations SHOULD be auditable where appropriate.

### Testability

New behavior requires tests. Bug fixes SHOULD include regression tests where practical.

A design that cannot be tested at the appropriate level is incomplete.

### Secure by Default

Security controls MUST be present by default and fail closed.

Authentication, authorization, and tenant isolation MUST NOT be optional conveniences to enable later.

See [SECURITY_PRINCIPLES.md](SECURITY_PRINCIPLES.md).

### Explicit Failure

Failures MUST be visible.

Agents MUST NOT hide errors, swallow exceptions without cause, fabricate success, or mark incomplete work complete.

User-facing errors SHOULD be useful without leaking internals.

### Backward Compatibility

Public contracts, persisted data, and rolling deployments SHOULD remain compatible unless a breaking change is explicit, versioned, and approved.

Schema migrations SHOULD preserve compatibility during rolling deployments where relevant.

### Small Changes

Prefer short-lived branches and reviewable diffs.

A change SHOULD do one job. Unrelated cleanup MUST NOT be smuggled into a risky change.

### Documentation

Document decisions that a later engineer cannot infer from the code.

Important architectural decisions MUST be recorded. Task, PR, and release templates exist so documentation stays attached to work, not stored only in chat.

### Automation

Repeatable checks SHOULD run in CI.

Automation MUST NOT become a substitute for required human or independent-agent judgment. Green CI is evidence, not approval.

### Ownership

Every change MUST have a responsible role and a next owner.

The Chief of Staff tracks ownership. The Architect owns design decisions. Implementation agents own the change they make. QA, Security, and Code Review own their verdicts.

### Reversibility

Prefer reversible changes.

Meaningful releases MUST have a rollback or recovery plan. Destructive or irreversible work requires stronger gates and explicit human approval.

### Evidence-Based Engineering

Claims require evidence.

Agents MUST NOT invent test results, approvals, tool output, or completion percentages.

If evidence is missing, the status is `BLOCKED` or `NEEDS REVIEW`, not `COMPLETED`.

### Avoid Premature Complexity

Do not optimize for imagined scale, imagined teams, or imagined products.

Do not introduce infrastructure, extra languages, or extra services without a concrete requirement.

---

## Modular Monolith Before Microservices

Microservices are a supported engineering capability, not the default architecture.

### Why this is the default

A network boundary is not a module boundary. It adds:

- independent failure modes
- versioning and compatibility work
- local development complexity
- observability and tracing cost
- deployment and rollback coupling or drift
- data consistency problems
- more authentication and authorization surface
- more operational toil for a small company

Those costs are justified only when they buy a concrete advantage.

### What to do instead

New products SHOULD start as a modular monolith:

- one deployable unit
- clear internal module boundaries
- explicit interfaces between modules
- data ownership that can be separated later if needed

Prefer cohesive modules before network boundaries.

Do not create `auth-service`, `user-service`, `audit-service`, `notification-service`, or similar services merely because those concepts exist.

### When microservices become justified

A separate service MAY be proposed when at least one concrete requirement exists, such as:

- independent scaling requirements
- security isolation
- fault isolation
- regulatory isolation
- deployment independence
- substantially different runtime requirements
- clear domain boundaries
- team ownership boundaries
- operational requirements that justify separation

"Future scale" by itself is NOT sufficient justification.

Every proposed microservice MUST have a documented reason for existing.

The Architect MUST approve new service boundaries.

The Backend Engineer MUST NOT introduce a new microservice without an approved architectural decision.

---

## Technology Choice

Technology choice MUST follow product requirements, not agent preference.

The organization supports multiple stacks. Backend agents are expected to be strong in Java/Spring Boot and TypeScript/Node.js. Frontend agents are expected to be strong in React, Next.js, and TypeScript. That does not make those stacks mandatory for every product.

A single product SHOULD minimize the number of languages and frameworks unless there is a concrete benefit.

The Architect SHOULD document major technology decisions.

---

## Change Discipline

1. Understand the requirement.
2. Inspect the current system.
3. Choose the smallest correct change.
4. Record architecture and security impact.
5. Implement and test.
6. Produce evidence.
7. Hand off through the required gates.

See [DEFINITION_OF_DONE.md](DEFINITION_OF_DONE.md) and [../skills/feature-development/SKILL.md](../skills/feature-development/SKILL.md).
