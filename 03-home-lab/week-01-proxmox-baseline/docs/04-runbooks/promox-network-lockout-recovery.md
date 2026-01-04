# Runbook – Proxmox Network Lockout Recovery

## Purpose

This runbook provides a **repeatable, step-by-step procedure** to recover a Proxmox host after a network lockout caused by bridge, IP, or firewall misconfiguration.

It is intended for **production-safe recovery** with minimal blast radius and zero VM downtime.

---

## When to Use This Runbook

Trigger this runbook when **any** of the following occur:

* Proxmox Web UI is unreachable
* SSH access to Proxmox host fails
* Host does not respond to ping on management IP
* Recent network or firewall changes were applied

---

## Preconditions

* Physical or console access to the Proxmox host is available
* You have root credentials for the host
* VMs may still be running (do NOT reboot unless required)

---

## Recovery Procedure

### Step 1: Access the Host via Console

* Use physical keyboard + monitor OR
* Use Proxmox local console access

**Goal:** Bypass network dependency entirely.

---

### Step 2: Confirm Host Is Running Normally

```bash
uptime
systemctl status pve-cluster
```

* Confirm system is stable
* Do NOT reboot unless system services are failing

---

### Step 3: Identify Active Network Interfaces

```bash
ip addr
ip link
```

* Identify physical NIC (e.g., `enp3s0`)
* Verify link state is UP

---

### Step 4: Inspect Network Configuration

```bash
cat /etc/network/interfaces
```

Check for:

* Correct bridge name (`vmbr0`)
* Correct physical NIC in `bridge_ports`
* Valid IP address, netmask, and gateway

---

### Step 5: Apply Minimal Known-Good Configuration

If configuration is suspect, restore a **minimal static bridge**:

```bash
auto vmbr0
iface vmbr0 inet static
    address <MANAGEMENT_IP>
    netmask <NETMASK>
    gateway <GATEWAY>
    bridge_ports <PHYSICAL_NIC>
    bridge_stp off
    bridge_fd 0
```

**Principle:** Restore access first. Optimize later.

---

### Step 6: Reload Networking Safely

Preferred method:

```bash
ifreload -a
```

Fallback:

```bash
systemctl restart networking
```

Watch console output for errors.

---

### Step 7: Validate Network Connectivity

```bash
ip route
ping <GATEWAY>
ping 8.8.8.8
```

* Confirm routing
* Confirm outbound connectivity

---

### Step 8: Restore Remote Access

From another machine:

* SSH into Proxmox host
* Access Proxmox Web UI

If successful, incident is resolved.

---

## Post-Recovery Actions

* Save known-good `/etc/network/interfaces`
* Document recent changes that caused failure
* Update ADR or network checklist if required

---

## What NOT to Do

* Do NOT reboot immediately
* Do NOT make multiple changes at once
* Do NOT optimize network config during recovery

---

## Escalation

Escalate only if:

* Console access is unavailable
* Physical NIC is down
* Disk or filesystem errors are present

---

## Outcome

* Management access restored
* VM uptime preserved
* Incident converted into institutional knowledge

---

## Runbook Status

Approved for reuse in future incidents.
