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
└── week-02-...
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

* [Proxmox host baseline - Update and Stabilize Proxmox Host](./week-01-proxmox-baseline/01-build/01-update-and-stabilize-proxmox-host.md)
* [SSH Key-Based Access Hardening](./week-01-proxmox-baseline/01-build/02-ssh-key-based-access-hardening.md)
* [Proxmox Storage Validation](./week-01-proxmox-baseline/01-build/03-promox-storage-validation.md)
* [Proxmox Network Baseline - Network bridges (vmbr0)](./week-01-proxmox-baseline/01-build/04-promox-network-baseline.md)

**Failures Practiced**

* [Control Plane Disruption (pveproxy stopped)](./week-01-proxmox-baseline/02-incidents/01-proxmox-control-plane-disruption.md)
* [Network Lockout (bridge/firewall misconfiguration)](./week-01-proxmox-baseline/02-incidents/02-network-lockout-simulation.md)

**Documentation Produced**

* **Incident reports** - what broke

  * [Control Plane Disruption](./week-01-proxmox-baseline/docs/01-incident-reports/proxmox-control-plane-disruption.md)
  * [Network Lockout](./week-01-proxmox-baseline/docs/01-incident-reports/network-lockout.md)

* **Incident responses** - How it was fixed
  
  * [Control Plane Disruption](./week-01-proxmox-baseline/docs/02-incident-responses/proxmox-control-plane-disruption.md)
  * [Network Lockout](./week-01-proxmox-baseline/docs/02-incident-responses/promox-network-lockout.md)

* **Tactical decisions** - why specific actions were chosen

  * [Control Plane Service Handling](./week-01-proxmox-baseline/docs/03-decisions/proxmox-control-plane-handling.md)
  * [Network Lockout](./week-01-proxmox-baseline/docs/03-decisions/network-lockout.md)
  * [Directory vs LVM-Thin in Home Lab](./week-01-proxmox-baseline/docs/03-decisions/directory-vs-lvm-thin.md)

* **Runbooks** - how to recover next time without thinking
  * [Proxmox Control Plane Outage](./week-01-proxmox-baseline/docs/04-runbooks/proxmox-control-plane-outage.md)
  * [Proxmox Network Lockout Recovery](./week-01-proxmox-baseline/docs/04-runbooks/promox-network-lockout-recovery.md)
* **ADRs** - Architectural decisions

  * [Why Proxmox as hypervisor](./week-01-proxmox-baseline/docs/05-adrs/why-promox-as-a-hypervisor.md)
  * [Storage backend choice](./week-01-proxmox-baseline/docs/05-adrs/proxmox-storage-backend-selection.md)
  * [Bridged networking Configuration](./week-01-proxmox-baseline/docs/05-adrs/promox-bridged-networking-configuration.md)
  * [SSH hardening](./week-01-proxmox-baseline/docs/05-adrs/ssh-access-hardening-on-proxmox.md)
  * [Proxmox Control Plane Separation](./week-01-proxmox-baseline/docs/05-adrs/promox-control-plane-separation.md)
  * [Bridged Networking Configuration](./week-01-proxmox-baseline/docs/05-adrs/promox-network-change-safety.md)

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

### Week 03 — Networking & DNS *(Planned)*

**Build**

* Raspberry Pi DNS
* Internal name resolution

**Failures**

* DNS outage
* Misconfigured resolvers

**Docs**

* DNS architecture ADR
* Network incident runbooks

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
