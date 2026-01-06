# Bridged Networking and VM Connectivity

This document explains **bridged networking in virtualization environments** and how virtual machines achieve network connectivity through the host.

This is not about clicking UI options. This is **core systems and networking engineering knowledge** that directly maps to cloud networking concepts.

---

## 1. Why This Matters

Most severe infrastructure outages are networking-related.

Junior engineers ask:

> “Why can’t I SSH into my VM?”

Senior engineers ask:

> “Where is the packet being dropped — host, bridge, firewall, or guest OS?”

Understanding bridged networking allows you to:

* Diagnose VM connectivity failures quickly
* Avoid host lockouts
* Translate on‑prem networking knowledge to cloud VPCs
* Design predictable, debuggable network architectures

---

## 2. Virtual Networking Overview

In a virtualized environment, networking consists of multiple layers:

* Physical Network Interface (NIC)
* Host operating system networking stack
* Virtual switch / bridge
* Virtual NIC (vNIC) attached to the VM
* Guest operating system network stack

Each layer can independently fail.

---

## 3. What Is Bridged Networking?

Bridged networking connects virtual machines directly to the same Layer 2 network as the host.

A **Linux bridge** behaves like a software switch:

* Forwards Ethernet frames
* Learns MAC addresses
* Does not perform NAT

In Proxmox, these bridges are typically named:

* `vmbr0`
* `vmbr1`

---

## 4. Traffic Flow (End-to-End)

Inbound traffic:

Client → Physical Switch → Host NIC → Linux Bridge → VM vNIC → Guest OS

Outbound traffic follows the reverse path.

Key point:

> The host does **not** rewrite or proxy traffic in bridged mode.

VMs appear as **first-class network devices**.

---

## 5. IP Addressing and Connectivity

With bridged networking:

* VMs receive IPs from the same subnet as the host
* DHCP or static IPs behave normally
* VMs can communicate directly with:

  * Other VMs
  * The host
  * External devices on the LAN

This is why bridged VMs feel identical to physical servers.

---

## 6. Linux Bridge Components

A typical Proxmox bridge configuration includes:

* Physical NIC (e.g. `eno1`)
* Bridge interface (e.g. `vmbr0`)
* Optional VLAN tagging
* Firewall rules (iptables / nftables)

The physical NIC becomes a **bridge port**, not an IP endpoint.

---

## 7. Common Failure Scenarios

Bridged networking fails most often due to:

* Bridge interface down
* Physical NIC removed from bridge
* Incorrect VLAN configuration
* Firewall rules blocking traffic
* Accidental IP assignment to the wrong interface

These failures often cause **total VM isolation**.

---

## 8. Network Lockout Risk

Because the host depends on the bridge:

* Misconfiguring the bridge can lock you out
* SSH and Web UI fail simultaneously
* VMs may continue running but are unreachable

This is why console access is mandatory before changes.

---

## 9. Bridged Networking vs NAT

| Feature              | Bridged         | NAT             |
| -------------------- | --------------- | --------------- |
| VM visibility        | Full LAN access | Private network |
| IP assignment        | LAN subnet      | Private subnet  |
| Performance          | Near‑native     | Slight overhead |
| Failure blast radius | High            | Lower           |
| Cloud similarity     | High            | Low             |

Bridged networking mirrors **cloud VPC subnet behavior**.

---

## 10. Mapping to Cloud Concepts

| On‑Prem / Proxmox | Cloud Equivalent      |
| ----------------- | --------------------- |
| Linux bridge      | VPC subnet            |
| VM NIC            | ENI                   |
| Host firewall     | Security group / NACL |
| Physical switch   | Cloud fabric          |

This is why mastering bridges accelerates cloud learning.

---

## 11. Operational Best Practices

* Always verify console access before network changes
* Document current network state
* Change one variable at a time
* Avoid editing live bridges remotely
* Maintain recovery runbooks

These practices separate operators from engineers.

---

## 12. You Should Now Clearly Understand

* What bridged networking is
* How VM traffic flows end‑to‑end
* Why bridge misconfiguration is dangerous
* Common failure modes
* How on‑prem bridges map to cloud networking

---

## Next Theory Topic

[**SSH key-based authentication**](../23-ssh-key-based-authentication/README.md)
