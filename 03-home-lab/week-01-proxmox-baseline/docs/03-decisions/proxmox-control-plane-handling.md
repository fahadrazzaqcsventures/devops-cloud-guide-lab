# Decision: Control Plane Service Handling

## Decision ID

DEC-2025-W1-CP-01

## Date

Week 1 Lab Execution

## Context

Proxmox web UI was unavailable due to stopped control plane service.

## Decision Made

Restart `pveproxy` immediately rather than rebooting the host.

## Rationale

* Faster recovery
* No impact on running VMs
* Confirms service-level isolation

## Risk

If multiple services were affected, partial recovery could mask deeper issues.

## Outcome

Service restored successfully without host reboot.
