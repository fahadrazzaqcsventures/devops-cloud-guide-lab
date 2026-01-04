# ADR: Selection of Proxmox as Hypervisor Platform

## ADR ID

ADR-PLX-ARCH-001

## Status

Accepted

## Context

A hypervisor platform was required to support a long-term DevOps and Cloud home lab with the following constraints:

* Limited hardware (single host + Raspberry Pi)
* Need for realistic, production-like virtualization
* Strong networking and storage visibility
* Support for automation and infrastructure-as-code concepts
* Minimal licensing cost

The platform would form the **control plane** for all subsequent learning and experiments.

---

## Decision

Proxmox VE was selected as the primary hypervisor and virtualization platform for the home lab.

---

## Rationale

Proxmox was chosen because it provides:

* Native support for **KVM** (VMs) and **LXC** (containers)
* Enterprise-grade features (clustering, storage, networking) without licensing barriers
* Strong Linux alignment (Debian-based)
* First-class support for bridges, VLANs, and advanced networking
* Compatibility with **Terraform providers** and automation tools
* Excellent observability into compute, storage, and network layers

This makes Proxmox ideal for learning **platform engineering concepts**, not just virtualization.

---

## Consequences

### Positive

* Realistic production-like control plane
* Full visibility into infrastructure layers
* Enables future HA, clustering, and IaC experiments

### Negative

* Single-node setup lacks true HA initially
* Requires careful change management on the host

---

## Alternatives Considered

* **VMware ESXi** – Rejected due to licensing and ecosystem constraints
* **VirtualBox** – Rejected due to limited networking realism
* **Cloud-only labs** – Rejected due to cost and reduced low-level control

---

## Scope

Applies to all virtualization workloads in the home lab.

---

**Decision Type:** Platform Selection
**Phase:** Week 1 – Foundations
