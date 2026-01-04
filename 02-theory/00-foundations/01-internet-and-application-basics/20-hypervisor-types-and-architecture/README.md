# Hypervisor Types and Architecture

This document deepens your understanding of **how hypervisors are built internally**, how they interact with hardware, and how Proxmox leverages Linux, KVM, and QEMU to provide enterprise-grade virtualization.

This is a **core systems topic**. Senior DevOps engineers understand not just *what* tools do, but *how* they are architected.

---

## 1. Why Architecture Matters

When something breaks at the virtualization layer:

* VMs become slow or unresponsive
* Storage I/O spikes
* Networking silently fails

Without architectural understanding, troubleshooting becomes guesswork.

---

## 2. Hypervisor Architecture Overview

At a high level, a modern hypervisor stack consists of:

1. Physical Hardware
2. CPU Virtualization Extensions (Intel VT-x / AMD-V)
3. Host Kernel
4. Hypervisor Engine
5. VM Processes
6. Guest Operating Systems

Each layer has a defined responsibility and failure domain.

---

## 3. CPU Virtualization Architecture

### Hardware Support

Modern CPUs include virtualization extensions:

* Intel VT-x
* AMD-V

These allow:

* Safe execution of guest OS instructions
* Trap-and-emulate for privileged operations
* Reduced overhead compared to software-only virtualization

---

### vCPU Scheduling

* Guest vCPUs are mapped to physical CPUs
* Hypervisor schedules execution time
* Overcommitment is possible

**Failure Mode:**

* CPU contention → latency, VM freezes

---

## 4. Memory Virtualization Architecture

### How Memory Is Virtualized

* Guest OS thinks it owns contiguous RAM
* Hypervisor maps guest memory to host memory
* Uses page tables and shadow paging

### Advanced Techniques

* Ballooning
* Swapping
* Kernel Same-page Merging (KSM)

**Failure Mode:**

* Host memory exhaustion → OOM kills, VM crashes

---

## 5. Storage Virtualization Architecture

### Virtual Disks

* File-backed (qcow2)
* Block-backed (LVM, ZFS)

### Snapshot Mechanism

* Copy-on-write
* Metadata tracking

**Failure Mode:**

* Storage full → VM freeze
* Snapshot chain corruption

---

## 6. Network Virtualization Architecture

### Virtual Networking Components

* Virtual NICs (vNIC)
* Linux bridges
* Software switches
* VLAN tagging

### Traffic Flow

VM → vNIC → Bridge → Physical NIC

**Failure Mode:**

* Bridge misconfiguration → network isolation

---

## 7. Type 1 Hypervisor Internal Models

### Monolithic Hypervisors

* Most logic in hypervisor kernel
* Example: ESXi

Pros:

* Performance

Cons:

* Less flexible

---

### Microkernel / Modular Hypervisors

* Minimal kernel
* User-space components
* Example: KVM + Linux

Pros:

* Flexibility
* Leverages Linux ecosystem

Cons:

* More moving parts

---

## 8. Proxmox Architecture (Your Lab)

Proxmox is **not a single hypervisor**. It is a platform composed of:

* Debian Linux (base OS)
* Linux Kernel (scheduler, memory, networking)
* KVM (virtualization engine)
* QEMU (VM emulation)
* Proxmox VE services (API, UI, clustering)

This design is why Proxmox feels powerful but complex.

---

## 9. Control Plane vs Data Plane

### Control Plane

* Proxmox Web UI
* REST API
* Cluster services

### Data Plane

* VM execution
* Disk I/O
* Network traffic

Breaking control plane ≠ VM downtime (important concept).

---

## 10. Failure Domains You Will Practice

* CPU overcommit stress tests
* Memory exhaustion
* Storage saturation
* Network isolation
* Hypervisor reboot

Each failure maps directly to a real-world incident scenario.

---

## 11. You Should Now Clearly Understand

* How hypervisors are layered on hardware
* CPU, memory, storage, and network virtualization internals
* Why Proxmox uses Linux + KVM
* Where failures originate and how they propagate

---

## Next Theory Topic

[**Proxmox Control Plane, Storage, and VM Networking**](../21-proxmox-control-plane-storage-vm-networking/README.md)