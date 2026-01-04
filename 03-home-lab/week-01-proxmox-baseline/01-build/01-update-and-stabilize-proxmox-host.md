# Build Phase 1 – Update and Stabilize Proxmox Host

## Objective

Establish a **secure, predictable, and supportable baseline** for the Proxmox hypervisor before performing any further configuration or experimentation.

This step treats the Proxmox host as **production infrastructure**, not a lab toy.

---

## Purpose

* Ensure the host is running supported, up-to-date packages
* Reduce exposure to known bugs and security vulnerabilities
* Confirm clean boot behavior before network and VM changes
* Validate management-plane availability (Web UI)

---

## Preconditions

* Console or SSH access to Proxmox host
* Stable power source
* No active critical VM workloads

---

## Actions

### 1. Update Package Lists

```bash
apt update
```

**Why:**

* Refreshes metadata from configured repositories
* Ensures upgrades target correct package versions

---

### 2. Apply System Upgrades

```bash
apt upgrade -y
```

**Why:**

* Applies security patches and bug fixes
* Aligns system packages with current Proxmox release state

**Notes:**

* Monitor output for held or failed packages
* Do not interrupt the process

---

### 3. Reboot the Host Safely

```bash
reboot
```

**Why:**

* Ensures kernel and system service updates are fully applied
* Validates bootloader and system startup integrity

---

## Validation Checklist

After reboot, confirm the following:

* [x] Host boots without errors
* [x] Login prompt appears normally
* [x] Network interfaces come up
* [x] Proxmox Web UI is reachable via browser
* [x] No unexpected systemd service failures

Recommended verification commands:

```bash
systemctl --failed
ip a
```

---

## Expected Outcome

* Proxmox host boots cleanly
* Web UI is reachable
* Management plane is stable
* System is ready for controlled configuration changes

---

## Failure Awareness

Potential issues to watch for:

* Web UI not reachable after reboot
* Network interfaces renamed or missing
* Kernel panic or boot loop

If any occur, initiate the appropriate **Incident Response Playbook**.

---

## Documentation

* Record completion in Week 1 build checklist
* Reference this step in future ADRs as the **baseline requirement**

---

## Engineering Principle Reinforced

> Never build on an unstable or outdated control plane.

Stability precedes complexity.
