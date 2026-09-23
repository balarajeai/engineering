# Code Quality

## Purpose

All production code must be easy for engineers to:

- read
- understand
- test
- debug
- review
- modify
- operate safely

Production-grade does not mean complicated.

Prefer code that is:

- correct
- cohesive
- readable
- well-named
- explicit
- testable
- debuggable
- secure
- predictable
- maintainable

Prefer boring, understandable solutions over clever or unnecessarily abstract ones.

---

## 1. Cohesion and Responsibility

Classes, modules, functions, components, packages, and scripts should have clear responsibilities.

Prefer cohesive units with a clear reason to change.

Avoid god objects, god services, giant components, giant functions, and scripts that accumulate unrelated responsibilities.

Do not combine unrelated concerns such as:

- authorization
- validation
- persistence
- transport
- cryptography
- auditing
- UI rendering
- workflow orchestration
- result processing

into a single unit when separation would materially improve clarity, testing, or debugging.

Do not artificially fragment cohesive behavior merely to reduce line count.

There is no universal maximum number of lines for a class or function.

Responsibility and complexity are the deciding factors.

---

## 2. Small, Understandable Functions and Methods

Functions and methods should perform one understandable operation.

Prefer explicit operations such as:

authorizeAction(...)
validateConfirmation(...)
buildCommand(...)
recordAuditEvent(...)
applyResult(...)

over vague orchestration functions that perform many unrelated steps internally.

Avoid deeply nested control flow.

Prefer when appropriate:

- guard clauses
- early failure
- extracted business rules
- explicit validation
- explicit state transitions

Refactor when a function becomes difficult to:

- name accurately
- understand quickly
- test independently
- debug
- reason about safely

Do not enforce arbitrary line-count limits.

---

## 3. Naming

Names must communicate intent.

Use domain/business terminology whenever possible.

Prefer names such as:

organizationId
environmentId
operationId
confirmationBinding
commandExpiry
affectedRecordLimit

Avoid vague names such as:

data
info
obj
thing
stuff
temp
helper
util
manager
processor

unless the term genuinely represents the concept.

Prefer:

verifyConnectionBinding()

over:

check()

Prefer:

markOperationUnknown()

over:

updateStatus()

Names should make the code easier to understand without requiring the reader to inspect every implementation detail.

Avoid obscure abbreviations.

Use established project terminology consistently.

---

## 4. Domain Language

Use one consistent name for each important domain concept.

Do not invent multiple terms for the same concept.

Do not rename established domain concepts merely because another term is personally preferred.

Code should communicate the business domain, not only technical mechanics.

---

## 5. Dependencies

Dependencies should be explicit.

Prefer dependency injection or equivalent explicit construction appropriate to the language/framework.

Avoid:

- global mutable state
- hidden dependencies
- service locator patterns
- unnecessary static mutable state
- excessive framework magic
- unnecessary reflection

Do not create interfaces or abstractions automatically.

Create abstractions when they represent meaningful boundaries such as:

- persistence
- external APIs
- network transport
- cryptography
- time
- filesystem
- infrastructure

Do not create abstractions solely in anticipation of hypothetical future requirements.

---

## 6. Simplicity

Use the simplest design that safely satisfies current approved requirements.

Do not introduce architecture or patterns merely because they are fashionable.

Avoid unjustified:

- microservices
- message brokers
- distributed caches
- plugin systems
- generic frameworks
- complex inheritance
- CQRS
- event sourcing
- unnecessary design patterns
- speculative extension points

Future scale alone is not sufficient justification for complexity.

Complexity must solve a concrete problem.

---

## 7. Business Logic

Business rules must be explicit and independently testable where practical.

Do not bury important behavior inside framework plumbing.

Avoid hiding critical rules inside:

- controllers
- UI components
- ORM callbacks
- repositories
- serialization
- infrastructure code
- database triggers

unless explicitly justified and documented.

Important state transitions must be understandable.

Avoid hidden side effects.

---

## 8. Boundaries

Keep responsibilities clear between:

- transport
- business logic
- persistence
- security
- external integrations
- presentation
- infrastructure

Controllers/routes/handlers should generally remain thin.

Repositories/data-access layers should focus on persistence.

UI components should not silently become backend/domain layers.

Infrastructure scripts should not silently encode undocumented business rules.

---

## 9. Testability

Important behavior must be designed so it can be tested.

Separate where appropriate:

- business rules
- authorization
- persistence
- external transport
- serialization
- cryptography
- infrastructure
- UI behavior

Avoid designs that require an entire application or environment to run merely to test ordinary business logic.

Use the smallest appropriate test level.

---

## 10. Test Quality

Tests are production code and must meet quality standards.

Tests should be:

- readable
- deterministic
- focused
- appropriately isolated
- meaningfully named

Test behavior rather than implementation trivia.

Prioritize:

- business invariants
- security boundaries
- authorization
- tenant isolation
- state transitions
- failure modes
- persistence constraints
- transactions
- concurrency where relevant
- idempotency where relevant
- protocol behavior
- integration contracts

Avoid low-value tests that merely prove:

- getters/setters work
- a framework created a bean
- a mock was called without verifying meaningful behavior

Do not claim tests were executed when they were not.

---

## 11. Debuggability

Production behavior must be diagnosable.

Important workflows should expose useful context through appropriate:

- structured logging
- operation/request identifiers
- state transitions
- error information
- metrics/tracing where justified

Logs should help answer:

- what happened?
- where did it happen?
- which operation/resource was involved?
- why did it fail?

Do not hide failures.

Do not swallow exceptions/errors.

Do not fabricate success.

---

## 12. Logging

Logging must be useful rather than noisy.

Log important boundaries and failures with safe contextual identifiers.

Never log:

- passwords
- database credentials
- private keys
- access tokens
- session tokens
- authorization headers
- raw secrets
- sensitive data without explicit justification

Avoid excessive debug logging in production paths.

---

## 13. Error Handling

Errors must be predictable and actionable.

Do not swallow exceptions/errors.

Do not convert failures into success.

Do not expose internal stack traces or unnecessary implementation details to external users.

Translate failures at appropriate boundaries while preserving internal diagnostic context.

Use explicit failure/unknown states when an outcome cannot safely be determined.

---

## 14. Validation

Treat external input as untrusted.

Validate at system boundaries.

Frontend validation is for usability and must not replace server-side validation.

Security-sensitive validation must fail closed.

Invalid state should normally be rejected rather than silently repaired.

---

## 15. Security

Security is part of code quality.

Code must respect applicable:

- authentication
- authorization
- object-level authorization
- tenant isolation
- environment isolation
- injection protection
- secret handling
- sensitive-data handling
- replay protection
- idempotency
- concurrency safety
- privilege boundaries

Never weaken a security requirement merely to simplify implementation.

Security-critical placeholder implementations are not acceptable as completed production code.

---

## 16. Secrets

Never:

- hardcode credentials
- commit credentials
- log credentials
- expose private keys
- expose tokens
- place secrets in audit events
- return secrets through inappropriate APIs

Use approved secret-management boundaries.

---

## 17. Persistence and Transactions

When working with persistent data, explicitly consider:

- transaction boundaries
- constraints
- locking
- concurrency
- race conditions
- retries
- idempotency
- consistency
- partial failure

Use database constraints to reinforce important invariants where appropriate.

Avoid N+1 query patterns and obviously unbounded data access.

Production schema changes must use the project's approved migration mechanism.

---

## 18. Distributed Systems

Never assume network operations execute exactly once.

When relevant, reason explicitly about:

- retries
- duplicate delivery
- timeout
- ordering
- partial failure
- race conditions
- idempotency
- unknown outcomes
- eventual consistency

Do not report success when the outcome is indeterminate.

---

## 19. Performance

Be performance-aware without premature optimization.

Avoid obvious problems such as:

- unbounded queries
- N+1 queries
- unnecessary network calls
- unnecessary serialization
- loading large datasets into memory
- resource leaks
- uncontrolled retries

Measure before introducing complicated optimization where practical.

---

## 20. Comments and Documentation

Prefer clear code over comments explaining confusing code.

Comments should primarily explain:

- why
- non-obvious constraints
- security reasoning
- protocol requirements
- important tradeoffs

Do not add comments that merely restate the code.

Do not leave stale TODOs.

Security-critical TODO placeholders are not acceptable in completed work.

---

## 21. Duplication and Abstraction

Avoid meaningful duplication.

However, do not create premature abstractions merely because two small implementations look similar.

A wrong abstraction is often more expensive than small duplication.

Create abstractions when a stable concept or boundary has emerged.

---

## 22. Language and Framework Conventions

Follow idiomatic practices for the language/framework being used.

Examples:

Java:
- cohesive classes
- constructor injection
- explicit domain/application boundaries

Go:
- small focused packages
- simple functions
- small interfaces defined where consumed
- explicit error handling

TypeScript/React:
- focused components/hooks
- explicit types
- separation of server state, UI state and domain behavior
- avoid giant page components

Test automation:
- readable fixtures
- reusable helpers only where meaningful
- deterministic setup/cleanup

Infrastructure:
- small scripts
- explicit configuration
- idempotent automation where appropriate
- fail visibly and safely

Language-specific conventions supplement this policy but may not weaken it.

---

## 23. Scope Discipline

Implement the assigned requirement.

Do not mix unrelated refactoring or future features into a task.

Do not build speculative capabilities.

If unrelated technical debt is discovered, report it separately unless fixing it is required for safe implementation.

---

## 24. Reviewability

Code should be structured so another engineer can review it confidently.

Keep pull requests focused where practical.

Use meaningful commits.

Explain non-obvious decisions.

Do not hide significant behavior in generated code, framework configuration, or implicit side effects.

---

## 25. Definition of Production-Quality Code

Production-quality code is not defined by the number of:

- classes
- patterns
- abstractions
- tests
- lines
- technologies

It is code that correctly satisfies its requirements while remaining:

- secure
- understandable
- maintainable
- testable
- diagnosable
- operationally safe

---

## 26. Review Enforcement

Independent Code Review must explicitly consider:

- responsibility/cohesion
- function/method complexity
- naming
- readability
- testability
- debuggability
- coupling
- duplication
- error handling
- logging
- security
- persistence behavior
- concurrency
- performance where relevant
- unnecessary abstractions
- scope discipline

"Tests pass" is not sufficient evidence of production quality.

Code that technically works but is unnecessarily:

- large
- confusing
- tightly coupled
- poorly named
- difficult to test
- difficult to debug
- excessively abstract
- operationally opaque

must receive CHANGES REQUIRED when the problem is material.

---

## 27. AI-Generated Code

AI-generated code is held to exactly the same standard as human-written code.

AI agents must not optimize for producing the most code.

They must optimize for producing the smallest clear implementation that safely satisfies the requirement.

AI agents must inspect existing code before creating new abstractions.

AI agents must not:

- fabricate tests
- fabricate execution results
- fabricate review evidence
- create unnecessary frameworks
- duplicate existing functionality without checking
- weaken requirements for convenience

Generated code must be understandable and maintainable by engineers who did not generate it.

---

## Core Principle

Our company-wide code standard is:

**Production-grade, cohesive, readable, well-named, testable, debuggable, explicit, secure, and simple.**

Optimize for clarity, correctness, cohesion, safety and maintainability — not architectural impressiveness.

## Policy hierarchy

This policy supplements:

- `policies/ENGINEERING_PRINCIPLES.md`
- `policies/SECURITY_PRINCIPLES.md`
- `policies/DEFINITION_OF_DONE.md`
- `policies/GIT_WORKFLOW.md`
- `policies/AI_AGENT_POLICY.md`

Security requirements override convenience or readability preferences when they conflict.

Product-specific architecture and requirements MAY specialize this policy. They MUST NOT silently weaken its quality expectations.
