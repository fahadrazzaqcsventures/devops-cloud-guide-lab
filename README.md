# DevOps & Cloud Guide + Home Lab

Welcome to the **DevOps Cloud Guide Lab** — a comprehensive, production‑oriented learning repository designed to take you from **zero experience to senior DevOps / Cloud / Platform Engineer level**.

This repository intentionally combines **theory, hands‑on labs, failure injection, incident response, and architectural decision documentation** — the same disciplines used by mature engineering organizations.

---

![AWS](https://img.shields.io/badge/AWS-Cloud-orange?logo=amazonaws\&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-System%20Administration-black?logo=linux)
![Docker](https://img.shields.io/badge/Docker-Containers-blue?logo=docker)
![Kubernetes](https://img.shields.io/badge/Kubernetes-Orchestration-blue?logo=kubernetes)
![Terraform](https://img.shields.io/badge/Terraform-IaC-purple?logo=terraform)
![Ansible](https://img.shields.io/badge/Ansible-Configuration%20Management-red?logo=ansible)
![CI/CD](https://img.shields.io/badge/CI%2FCD-Automation-success)

---

## Who This Repository Is For

* Aspiring **DevOps Engineers / Platform Engineers**
* **Cloud Engineers** (AWS‑focused, multi‑cloud aware)
* **Site Reliability Engineers (SREs)**
* System Administrators transitioning into DevOps

This repository assumes **curiosity, discipline, and consistency**, not prior expertise.

---

## Repository Structure (Authoritative)

```
/devops-cloud-guide-lab/
│
├── README.md                     # You are here
│
├── 01-roadmap/                   # End‑to‑end DevOps → Senior roadmap
│   └── README.md
│
├── 02-theory/                    # All conceptual foundations
│   ├── 00-foundations/
│   │   ├── 01-internet-and-application-basics/
│   │   └── 02-os-fundamentals/
│
├── 03-home-lab/                  # Week‑by‑week hands‑on lab execution
│   └── week-01-proxmox-baseline/
│       ├── README.md
│       ├── 01-build/
│       ├── 02-incidents/
│       └── docs/
│           ├── incidents-reports/
│           ├── incidents-responses/
│           ├── decisions/
│           ├── runbooks/
│           └── adrs/
│
├── templates/                    # Canonical documentation templates
│   ├── README.md
│   ├── adr-template.md
│   ├── decision-template.md
│   ├── incident-report-template.md
│   ├── incident-response-template.md
│   └── runbook-template.md
```

---

## Core Learning Workflow (Non‑Negotiable)

Every topic and every week follows the same **senior‑engineering loop**:

**theory → build → break → respond → document**

1. **Theory** — Study concepts in `02-theory/` aligned to the roadmap
2. **Build** — Execute labs in `03-home-lab/`
3. **Break** — Inject controlled failures intentionally
4. **Respond** — Recover using calm, methodical diagnosis
5. **Document** — Produce incidents, responses, runbooks, and ADRs

If documentation is missing, the work is **not complete**.

---

## What Each Major Section Is For

### 1. `01-roadmap/`

Defines the **full journey** from beginner to senior DevOps / Cloud Architect.

Use this to:

* Understand skill dependencies
* See how tools map to engineering problems
* Avoid random learning

---

### 2. `02-theory/`

All conceptual learning, written to support **real systems**, not exams:

* Internet, applications, and system thinking
* Operating systems and Linux internals
* Networking, scalability, reliability
* Containers, cloud, Kubernetes, observability

**Rule:** Never build before understanding the theory.

---

### 3. `03-home-lab/`

The heart of the repository.

Each week contains:

* Explicit build steps
* Planned failure scenarios
* Mandatory documentation outputs

Example:

* Week 01 — Proxmox control plane, storage, networking, SSH hardening

Future weeks extend into:

* Linux VM operations
* Networking & DNS
* Automation & CI/CD
* Kubernetes & GitOps
* Observability & SRE

---

### 4. `templates/`

Standardized templates for professional documentation:

* Incident reports
* Incident responses
* Decisions
* Runbooks
* Architectural Decision Records (ADRs)

Using templates enforces **clarity, consistency, and senior‑grade thinking**.

---

## Expected Outcomes

By completing this repository, you will:

* Think in **systems**, not tools
* Operate Linux, networking, and cloud platforms confidently
* Recover from outages without panic
* Explain and justify architectural decisions
* Possess a **real, reviewable DevOps portfolio**

This is the difference between *knowing tools* and *being an engineer*.

---

## Core Philosophy (Read This Twice)

* DevOps is **engineering**, not automation scripts
* Control planes fail — design and operate accordingly
* Failure is a **training mechanism**, not a mistake
* Documentation is part of the system
* Git is your **single source of truth**
* Depth beats breadth

---

## Author

**Fahad**
Aspiring DevOps & Cloud Engineer

Focused on building production‑grade systems through disciplined learning, failure‑driven practice, and documentation‑first engineering.
