# ADR: Proxmox Storage Backend Selection

## ADR ID

ADR-PLX-STG-002

## Status

Accepted

## Context

The Proxmox host required a storage backend suitable for:

* VM disk images
* ISO storage
* Backups
* Predictable performance on HDD-based hardware

The host uses a single 500GB HDD with no dedicated SSD or RAID controller.

---

## Decision

Local storage using **LVM-Thin** for VM disks and **local directory storage** for ISOs and backups was selected.

---

## Rationale

This storage configuration was chosen because:

* LVM-Thin is Proxmox-native and well-documented
* Supports snapshots and thin provisioning
* Minimal operational complexity for a single-node setup
* Avoids filesystem corruption risks under heavy experimentation
* Closely mirrors storage patterns used in small-to-medium enterprises

ZFS was intentionally avoided due to memory constraints (8GB RAM) and HDD-only performance characteristics.

---

## Consequences

### Positive

* Predictable performance
* Simple recovery model
* Lower memory overhead

### Negative

* No native compression or checksumming
* Limited snapshot flexibility compared to ZFS

---

## Alternatives Considered

* **ZFS** – Rejected due to RAM requirements and HDD wear
* **Directory-only storage** – Rejected due to lack of snapshot support
* **Ceph** – Out of scope for single-node setup

---

## Scope

Applies to all VM and ISO storage on the Proxmox host.

---

**Decision Type:** Storage Architecture
**Phase:** Week 1 – Foundations
