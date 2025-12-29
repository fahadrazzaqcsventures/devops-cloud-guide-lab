# Weekly Incident Response Mapping

This document now maps each incident response playbook to the **week-by-week unified home lab plan**, ensuring every weekly lab exercise has a corresponding step-by-step recovery guide.

---

## PHASE A — Foundations & System Thinking (Weeks 1–4)

### Week 1 — Proxmox / Virtualization

* **Playbooks:** SSH lockout, network bridge misconfiguration, VM power failure
* **Usage:** Follow when initial Proxmox setup breaks; record commands and recovery steps in portfolio.

### Week 2 — Linux VM Fundamentals

* **Playbooks:** Linux service failure, disk full, permissions errors
* **Usage:** Apply when Nginx/systemd fails or permissions prevent log access.

### Week 3 — DNS / Raspberry Pi

* **Playbooks:** DNS resolution failure, network misrouting
* **Usage:** Use when Pi DNS fails or VMs cannot resolve hostnames.

### Week 4 — Networking / Firewalls

* **Playbooks:** SSH lockout, blocked network traffic
* **Usage:** Use when firewall or internal network isolation causes service inaccessibility.

---

## PHASE B — Automation & Containers (Weeks 5–8)

### Week 5 — Bash Automation

* **Playbooks:** Script execution failure, permission denied
* **Usage:** Apply when scripts fail due to misconfiguration.

### Week 6 — Python Automation

* **Playbooks:** API call failure, dependency errors
* **Usage:** Apply for failed automation scripts or incorrect environment setup.

### Week 7 — Docker Fundamentals

* **Playbooks:** Container crash, port collisions, missing environment variables
* **Usage:** Apply when Docker container fails to start or communicate.

### Week 8 — Container Operations

* **Playbooks:** Container exit, volume mount issues, logging misconfiguration
* **Usage:** Apply when operational issues appear in multi-container deployments.

---

## PHASE C — Cloud Mindset & CI/CD (Weeks 9–12)

### Week 9 — On-Prem as Cloud

* **Playbooks:** Public access exposure, simulated security breach
* **Usage:** Apply when security misconfiguration exposes services.

### Week 10 — CI/CD Pipelines

* **Playbooks:** Pipeline failure, secret leak
* **Usage:** Apply when Jenkins/GitHub Actions pipelines fail or misdeploy.

### Week 11 — Deployment Safety

* **Playbooks:** Failed deployment, rollback required
* **Usage:** Apply when deployments trigger service downtime.

### Week 12 — Infrastructure as Code

* **Playbooks:** State corruption, accidental destroy
* **Usage:** Apply when Terraform configurations fail or destroy critical VMs.

---

## PHASE D — Kubernetes & GitOps (Weeks 13–18)

### Weeks 13–18 — Cluster, Workloads, Helm, Argo CD

* **Playbooks:** Pod CrashLoopBackOff, Node NotReady, Helm upgrade failure, GitOps drift
* **Usage:** Apply to any Kubernetes or GitOps failure scenario in cluster management and deployments.

---

## PHASE E — Observability & SRE (Weeks 19–22)

### Weeks 19–22 — Metrics, Alerting, Logging, Incident Simulation

* **Playbooks:** Metrics loss, alert noise, log pipeline failure, multi-component outages
* **Usage:** Apply during monitoring setup or SRE exercises; simulate multi-failure events and practice blameless postmortems.

---

## PHASE F — Senior Capstone (Weeks 23–26)

### Weeks 23–26 — Full Platform Rebuild, DR Simulation

* **Playbooks:** Multi-service outage, DR scenario, region outage simulation
* **Usage:** Apply for comprehensive failure testing and platform recovery; document all mitigation strategies and lessons learned.

---

**Instructions:**

* Each week, before performing lab tasks, read the mapped playbooks.
* During failures, strictly follow playbook steps.
* Document every recovery action and outcome in GitHub portfolio.
* Use postmortems to reinforce learning and senior-level decision-making.
