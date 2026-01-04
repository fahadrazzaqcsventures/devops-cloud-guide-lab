# Decision – Network Lockout

## Context

During Week 1 lab execution, the Proxmox host became unreachable due to a network bridge misconfiguration. All remote management access (SSH and Web UI) was lost. Virtual machines continued running, but the control plane was unavailable.

This document captures the **tactical decisions** made during the incident response.

---

## Decision 1: Use Console Access Instead of Further Remote Attempts

**Decision:**
Access the Proxmox host via local console (physical access) rather than attempting repeated remote recovery.

**Rationale:**

* Network-based recovery was impossible without management connectivity
* Console access provides guaranteed control regardless of network state
* Avoids compounding the issue with blind remote changes

**Alternatives Considered:**

* Waiting for network recovery (rejected: no automated rollback in place)
* Rebooting blindly (rejected: risk of worsening misconfiguration)

---

## Decision 2: Restore Minimal Known-Good Network Configuration First

**Decision:**
Apply a minimal, static, known-good vmbr0 configuration to restore connectivity before optimizing or expanding network setup.

**Rationale:**

* Primary goal was restoring management access, not perfect configuration
* Minimal config reduces failure surface
* Aligns with incident response principle: stabilize first, improve later

**Alternatives Considered:**

* Rebuilding full multi-bridge setup immediately (rejected: high risk)

---

## Decision 3: Restart Networking Instead of Rebooting Host

**Decision:**
Restart networking services using `ifreload -a` / `systemctl restart networking` instead of rebooting the Proxmox host.

**Rationale:**

* Reduced blast radius
* Faster recovery
* Preserved VM uptime

**Alternatives Considered:**

* Full system reboot (rejected: unnecessary downtime)

---

## Decision 4: Validate Connectivity Incrementally

**Decision:**
Validate recovery step-by-step (interface → route → gateway → internet) before declaring incident resolved.

**Rationale:**

* Prevents false positives
* Ensures root cause is fully addressed
* Matches production troubleshooting methodology

---

## Outcome

* Management access restored
* No VM downtime
* No data loss
* Root cause clearly identified

---

## Lessons Reinforced

* Network changes on hypervisors require extreme caution
* Always prefer reversible, minimal actions during incidents
* Console access is a non-negotiable recovery path

---

## Status

Decision record complete. This decision informed the creation of a permanent runbook.
