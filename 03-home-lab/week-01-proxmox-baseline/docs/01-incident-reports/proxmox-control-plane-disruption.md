# Incident Report – Proxmox Control Plane Disruption

## Incident ID

INC-2025-W1-CP-01

## Summary

Proxmox web control plane became unavailable after intentionally stopping the `pveproxy` service.

## Severity

Low (Planned / Non-production)

## Impact

* Proxmox Web UI unreachable
* API access unavailable
* Running virtual machines were **not affected**

## Timeline

* Detection: Immediately after stopping `pveproxy`
* Response Start: Immediate
* Mitigation: Restarted service
* Resolution: UI restored

## Root Cause

Intentional shutdown of the Proxmox web proxy service (`pveproxy`).

## Trigger

Manual execution of:

```
sudo systemctl stop pveproxy
```

## Resolution

Restarted the service using systemd.

## Lessons Learned

Control plane availability is independent of VM execution (data plane).

## Follow-Up Actions

* Create a runbook for control plane outages
* Validate console access before UI changes
