# Engineering Operating System

This repository is the company's reusable engineering governance system.

It defines how humans and AI agents design, implement, review, secure, validate, and release software. It is not an application repository and is not specific to any one product.

Future products adopt these policies, agent roles, skills, templates, and workflows. Product source code, schemas, and APIs live in product repositories.

---

## Purpose

The company is AI-first and human-controlled.

AI agents do most of the engineering work. Humans keep authority over product direction, production releases, security exceptions, major architecture, critical risk acceptance, and production credentials.

This repository exists to make that model explicit, repeatable, and hard to accidentally bypass.

It does **not** make the company certified, compliant, or secure by itself. Security and quality come from evidence produced while building products.

---

## What This Repository Contains

| Area | Location | Purpose |
| --- | --- | --- |
| Constitution | [AGENTS.md](AGENTS.md) | Non-negotiable rules for every AI agent |
| Policies | [policies/](policies/) | Engineering, security, AI, definition of done, git, and release rules |
| Agents | [agents/](agents/) | Role definitions, authority, and handoff contracts |
| Skills | [skills/](skills/) | Repeatable procedures for common workflows |
| Templates | [templates/](templates/) | Task, review, PR, and release artifacts |

---

## Operating Model

```text
                 Founder / Product Owner
                         |
                         v
                  Chief of Staff
                         |
                         v
                    Architect
                         |
              +----------+----------+
              |                     |
              v                     v
           Backend               Frontend
              |                     |
              +----------+----------+
                         |
                         v
                         QA
                         |
                         v
                Security if required
                         |
                         v
                    Code Review
                         |
                         v
                  Chief of Staff
                         |
                         v
                  Release Ready
                         |
                         v
                Human Approval
                         |
                         v
                   Platform/SRE
                         |
                         v
                    Production
```

Implementation MAY happen in parallel when architecture and contracts permit it.

No AI agent owns the entire lifecycle.

---

## Responsibilities

| Role | Authority |
| --- | --- |
| Founder / Product Owner | WHAT gets built, priorities, final product decisions, production release approval |
| [Chief of Staff](agents/chief-of-staff.md) | WHO works, WHEN work moves, coordination, gates, release-readiness reporting |
| [Architect](agents/architect.md) | HOW the system is designed |
| [Backend Engineer](agents/backend-engineer.md) | Server-side implementation within approved architecture |
| [Agent Engineer](agents/agent-engineer.md) | Customer-side/edge agent implementation within approved architecture |
| [Frontend Engineer](agents/frontend-engineer.md) | User-facing implementation within approved architecture |
| [QA Engineer](agents/qa-engineer.md) | Independent verification of behavior |
| [Security Engineer](agents/security-engineer.md) | Independent security evaluation |
| [Code Reviewer](agents/code-reviewer.md) | Independent quality and compliance review |
| [Platform / SRE](agents/platform-engineer.md) | Infrastructure, CI/CD, operational readiness, and deployment after approval |

The Chief of Staff coordinates gates and MUST NOT waive them.

---

## Policy Hierarchy

When documents conflict, use this order:

1. Explicit human decision within allowed governance boundaries
2. [AGENTS.md](AGENTS.md) non-negotiable rules
3. [Security policies](policies/SECURITY_PRINCIPLES.md)
4. Other engineering policies
5. Product-specific architecture and rules
6. Agent-specific instructions
7. Skill procedures
8. Individual task instructions

Human requests for unsafe or destructive production operations still require explicit confirmation and applicable safeguards.

If two documents conflict, agents MUST escalate rather than silently choosing the easier path.

---

## Key Policies

- [Engineering Principles](policies/ENGINEERING_PRINCIPLES.md)
- [Security Principles](policies/SECURITY_PRINCIPLES.md)
- [AI Agent Policy](policies/AI_AGENT_POLICY.md)
- [Definition of Done](policies/DEFINITION_OF_DONE.md)
- [Git Workflow](policies/GIT_WORKFLOW.md)
- [Release Policy](policies/RELEASE_POLICY.md)

---

## Skills

Skills are procedures, not optional suggestions.

- [Task orchestration](skills/task-orchestration/SKILL.md)
- [Feature development](skills/feature-development/SKILL.md)
- [Security review](skills/security-review/SKILL.md)
- [QA validation](skills/qa-validation/SKILL.md)
- [Code review](skills/code-review/SKILL.md)
- [Threat model](skills/threat-model/SKILL.md)
- [Database migration](skills/db-migration/SKILL.md)
- [Release](skills/release/SKILL.md)

---

## Task Lifecycle

```text
BACKLOG
→ READY
→ IN PROGRESS
→ QA
→ SECURITY (when required)
→ REVIEW
→ RELEASE READY
→ RELEASED
```

Additional states: `BLOCKED`, `REJECTED`, `CANCELLED`.

The Chief of Staff selects the workflow from policy and risk level. Mandatory gates cannot be skipped because a date is near or a model is confident.

See [skills/task-orchestration/SKILL.md](skills/task-orchestration/SKILL.md).

---

## Review Pipeline

```text
Product Owner
→ Chief of Staff
→ Architect when architecture is required
→ Implementation Agent(s)
→ QA
→ Security when required
→ Code Reviewer
→ Chief of Staff release-readiness check
→ Human production approval
→ Platform/SRE deployment
```

Failure at any mandatory gate returns the work to the appropriate earlier stage.

---

## Human Approval Boundaries

Humans MUST approve or explicitly accept:

- production deployments
- destructive production operations
- production credentials and secret-management changes
- security exceptions and accepted CRITICAL or HIGH residual risk
- major architectural changes
- changes to mandatory engineering gates
- product direction and business priorities

General coding agents MUST NOT hold unrestricted production credentials.

---

## Technology-Selection Philosophy

Technology choice follows product requirements, not agent preference.

The organization can support multiple stacks. Backend agents MUST be capable of Java/Spring Boot and TypeScript/Node.js because those stacks are expected for early products. That capability does not make either stack mandatory for every future product.

A single product SHOULD minimize languages and frameworks unless there is a concrete benefit. Unnecessary polyglot systems are a defect.

The Architect SHOULD record major technology decisions as ADRs in the product repository.

---

## Modular Monolith Before Microservices

Microservices are a supported capability, not the default architecture.

New products SHOULD start as a modular monolith unless concrete requirements justify independent services. "Future scale" is not sufficient justification.

Every proposed service boundary MUST have a documented reason and Architect approval.

Do not create `auth-service`, `user-service`, `audit-service`, or `notification-service` merely because those concepts exist.

---

## Risk-Based Rigor

The system is:

- **fast** for LOW-risk changes
- **rigorous** for HIGH-risk changes
- **very strict** for production, security, and destructive changes

Risk levels and required gates are defined in [policies/AI_AGENT_POLICY.md](policies/AI_AGENT_POLICY.md).

---

## How a New Product Adopts These Standards

1. Create the product repository. Do not copy application code into this repository.
2. Add this repository as the engineering baseline by submodule, subtree, vendor copy, or documented remote reference.
3. Point the product `AGENTS.md` at this constitution and add only product-specific deltas.
4. Record the initial architecture and technology decisions in the product repository.
5. Use the templates in [templates/](templates/) for tasks, PRs, security reviews, and releases.
6. Route work through the agent roles and skills defined here.
7. Keep product secrets, infrastructure state, and application code out of this repository.

Product-specific rules MAY tighten these standards. They MUST NOT silently weaken mandatory gates.

---

## Templates

- [Feature task](templates/feature-task.md)
- [Bug task](templates/bug-task.md)
- [Pull request](templates/pull-request.md)
- [Security review](templates/security-review.md)
- [Release checklist](templates/release-checklist.md)

---

## Hosting Note

The company's first products are expected to run on VPS infrastructure. Practices in this repository stay provider-neutral. Provider-specific runbooks belong in product or infrastructure repositories, not in company-wide policy.

---

## What This Repository Does Not Claim

This operating system does not claim SOC 2, ISO 27001, HIPAA, PCI DSS, GDPR certification, or any other compliance status.

It also does not claim that a product is secure merely because these files exist.
