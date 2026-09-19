# Skill Name

Security Review

# Purpose

Independently determine whether a change is safe enough to proceed, and record findings that can be reproduced and verified.

# When to Use

Use this skill when:

- risk is HIGH or CRITICAL
- a security review trigger in [../../policies/SECURITY_PRINCIPLES.md](../../policies/SECURITY_PRINCIPLES.md) applies
- QA or Code Review discovered a trust-boundary issue
- a security exception is being prepared for a human

# Required Inputs

- Task, PR, and risk level
- Implementation handoff
- Architecture or threat-model notes when they exist
- [../../templates/security-review.md](../../templates/security-review.md)

# Preconditions

- The reviewer is not acting as the only approver of their own material fix.
- Required source, config, and test evidence are available.
- Production systems are not being probed without explicit human authorization.

# Procedure

1. Confirm the change and the assets it touches.
2. Identify trust boundaries, actors, and entry points.
3. Review the following areas:

- authentication
- authorization
- tenant isolation
- injection
- secrets
- logging
- input validation
- output exposure
- rate limiting where applicable
- data exposure
- dependencies
- network boundaries
- privilege escalation
- CSRF
- SSRF
- auditability
- service-to-service trust where applicable

4. Attempt reproduction of suspected issues in an authorized non-production environment.
5. Write findings in the required format.
6. Issue one of:

- `PASS`
- `FAIL`
- `PASS WITH NON-BLOCKING FINDINGS`

7. If the implementer remediates a material finding, require independent verification. Do not self-approve that finding.

Unresolved CRITICAL or HIGH findings MUST block release unless explicitly accepted by the human authority under [../../policies/AI_AGENT_POLICY.md](../../policies/AI_AGENT_POLICY.md).

# Validation

- Every applicable check is `PASS`, `FAIL`, or `N/A` with a reason
- Findings include ID, severity, attack path, reproduction, impact, remediation, and verification method
- Verdict matches the highest unresolved blocking severity
- No secrets appear in the review artifact

# Failure Conditions

- Review claimed without inspecting the change
- Reproduction fabricated
- HIGH or CRITICAL finding downgraded without reason
- Silent fix plus self-approval
- Release allowed with unaccepted blocking findings

# Required Evidence

- Completed security-review template
- Reproduction notes or test output
- File list reviewed
- Exception record if a human accepted residual risk

# Output / Handoff

```text
STATUS:
COMPLETED / BLOCKED / REJECTED / NEEDS REVIEW

TASK:
Task identifier

SUMMARY:
PASS / FAIL / PASS WITH NON-BLOCKING FINDINGS

FILES:
Review artifact and files inspected.

DECISIONS:
N/A items and referenced exceptions.

TESTS:
Reproductions or security tests actually executed.

RISKS:
Residual risks.

SECURITY:
Findings and release-blocking status.

BLOCKERS:
Missing evidence or decisions.

NEXT:
Implementation agent, Code Reviewer, Chief of Staff, or human Product Owner.

EVIDENCE:
Links to the review document and real command output.
```
