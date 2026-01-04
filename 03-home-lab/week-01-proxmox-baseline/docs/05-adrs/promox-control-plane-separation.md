# ADR: Proxmox Control Plane Separation

## ADR ID

ADR-2025-W1-CP-01

## Title

Separation of Control Plane and Data Plane in Proxmox

## Status

Accepted

## Context

Need to validate whether Proxmox control plane availability affects VM execution.

## Decision

Accept Proxmox architecture where management services are decoupled from VM runtime.

## Alternatives Considered

* Single-plane systems where UI outage implies workload outage

## Consequences

### Positive

* Safe management operations
* Reduced blast radius

### Negative

* Requires operators to understand service boundaries

## Validation

Confirmed by stopping `pveproxy` without VM impact.
