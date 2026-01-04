# Incident Report – Network Lockout

## Incident ID

W1-NET-LOCKOUT-01

## Summary

Management access to the Proxmox host was lost due to network misconfiguration, resulting in SSH and Web UI unavailability.

## Impact

* Proxmox Web UI unreachable
* SSH access lost
* Running workloads unaffected (console access remained)

## Timeline

* Failure injected by disabling network bridge / misconfiguration
* Immediate loss of remote access
* Recovery performed via physical console

## Root Cause

Incorrect or unavailable network bridge configuration caused host isolation.

## Detection

Manual verification: inability to access Web UI and SSH.

## Resolution

Network configuration restored from console; services verified.

## Lessons Learned

* Network misconfiguration can fully isolate management planes
* Console access is a critical recovery path

## Severity

High (Management plane outage)

## Status

Resolved
