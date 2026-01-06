# Tasks of an Operating System

This document explains **what an operating system is actually responsible for** at runtime. These are not features; they are **non‑negotiable engineering duties** the OS must perform to keep systems stable, secure, and performant.

This knowledge is foundational for Linux administration, containerization, Kubernetes, and cloud operations.

---

## 1. Why This Matters

When systems fail, junior engineers blame:

> “The app is slow.”

Senior engineers ask:

> “Is this a CPU scheduling issue, memory pressure, I/O contention, or kernel bottleneck?”

Every production incident eventually maps back to **one or more OS responsibilities failing under load or misconfiguration**.

---

## 2. Core Responsibilities of an Operating System

At a high level, the OS is responsible for:

* Managing CPU time
* Managing memory
* Managing storage and files
* Managing hardware devices
* Managing networking
* Enforcing security and isolation

These responsibilities are handled primarily by the **kernel**, not by user commands.

---

## 3. CPU Management (Process Scheduling)

### What the OS Does

* Creates processes and threads
* Schedules them on CPU cores
* Performs context switching
* Enforces priorities and fairness

The Linux kernel uses advanced schedulers (e.g., CFS) to balance workloads.

### Failure Symptoms

* High load average
* Applications “hanging” without crashing
* Pods throttled in Kubernetes

### DevOps Relevance

* CPU limits/requests map directly to kernel scheduling
* Overcommitting CPU leads to noisy‑neighbor problems

---

## 4. Memory Management

### What the OS Does

* Allocates RAM to processes
* Manages virtual memory
* Handles paging and swapping
* Enforces memory isolation

Linux uses **virtual memory** to give each process the illusion of exclusive RAM.

### Failure Symptoms

* OOM killer terminating processes
* Swap thrashing
* Sudden pod restarts

### DevOps Relevance

* Container memory limits are enforced by the kernel
* Misconfigured memory causes unpredictable crashes

---

## 5. Storage & Filesystem Management

### What the OS Does

* Provides filesystems (ext4, xfs, zfs)
* Manages disk I/O scheduling
* Enforces permissions and ownership
* Handles buffering and caching

Applications never talk to disks directly — the OS mediates all access.

### Failure Symptoms

* Disk full outages
* High I/O wait
* Corrupt files or stalled services

### DevOps Relevance

* VM disks, container volumes, and cloud disks rely on OS I/O paths
* Storage issues often masquerade as “app bugs”

---

## 6. Device Management

### What the OS Does

* Loads device drivers
* Abstracts hardware via device files
* Handles interrupts
* Manages hot‑plug devices

In Linux, **everything is a file**, including devices.

### Failure Symptoms

* Network cards disappearing
* Disks not detected
* Kernel panic on driver failure

### DevOps Relevance

* Virtual NICs and disks depend on stable drivers
* Cloud VMs still rely on kernel‑level drivers

---

## 7. Networking Management

### What the OS Does

* Implements TCP/IP stack
* Manages sockets and ports
* Handles routing and ARP
* Applies firewall rules

Networking lives inside the kernel — tools like `ip`, `ss`, and `iptables` are just interfaces.

### Failure Symptoms

* Services reachable locally but not externally
* Dropped packets
* Latency spikes

### DevOps Relevance

* Containers, Kubernetes, and Proxmox all rely on kernel networking
* Most “cloud network issues” are OS networking issues

---

## 8. Security & Isolation

### What the OS Does

* Enforces user and group permissions
* Isolates processes
* Implements namespaces and cgroups
* Controls access to system resources

This is why multiple users and services can safely share a system.

### Failure Symptoms

* Privilege escalation
* Containers escaping isolation
* Unauthorized access

### DevOps Relevance

* Containers rely on OS isolation, not magic
* Misconfigured permissions are a top outage cause

---

## 9. You Should Now Clearly Understand

You should be able to explain:

* The six core responsibilities of an OS
* How failures map to specific OS subsystems
* Why “application issues” are often OS issues
* How Linux enforces isolation and resource control
* Why DevOps engineers must understand OS internals

---

## Next Topic

Proceed with:

[**Multi‑User and Multi‑Tasking Systems**](../04-multi-user-and-multitasking-systems/README.md)

This builds directly on OS responsibilities and prepares you for:

* Linux permissions
* Process ownership
* Server vs desktop operating systems

Theory first. Then labs.
