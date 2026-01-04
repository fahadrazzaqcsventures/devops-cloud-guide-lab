# What is a Hypervisor

This document explains **hypervisors**, the control layer that enables virtualization and forms the backbone of on‑prem, cloud, and enterprise infrastructure.

Understanding hypervisors is mandatory before working with Proxmox, VMware, cloud IaaS, or Kubernetes worker nodes.

---

## 1. Why This Topic Matters

A hypervisor is the **authority** that:

* Allocates CPU, memory, disk, and network to virtual machines
* Enforces isolation between workloads
* Enables live migration, snapshots, and high availability

If virtualization is the concept, **the hypervisor is the engine**.

---

## 2. What Is a Hypervisor?

A **hypervisor** (also called a Virtual Machine Monitor – VMM) is a software layer that:

* Runs on physical hardware (or on top of an OS)
* Creates and manages virtual machines
* Abstracts hardware for guest operating systems

Each VM believes it has dedicated hardware, but the hypervisor schedules and controls access.

---

## 3. Core Responsibilities of a Hypervisor

A hypervisor is responsible for:

* **CPU Scheduling** – mapping vCPUs to physical CPUs
* **Memory Management** – allocation, paging, ballooning
* **Storage Virtualization** – virtual disks, snapshots
* **Network Virtualization** – virtual NICs, bridges, switches
* **Isolation & Security** – preventing VM interference
* **Lifecycle Management** – start, stop, migrate, destroy VMs

---

## 4. Hypervisor Types

### Type 1 — Bare-Metal Hypervisor

Runs **directly on hardware**.

Examples:

* Proxmox VE
* VMware ESXi
* Microsoft Hyper-V (Server)
* Xen

Characteristics:

* High performance
* Strong isolation
* Used in data centers and clouds

---

### Type 2 — Hosted Hypervisor

Runs **on top of a host operating system**.

Examples:

* VirtualBox
* VMware Workstation
* Parallels

Characteristics:

* Easier to set up
* Lower performance
* Used for local development and testing

---

## 5. Type 1 vs Type 2 (Comparison)

| Aspect      | Type 1            | Type 2        |
| ----------- | ----------------- | ------------- |
| Runs on     | Bare metal        | Host OS       |
| Performance | High              | Lower         |
| Security    | Strong            | Weaker        |
| Use case    | Production, cloud | Desktop, labs |

Your home lab uses **Type 1**.

---

## 6. How a Hypervisor Actually Works (Simplified)

1. Physical hardware boots
2. Hypervisor kernel loads
3. Hardware resources are abstracted
4. VMs request virtual resources
5. Hypervisor schedules and enforces access

Modern CPUs (Intel VT‑x / AMD‑V) provide hardware support for this.

---

## 7. Hypervisors and the Cloud

Cloud providers expose VMs, but hide the hypervisor:

* AWS EC2 → Nitro / Xen-based systems
* Azure → Hyper-V
* GCP → KVM

When you create a VM in the cloud, you are indirectly interacting with a hypervisor.

---

## 8. Home Lab Mapping (Proxmox)

In your lab:

* Proxmox VE = Type 1 hypervisor
* Web UI / API = control plane
* KVM = virtualization engine
* Linux kernel = scheduling and isolation

You will:

* Overcommit CPU and RAM
* Observe performance contention
* Break and recover VMs

---

## 9. Common Hypervisor Failure Scenarios

* CPU overcommit → VM latency
* Memory exhaustion → VM OOM kills
* Storage saturation → VM crashes
* Network bridge misconfiguration → VM isolation

These failures will be intentionally simulated later.

---

## 10. You Should Now Clearly Understand

* What a hypervisor is and why it exists
* The difference between Type 1 and Type 2 hypervisors
* Why Proxmox is production‑grade
* How hypervisors underpin cloud and DevOps platforms

---

## Next Theory Topic

[**Hypervisor Types and Architecture**](../20-hypervisor-types-and-architecture/README.md)
