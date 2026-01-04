# Build Phase 3.3 – Proxmox Network Baseline

## Phase

Week 1 – Foundations

## Objective

Establish a **known-good, documented, and recoverable network baseline** for the Proxmox host management plane.

This baseline becomes the **reference state** for all future networking changes, experiments, and incident recovery.

---

## Purpose

* Ensure stable management access (Web UI + SSH)
* Validate bridge-based networking fundamentals
* Minimize blast radius before VM provisioning
* Create a rollback-safe network configuration

---

## Preconditions

* Build Phase 1 (Host Update) completed
* Build Phase 2 (SSH Key based Access) completed
* Build Phase 3 (Storage Validation) completed
* Console access available

---

## Network Design (Baseline)

### Management Network Characteristics

* Single Linux bridge (`vmbr0`)
* One physical NIC attached
* Static IP for Proxmox host
* Default gateway configured
* No firewall rules applied yet

This is intentionally **simple and boring**.

---

## Actions

### 1. Identify Physical Network Interface

```bash
ip link
```

Identify the active NIC (e.g. `enp3s0`).

---

### 2. Review Existing Network Configuration

```bash
cat /etc/network/interfaces
```

Confirm or establish the baseline configuration.

---

### 3. Apply Known-Good Bridge Configuration

Example baseline configuration:

```bash
auto lo
iface lo inet loopback

iface <PHYSICAL_NIC> inet manual

auto vmbr0
iface vmbr0 inet static
    address <MANAGEMENT_IP>
    netmask <NETMASK>
    gateway <GATEWAY>
    bridge_ports <PHYSICAL_NIC>
    bridge_stp off
    bridge_fd 0
```

**Engineering principle:**
One bridge. One NIC. One purpose.

---

### 4. Reload Networking Safely

Preferred:

```bash
ifreload -a
```

Fallback:

```bash
systemctl restart networking
```

Monitor console output closely.

---

### 5. Validate Connectivity

On Proxmox host:

```bash
ip addr show vmbr0
ip route
ping <GATEWAY>
ping 8.8.8.8
```

From another machine:

* SSH to Proxmox
* Access Proxmox Web UI

---

## Validation Checklist

* [x] vmbr0 exists and is UP
* [x] Correct IP assigned
* [x] Default route present
* [x] Gateway reachable
* [x] Web UI reachable
* [x] SSH reachable

---

## Expected Outcome

* Stable management-plane connectivity
* Documented baseline network state
* Confidence to proceed with VM creation

---

## Failure Awareness

Common failure modes:

* Wrong physical NIC bound
* Incorrect gateway
* Bridge misconfiguration
* Firewall interference

If failure occurs:

* Stop further changes
* Trigger **Network Lockout Incident Response**

---

## Documentation

* Save `/etc/network/interfaces` copy
* Screenshot Web UI network page
* Reference this baseline in future ADRs

---

## Engineering Principle Reinforced

> Stability first. Complexity later.

The hypervisor network is not a playground.
