# Runbook: Proxmox Control Plane Outage

## Purpose

Restore access to Proxmox management interface when the web control plane is unavailable.

## Scope

* Proxmox Web UI
* Proxmox API

## Preconditions

* Console or SSH access to host

## Symptoms

* Web UI unreachable
* API timeouts

## Verification Steps

```
systemctl status pveproxy
```

## Resolution Steps

1. Log in via console or SSH
2. Restart service:

   ```
   sudo systemctl start pveproxy
   ```
3. Verify status:

   ```
   systemctl status pveproxy
   ```

## Validation

* Web UI accessible
* No VM disruption

## Rollback

No rollback required; service restart is safe.

## Escalation

If service fails to start, inspect logs:

```
journalctl -u pveproxy
```

## Post-Incident Tasks

* Record incident
* Review access safeguards
