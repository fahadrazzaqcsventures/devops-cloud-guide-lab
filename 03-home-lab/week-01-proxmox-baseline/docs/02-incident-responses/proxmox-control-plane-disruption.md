# Incident Response: Control Plane Disruption

## Response ID

RESP-2025-W1-CP-01

## Incident Reference

INC-2025-W1-CP-01

## Detection

Observed Proxmox Web UI was unreachable after stopping `pveproxy`.

## Initial Hypothesis

The control plane service was stopped, but VM workloads should remain unaffected.

## Actions Taken

1. Verified service state:

   ```bash
   systemctl status pveproxy
   ```

2. Confirmed VMs were still running via console access.
3. Restarted the service:

   ```bash
   systemctl start pveproxy
   ```

## Verification

* Web UI accessible
* API responding
* No VM interruption observed

## Communication

In a production environment, this would be communicated as a control-plane-only incident with no customer impact.

## Improvements

* Add health checks for control plane services
* Document recovery steps in a runbook
