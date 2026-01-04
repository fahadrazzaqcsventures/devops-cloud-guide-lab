# Application Support and Maintenance

This document defines what **application support and maintenance** actually mean in real-world DevOps and SRE roles.

Most outages are not caused by new features—they are caused by **poor maintenance, weak ownership, and lack of operational discipline**.

---

## 1. Why This Topic Matters

Junior engineers focus on *building*. Senior engineers focus on *keeping systems healthy over time*. DevOps is about **sustained reliability**.

---

## 2. Application Support

**Definition:**
The ongoing responsibility to:

* Keep applications running
* Detect issues early
* Respond to incidents
* Communicate status clearly

**Typical responsibilities:**

* Monitoring dashboards
* Alert response
* Log analysis
* Performance troubleshooting
* Incident coordination

---

## 3. Application Maintenance

**Definition:**
Proactive work to:

* Prevent future incidents
* Reduce technical debt
* Improve operability

**Typical activities:**

* OS and package updates
* Dependency upgrades
* Configuration cleanup
* Capacity planning
* Documentation updates

---

## 4. Reactive vs Proactive Operations

| Approach  | Description      | Risk |
| --------- | ---------------- | ---- |
| Reactive  | Fix when broken  | High |
| Proactive | Prevent failures | Low  |

Senior DevOps engineers operate primarily at **proactive L2-L3 levels**.

---

## 5. Support Levels (L1–L3)

* **L1:** Alert acknowledgement, basic restarts, escalation
* **L2:** Log/metric analysis, config checks, known issue resolution
* **L3:** Root cause analysis, code and architecture fixes, long-term remediation

---

## 6. SLIs, SLOs, SLAs

* **SLI:** Metric (latency, error rate)
* **SLO:** Target value
* **SLA:** Contractual commitment

Example:

* SLI: API availability
* SLO: 99.9%
* SLA: Financial penalties

---

## 7. Maintenance Windows

Planned downtime reduces risk and allows controlled changes. Unplanned changes increase incidents.

---

## 8. Documentation as an Operational Tool

Good documentation reduces MTTR, enables safe handovers, and prevents tribal knowledge loss.

Required docs:

* Runbooks
* Architecture diagrams
* Incident playbooks

---

## 9. Home Lab Mapping

Practice:

* Weekly patching cycles
* Planned service restarts
* Incident tickets and postmortems

> Lab is “done” only when it is maintainable.

---

## 10. You Should Now Clearly Understand

* Support and maintenance are **core DevOps responsibilities**
* Stability beats feature velocity
* Documentation is a critical operational asset
* Senior engineers design for operability and maintainability

---

## Next Theory Topic

[**Software Development Life Cycle (SDLC)**](../12-software-development-life-cycle/README.md)