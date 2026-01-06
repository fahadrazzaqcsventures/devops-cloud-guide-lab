# DevOps Home Lab

## Purpose

This home lab is a **production-grade learning and experimentation environment** designed to take you from **zero to senior DevOps / Cloud / Platform Engineer** through disciplined practice.

This is **not a demo lab**.
This is an **engineering training ground** where every build is followed by:

**theory → build → break → respond → document**

The lab intentionally introduces failures so you develop:

* Operational confidence
* Incident response muscle memory
* Architecture decision discipline
* Senior-level reasoning under failure

---

## Hardware Overview

* **Primary Proxmox Host**: Old laptop (i5 3rd gen, 8GB RAM, 500GB HDD)
* **Edge / Auxiliary Node**: Raspberry Pi 3 B+
* **Personal Laptop**: Daily driver (SSH, docs, GitHub)

Proxmox acts as the **control plane** for all lab infrastructure.

---

## Repository Structure (Home Lab Scope)

```
03-home-lab/
└── week-01-proxmox-baseline/
    ├── README.md                # Week overview (goals, outcomes)
    ├── 01-build/                # Step-by-step build execution
    ├── 02-incidents/             # Failure injection instructions
    └── docs/
        ├── incidents-reports/    # What broke
        ├── incidents-responses/  # How it was fixed
        ├── decisions/            # Tactical decisions made
        ├── runbooks/             # Future recovery guides
        └── adrs/                 # Architectural decisions
```

Templates for all documentation live in `/templates` and are reused consistently.

---

## How to Use This Lab (Mandatory Order)

Each week **must** be executed in this order:

1. **Study theory** (from `02-theory/`)
2. **Build infrastructure** (`01-build/`)
3. **Inject failures intentionally** (`02-incidents/`)
4. **Recover calmly and methodically**
5. **Document everything** (docs folders)

Skipping documentation means the week is **not complete**.

---

## Week-by-Week Lab Plan

### Week 01 — Proxmox Baseline & Control Plane

**What We Build**

* [Proxmox host baseline (Update and Stabilize Proxmox Host)](./01-build/01-update-and-stabilize-proxmox-host.md)
* [SSH Key-Based Access Hardening](./01-build/02-ssh-key-based-access-hardening.md)
* [Storage validation](./01-build/03-promox-storage-validation.md)
* [Proxmox Network Baseline](./01-build/04-promox-network-baseline.md)

**Failures Practiced**

* [Control Plane Disruption (pveproxy stopped)](./02-incidents/01-proxmox-control-plane-disruption.md)
* [Network Lockout (bridge/firewall misconfiguration)](./02-incidents/02-network-lockout-simulation.md)

**Documentation Produced**

* Incident reports
  * [Proxmox Control Plane Disruption](./docs/01-incident-reports/proxmox-control-plane-disruption.md)
  * [Network Lockout](./docs/01-incident-reports/network-lockout.md)

* Incident responses
  * [Control Plane Disruption](./docs/02-incident-responses/proxmox-control-plane-disruption.md)
  * [Network Lockout](./docs/02-incident-responses/promox-network-lockout.md)

* Tactical decisions
  * [Control Plane Service Handling](./docs/03-decisions/proxmox-control-plane-handling.md)
  * [Network Lockout](./docs/03-decisions/network-lockout.md)
  * [Directory vs LVM-Thin](./docs/03-decisions/directory-vs-lvm-thin.md)

* Runbooks
  * [Proxmox Control Plane Outage](./docs/04-runbooks/proxmox-control-plane-outage.md)
  * [Proxmox Network Lockout Recovery](./docs/04-runbooks/promox-network-lockout-recovery.md)

* ADRs

  * [Proxmox as hypervisor](./docs/05-adrs/why-promox-as-a-hypervisor.md)
  * [Storage backend choice](./docs/05-adrs/proxmox-storage-backend-selection.md)
  * [Proxmox Control Plane Separation](./docs/05-adrs/promox-control-plane-separation.md)
  * [Bridged networking](./docs/05-adrs/promox-bridged-networking-configuration.md)
  * [Proxmox Network Change Safety](./docs/05-adrs/promox-network-change-safety.md)
  * [SSH Access Hardening on Proxmox](./docs/05-adrs/ssh-access-hardening-on-proxmox.md)

---

### Week 02 — Linux VM Fundamentals *(Planned)*

**Build**

* First Ubuntu Server VM
* Users, permissions, systemd services

**Failures**

* Service not starting
* Permission denied
* Disk full

**Docs**

* Linux service recovery runbooks
* Permission failure incident reports

---

## Documentation Philosophy

| Document Type     | Purpose                                  |
| ----------------- | ---------------------------------------- |
| Incident Report   | Describe the failure objectively         |
| Incident Response | Exact recovery steps                     |
| Decision          | Why a specific action was chosen         |
| Runbook           | How to fix it next time without thinking |
| ADR               | Long-term architectural reasoning        |

This mirrors how senior engineers work in production.

---

## Completion Standard

A week is complete **only if**:

* You can explain every failure
* You can recover without panic
* You can rebuild from scratch
* You have documentation to prove it

---

## Final Note

This lab is intentionally uncomfortable.

That discomfort is what produces **real DevOps engineers**.
