# Kernel Responsibilities

This document explains **what the Linux kernel is responsible for — and just as importantly, what it is NOT responsible for**.

Understanding this boundary is critical for debugging production issues and avoiding incorrect assumptions during incidents.

---

## 1. Why Kernel Responsibilities Matter

During outages, engineers often say:

> “Linux is slow”

or

> “The OS is broken.”

Senior engineers instead ask:

> “Which kernel subsystem is under pressure?”

Correct diagnosis depends on knowing **exact kernel duties**.

---

## 2. The Kernel’s Core Mission

The Linux kernel’s job is to:

* Abstract hardware
* Enforce isolation
* Allocate resources fairly
* Provide secure primitives

It does **not** manage business logic, application correctness, or deployment safety.

---

## 3. CPU Scheduling

The kernel:

* Decides **which process runs and when**
* Implements preemption
* Balances fairness vs throughput

Key concepts:

* Scheduler (CFS)
* Run queues
* Context switching

**Failure Symptoms:**

* High load average
* Latency spikes
* Processes waiting despite free CPU

---

## 4. Memory Management

The kernel manages:

* Virtual memory
* Page tables
* RAM allocation
* Swapping
* OOM Killer

Key concepts:

* Resident Set Size (RSS)
* Page cache
* Anonymous vs file-backed memory

**Failure Symptoms:**

* Sudden process termination
* System stalls
* Swap thrashing

---

## 5. Process & Thread Management

The kernel:

* Creates processes (fork)
* Loads executables (exec)
* Cleans up processes (exit)
* Manages threads

Every process has:

* PID
* State
* Memory space
* Open file descriptors

---

## 6. Filesystem & Storage Interfaces

The kernel provides:

* Virtual File System (VFS)
* Filesystem drivers (ext4, xfs)
* Block device abstraction

It does **not** decide:

* Application file structure
* Backup policies
* Data retention

**Failure Symptoms:**

* I/O wait spikes
* Disk full errors
* Hung processes

---

## 7. Networking Stack

The kernel handles:

* TCP/IP stack
* Packet routing
* Socket interfaces
* Firewall hooks

It does **not** manage:

* DNS correctness
* Application retries
* Load balancing logic

---

## 8. Security & Isolation

The kernel enforces:

* User/group permissions
* Process isolation
* Capabilities
* Namespaces
* cgroups

Security failures are often **misconfigurations**, not kernel bugs.

---

## 9. Device & Hardware Management

The kernel:

* Loads drivers
* Handles interrupts
* Manages hardware access

This is why missing drivers cause:

* Network cards disappearing
* Storage devices not mounting

---

## 10. What the Kernel Does NOT Do

The kernel does NOT:

* Start applications (systemd does)
* Restart failed services
* Handle application-level retries
* Enforce deployment safety
* Understand your architecture

Confusing these layers leads to poor incident response.

---

## 11. Kernel Responsibility Map

| Area              | Kernel Responsible | User Space Responsible |
| ----------------- | ------------------ | ---------------------- |
| CPU time          | Yes                | No                     |
| Memory allocation | Yes                | No                     |
| Process lifecycle | Yes                | No                     |
| Service restarts  | No                 | Yes                    |
| Application logic | No                 | Yes                    |
| Deployment safety | No                 | Yes                    |

---

## 12. You Should Now Clearly Understand

* Exact responsibilities of the Linux kernel
* How kernel subsystems fail
* How symptoms map to kernel areas
* Why blaming “Linux” is usually incorrect

---

## Next Topic

**Linux Boot Process (BIOS/UEFI → GRUB → Kernel → systemd)**

This explains **how a system becomes usable at all** — and how boot failures are diagnosed and recovered.
