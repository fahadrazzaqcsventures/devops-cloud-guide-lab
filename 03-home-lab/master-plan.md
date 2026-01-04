# DevOps Home Lab Master Plan (theory + Labs + Incidents)

Each week explicitly defines:

1. **What theory to study (why)**
2. **What to build (how)**
3. **What to break (failure engineering)**
4. **How to respond (incident response & SRE thinking)**
5. **What to document (portfolio signal)**

This is written to train you as a **production operator and architect**, not a tool user.

---

## PHASE A — FOUNDATIONS & SYSTEM THINKING (WEEK 1–4)

### WEEK 1 — Virtualization & Control Plane (Proxmox)

**Theory (Study First)**

* What a hypervisor is (Type 1 vs Type 2)
* Why clouds virtualize compute
* Bare metal vs VM vs container
* Linux boot process (high level)
* Networking bridges vs switches

**Lab Build**

* Proxmox baseline setup on old laptop
* Storage pools (thin provisioning)
* vmbr0 (LAN), vmbr1 (internal), vmbr2 (DMZ)
* SSH key-based access

**Break It (Failures)**

* Break vmbr0 → lose network
* Break SSH access

**Incident Response**

* Console access recovery
* Validate bridges, restart networking
* Document exact commands used

**Portfolio Output**

* Proxmox architecture + recovery runbook

---

### WEEK 2 — Linux Server Fundamentals

**Theory**

* OS responsibilities
* Users vs processes
* systemd and service lifecycle
* Filesystems, permissions, logs

**Lab Build**

* Ubuntu Server VM (linux-core-01)
* Users, groups, sudo
* Nginx installation
* Journald + log locations

**Break It**

* chmod/chown incorrectly
* Stop nginx
* Fill disk to 100%

**Incident Response**

* Diagnose with journalctl, df, systemctl
* Restore service

**Portfolio**

* Linux service recovery runbook

---

### WEEK 3 — Networking & DNS (Raspberry Pi)

**Theory**

* DNS resolution flow
* Why DNS outages break everything
* Static vs dynamic IPs

**Lab Build**

* Raspberry Pi as DNS node
* Pi-hole/CoreDNS
* Point all VMs to Pi DNS

**Break It**

* Stop DNS service
* Wrong resolv.conf

**Incident Response**

* Trace name resolution failure
* Restore DNS

**Portfolio**

* DNS dependency diagram

---

### WEEK 4 — Firewalls & Network Isolation

**Theory**

* East–west vs north–south traffic
* Firewalls vs security groups

**Lab Build**

* Internal-only VM networks
* ufw / iptables rules

**Break It**

* Lock out SSH
* Break routing

**Incident Response**

* Console-based recovery

**Portfolio**

* Network troubleshooting notes

---

## PHASE B — AUTOMATION & CONTAINERS (WEEK 5–8)

### WEEK 5 — Bash Automation

**Theory**

* Idempotency
* Why automation fails in production

**Lab Build**

* User creation scripts
* Backup scripts
* Log cleanup scripts

**Break It**

* Wrong permissions
* Partial execution

**Incident Response**

* Defensive scripting fixes

**Portfolio**

* Bash automation repo

---

### WEEK 6 — Python Automation

**Theory**

* Why Python over Bash
* Error handling & logging

**Lab Build**

* Health-check scripts
* API calls (local services / MinIO)

**Break It**

* API timeout
* Bad credentials

**Incident Response**

* Retry logic, logging fixes

**Portfolio**

* Python automation toolkit

---

### WEEK 7 — Docker Fundamentals

**Theory**

* Containers vs VMs
* Image immutability

**Lab Build**

* Docker install
* Multi-stage builds
* Docker Compose

**Break It**

* Missing env vars
* Port conflicts

**Incident Response**

* docker logs, inspect

**Portfolio**

* Containerized app repo

---

### WEEK 8 — Container Operations

**Theory**

* Why containers fail in prod

**Lab Build**

* Registry usage
* Logging setup

**Break It**

* Crash loops
* Image bloat

**Incident Response**

* Optimize Dockerfile

**Portfolio**

* Container ops guide

---

## PHASE C — CLOUD MINDSET & CI/CD (WEEK 9–12)

### WEEK 9 — On-Prem as Cloud

**Theory**

* Cloud abstraction layers
* Shared Responsibility Model

**Lab Build**

* Map Proxmox → AWS EC2/VPC concepts

**Break It**

* Public exposure simulation

**Incident Response**

* Security remediation

**Portfolio**

* Cloud mental model doc

---

### WEEK 10 — CI/CD

**Theory**

* CI vs CD failures

**Lab Build**

* Jenkins or GitHub Actions

**Break It**

* Pipeline failure
* Secret exposure

**Incident Response**

* Secure pipeline fix

**Portfolio**

* CI/CD repo

---

### WEEK 11 — Deployment Safety

**Theory**

* Blue/green vs canary

**Lab Build**

* Safe deployments

**Break It**

* Bad deploy

**Incident Response**

* Rollback

**Portfolio**

* Deployment docs

---

### WEEK 12 — Infrastructure as Code

**Theory**

* Declarative infra

**Lab Build**

* Terraform + Proxmox

**Break It**

* State corruption

**Incident Response**

* State recovery

**Portfolio**

* IaC repo

---

## PHASE D — KUBERNETES & GITOPS (WEEK 13–18)

(Weeks 13–18 continue same pattern: theory → build → break → respond → document)

Includes:

* k3s/kubeadm cluster (Laptop + Pi)
* Workloads, scaling, Helm, Argo CD
* Node failures, CrashLoopBackOff, drift

---

## PHASE E — OBSERVABILITY & SRE (WEEK 19–22)

Includes:

* Prometheus, Grafana, logging
* Alert fatigue simulation
* Multi-component outages
* Blameless postmortems

---

## PHASE F — SENIOR CAPSTONE (WEEK 23–26)

**Outcome**

* Full platform rebuilt from code
* DR simulation
* Cost + reliability tradeoffs
* Interview-ready incident stories

---

## FINAL RULE

You do **not progress weeks by finishing builds**.
You progress by:

* Breaking systems
* Recovering calmly
* Explaining *why* choices were made

This is how senior DevOps engineers are formed.
