# ADR: Proxmox Network Change Safety

## ADR ID

ADR-PLX-NET-001

## Status

Accepted

## Context

During Week 1 lab execution, a network misconfiguration caused complete loss of management-plane access (Web UI and SSH) to the Proxmox host. Recovery required console access. This highlighted the risk of applying unvalidated network changes directly on the hypervisor.

## Decision

All network changes on the Proxmox host must follow a safe-change procedure:

* Maintain a documented, known-good network configuration
* Validate changes incrementally
* Ensure console access is available before applying changes
* Avoid experimental or dynamic networking on the hypervisor
* Treat the Proxmox host as immutable infrastructure where possible

## Rationale

* The hypervisor is a single point of failure for all workloads
* Network outages on the host have a higher blast radius than VM-level failures
* Console recovery is slower and riskier than validated change control

## Consequences

### Positive

* Reduced risk of full management-plane outages
* Faster recovery during incidents
* Clear operational discipline for future changes

### Negative

* Slightly slower iteration for network experimentation
* Additional documentation overhead

## Alternatives Considered

* Allow ad-hoc network experimentation on the host (rejected)
* Delegate all networking changes to VMs only (accepted where possible)

## Compliance

This ADR applies to all future Proxmox network changes in the home lab.

## Review

Re-evaluate if high-availability or redundant management access is introduced.
