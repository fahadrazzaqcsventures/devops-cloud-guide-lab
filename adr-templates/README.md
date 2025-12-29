# Architecture Decision Record (ADR) Templates

These templates help document **design decisions, trade-offs, and rationale** for your DevOps home lab, infrastructure, and lab exercises. Each ADR should be versioned in GitHub alongside your lab projects.

---

## 1. Basic ADR Template

```
# [ADR #] [Title]

## Status
Proposed / Accepted / Deprecated / Superseded

## Context
Explain the background of the decision. Why is this decision necessary? Include any constraints, requirements, or problems that prompted it.

## Decision
Describe the decision made. Include the technology, tool, or architecture pattern chosen.

## Alternatives Considered
List other options considered and why they were rejected.

## Consequences
Describe the expected impact of the decision: positive and negative, technical debt, operational implications, cost, and maintenance.

## Related Artifacts
- Link to design diagrams
- Related playbooks
- Related Terraform/Ansible scripts

## Date
YYYY-MM-DD

## Author
Your Name
```

---

## 2. ADR Template for Home Lab Week (Week-Specific)

```
# [ADR #] [Week #] [Decision Title]

## Status
Proposed / Accepted / Deprecated / Superseded

## Context
What are you trying to achieve this week in your lab? Why is this decision necessary? Reference relevant theory.

## Decision
What infrastructure, configuration, or approach did you choose?

## Alternatives Considered
- Option 1: Reason rejected
- Option 2: Reason rejected

## Failure Scenarios Considered
Document potential failures and mitigations.

## Consequences / Observations
- Operational consequences
- Lessons learned during lab
- Impact on subsequent weeks

## Related Artifacts
- Scripts
- YAML files
- Diagrams
- Incident response notes

## Date
YYYY-MM-DD

## Author
Your Name
```

---

## 3. ADR Template for Cloud / IaC Decisions

```
# [ADR #] [Cloud/IaC Decision Title]

## Status
Proposed / Accepted / Deprecated / Superseded

## Context
Business/learning goal, infrastructure context, and constraints

## Decision
- Tool (Terraform, Ansible, etc.)
- Cloud resources selected
- Configuration choices

## Alternatives Considered
- Other IaC tools
- Manual provisioning
- Different resource types or regions

## Failure Scenarios
- State corruption
- Resource misconfiguration
- Cost overruns

## Consequences
- Impact on reproducibility, reliability, cost
- Notes for recovery

## Related Artifacts
- Terraform scripts
- Diagrams
- Test/validation results

## Date
YYYY-MM-DD

## Author
Your Name
```

---

**Usage Guidelines:**

1. Create a new ADR for every major design decision.
2. Reference ADRs in lab documentation and incident playbooks.
3. Keep ADRs version-controlled in GitHub to show rationale evolution.
4. Use ADRs to justify architecture choices during interviews and portfolio reviews.
