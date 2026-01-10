# Linux Architecture

This document explains **how Linux is structured internally** and how its components interact. This is not about commands — it is about understanding **why Linux behaves the way it does under load, failure, and scale**.

This knowledge is foundational for debugging production systems, containers, Kubernetes nodes, and cloud instances.

---

## 1. Why Linux Architecture Matters

Junior engineers ask:

> “Which command do I run?”

Senior engineers ask:

> “Which subsystem is failing?”

Linux architecture explains:

* Why high CPU does not always mean a CPU problem
* Why disk issues can appear as application slowness
* Why networking failures cascade across services
* Why containers are not magic — they are Linux features

---

## 2. High-Level Linux Architecture

At a high level, Linux is divided into two major domains:

1. **Kernel Space** — privileged, hardware-facing code
2. **User Space** — applications, services, and tools

Everything you interact with eventually crosses this boundary.

```
+---------------------------+
|        User Space         |
|---------------------------|
|  Shells, Apps, Services   |
|  systemd, Docker, kubelet |
+---------------------------+
|        Kernel Space       |
|---------------------------|
| Scheduler | Memory | VFS  |
| Networking | Drivers      |
+---------------------------+
|         Hardware          |
+---------------------------+
```

---

## 3. Kernel Space

The **Linux kernel** is responsible for:

* Enforcing security and isolation
* Managing hardware resources
* Scheduling processes
* Handling memory and I/O

Applications **cannot directly access hardware**. All access is mediated by the kernel.

### Key Kernel Subsystems

#### a) Process Scheduler

* Decides **which process runs on which CPU core**
* Implements time slicing and priorities
* Directly impacts latency and throughput

High load ≠ CPU shortage — it may be scheduling contention.

---

#### b) Memory Management

Handles:

* Virtual memory
* Page tables
* Caching
* Swap
* Out-of-memory (OOM) killing

OOM events are architectural signals, not random failures.

---

#### c) Virtual File System (VFS)

* Abstracts filesystems (ext4, xfs, tmpfs, procfs)
* Allows applications to treat everything as a file

This abstraction enables containers, mounts, and namespaces.

---

#### d) Networking Stack

Implements:

* TCP/IP
* Routing
* Netfilter (iptables / nftables)
* Socket handling

Network latency often originates **inside the kernel**, not the network cable.

---

#### e) Device Drivers

* Bridge between hardware and kernel subsystems
* NICs, disks, GPUs, USB, etc.

Driver instability causes some of the hardest-to-debug outages.

---

## 4. User Space

User space contains everything that is **not privileged**:

* Shells (bash, zsh)
* Applications
* Daemons (sshd, nginx, docker)
* systemd
* CLI tools

User space cannot bypass kernel controls.

---

## 5. System Calls: The Boundary

Applications interact with the kernel using **system calls**:

* read()
* write()
* fork()
* exec()
* open()

This boundary is:

* A security barrier
* A performance boundary
* A debugging boundary

Strace exists because this boundary matters.

---

## 6. systemd in the Architecture

`systemd` is a **user-space init system**, not part of the kernel.

It:

* Starts services
* Manages dependencies
* Restarts failed units
* Tracks system state

systemd orchestrates services; the kernel executes them.

---

## 7. Containers in Linux Architecture

Containers are **not virtualization**.

They rely on:

* Namespaces (process, network, mount)
* cgroups (CPU, memory limits)
* Capabilities

All container isolation is implemented **inside the Linux kernel**.

This is why Linux dominates container platforms.

---

## 8. Failure Domains in Linux Architecture

| Symptom               | Likely Subsystem             |
| --------------------- | ---------------------------- |
| High load             | Scheduler / I/O wait         |
| App freeze            | Disk or memory pressure      |
| Network drops         | Kernel networking / firewall |
| Random kills          | OOM killer                   |
| Service restart loops | systemd / dependencies       |

Understanding architecture prevents guesswork.

---

## 9. Mapping to Cloud & DevOps

| Linux Concept | Cloud Equivalent      |
| ------------- | --------------------- |
| Process       | Pod / Container       |
| cgroups       | Resource limits       |
| Namespaces    | Tenant isolation      |
| Kernel        | Cloud hypervisor      |
| systemd       | Orchestration control |

Cloud abstractions are built **on top of Linux architecture**.

---

## 10. You Should Now Clearly Understand

* Difference between kernel space and user space
* Role of major kernel subsystems
* Why Linux failures cascade the way they do
* Why containers and Kubernetes depend on Linux
* How architecture informs incident response

---

## Next Topic

**Kernel Responsibilities**

This will go deeper into *what the kernel actually guarantees* — and what it does not.

Do not rush. This is core system engineering knowledge.
