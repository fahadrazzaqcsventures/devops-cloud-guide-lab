# ADR: Bridged Networking Configuration

## ADR ID

ADR-PLX-NET-003

## Status

Accepted

## Context

The home lab requires VMs to:

* Be reachable directly from the LAN
* Behave like real servers (not NAT-isolated instances)
* Support realistic networking failures and recoveries
* Enable future services such as load balancers, reverse proxies, and clusters

---

## Decision

Linux bridge networking (`vmbr0`) was selected as the primary Proxmox VM networking model.

---

## Rationale

Bridged networking was chosen because it:

* Places VMs directly on the physical network
* Avoids NAT complexity and hidden failure modes
* Enables realistic IP management and routing
* Mirrors how production hypervisors connect workloads
* Simplifies troubleshooting using standard Linux tools

This decision intentionally exposed the risk of network misconfiguration to enable real-world learning.

---

## Consequences

### Positive

* Production-like VM connectivity
* Realistic failure scenarios
* Direct LAN access

### Negative

* Misconfiguration can cause host lockout
* Requires strict change discipline

---

## Alternatives Considered

* **NAT networking** – Rejected due to reduced realism
* **Host-only networking** – Rejected due to isolation
* **SDN overlays** – Deferred to later phases

---

## Scope

Applies to all VM networking on the Proxmox host.

---

**Decision Type:** Network Architecture
**Phase:** Week 1 – Foundations
