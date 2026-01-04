# Proxmox Control Plane, Storage, and VM Networking

This document explains **how Proxmox VE actually works under the hood**: how the control plane operates, how storage is managed, and how virtual machine networking is implemented.

This is not tool usage. This is **platform engineering knowledge**.

---

## 1. Why This Matters

When Proxmox fails, engineers often ask the wrong question:

> “Why is my VM down?”

Senior engineers ask:

> “Is this a control plane failure, data plane failure, or storage bottleneck?”

Understanding this distinction prevents panic-driven mistakes.

---

## 2. Proxmox Architecture Overview

Proxmox VE is composed of:

* Debian Linux (host OS)
* Linux Kernel (scheduler, memory, networking)
* KVM (hypervisor)
* QEMU (VM execution)
* Proxmox services (API, UI, cluster services)

Proxmox itself is **not** the hypervisor — it **orchestrates** virtualization.

---

## 3. Control Plane Architecture

### What Is the Control Plane?

The control plane is responsible for **management and orchestration**, not VM execution.

Components include:

* Web UI (pveproxy)
* REST API
* pvedaemon
* pmxcfs (cluster filesystem)
* Authentication and RBAC

### Key Principle

> Control plane down ≠ VM down

VMs continue running even if the UI/API is unavailable.

---

## 4. Control Plane Failure Scenarios

* Web UI unreachable
* API timeouts
* Authentication failures
* Cluster state inconsistencies

**Impact:**

* No VM start/stop/migration
* No configuration changes
* Running workloads unaffected

This distinction is critical during incidents.

---

## 5. Proxmox Storage Architecture

### Storage Abstraction

Proxmox abstracts storage via **storage backends**:

* Directory
* LVM / LVM-Thin
* ZFS
* Ceph (enterprise)

VM disks are mapped to these backends.

---

### Storage Data Flow

VM → Virtual Disk → Storage Backend → Physical Disk

Each layer introduces latency and failure potential.

---

## 6. Storage Failure Domains

Common failure modes:

* Disk full → VM freeze
* Snapshot chain growth
* I/O wait spikes
* Corrupt volumes

**Key Lesson:**

> Storage issues often appear as “VM CPU problems” or “network slowness”.

---

## 7. VM Networking Architecture

### Virtual Networking Components

* vmbrX (Linux bridges)
* vNICs attached to VMs
* Physical NICs
* VLANs (optional)

Proxmox uses **standard Linux networking**, not proprietary switching.

---

### Traffic Flow

Inbound traffic:

Client → Physical NIC → Linux Bridge → VM vNIC → Guest OS

Outbound traffic follows the reverse path.

---

## 8. Bridged Networking Explained

Bridged networking allows:

* VMs to appear as first-class network hosts
* Direct IP assignment from LAN

This is why bridged misconfiguration causes total VM isolation.

---

## 9. Network Failure Scenarios

* Incorrect bridge mapping
* VLAN mismatch
* Firewall rules blocking traffic
* NIC driver issues

These failures mimic cloud VPC misconfigurations.

---

## 10. Proxmox Firewall Model

* Host-level firewall
* VM-level firewall
* Linux iptables/nftables underneath

Rules apply at multiple layers.

---

## 11. Mapping Proxmox to Cloud Concepts

| Proxmox Concept | Cloud Equivalent |
| --------------- | ---------------- |
| VM              | EC2 / VM         |
| Bridge          | VPC subnet       |
| Firewall        | Security Group   |
| Storage pool    | EBS / Disk       |

This mapping is intentional — cloud skills transfer directly.

---

## 12. You Should Now Clearly Understand

* Difference between control plane and data plane
* How Proxmox manages VM lifecycle
* Storage backends and failure domains
* VM networking and traffic flow
* Why Proxmox incidents resemble cloud outages

---

## Next Step

You are now ready to build [**Week 1 hands-on labs**](../../../../03-home-lab/01-promox/week-01-proxmox-baseline/README.md):

* Proxmox baseline configuration
* Network bridges
* SSH access
* First VM creation

This is where theory turns into muscle memory.
