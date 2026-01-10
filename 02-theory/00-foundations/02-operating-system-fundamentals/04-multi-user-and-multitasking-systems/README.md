# Multi-User and Multi-Tasking Systems

This document explains how operating systems safely support **multiple users** and **multiple workloads at the same time**. These concepts are fundamental to servers, cloud platforms, containers, and Kubernetes.

Without multi-user and multitasking design, modern infrastructure would collapse under shared usage.

---

## 1. Why This Matters

In production environments, systems are **never single-user** and **never single-task**:

* Multiple engineers access the same servers
* Dozens to thousands of processes run concurrently
* Containers and pods share the same kernel

Senior engineers must understand **how isolation and fairness are enforced**, not assume they “just work.”

---

## 2. What Is a Multi-User System?

A **multi-user system** allows multiple users to:

* Log in concurrently
* Run processes independently
* Access shared system resources safely

Each user has:

* A unique UID (User ID)
* One or more GIDs (Group IDs)
* Separate permissions and ownership

The OS enforces boundaries between users at the kernel level.

---

## 3. User Isolation Model

Linux isolates users through:

* File ownership and permissions
* Process ownership
* Privilege separation (root vs non-root)
* Authentication and authorization controls

Even if users share hardware, their **processes and files remain isolated** unless explicitly permitted.

### Failure Symptoms

* Permission denied errors
* Accidental deletion of shared files
* Privilege escalation incidents

---

## 4. What Is Multi-Tasking?

**Multi-tasking** allows the OS to execute multiple processes seemingly at the same time.

This is achieved through:

* Time slicing
* Context switching
* CPU scheduling algorithms

Even on a single CPU core, the OS rapidly switches between processes to create concurrency.

---

## 5. Process and Thread Management

### Processes

* Independent execution units
* Separate memory spaces
* Isolated from each other by default

### Threads

* Lightweight execution units within a process
* Share memory space
* Faster context switches

The OS scheduler manages both based on priority and fairness.

---

## 6. Fairness and Resource Control

The OS ensures:

* No single process monopolizes CPU
* Memory usage is bounded
* I/O operations are scheduled fairly

In Linux, this is enforced via:

* Scheduler policies
* Cgroups (control groups)

This is the foundation of container resource limits.

---

## 7. Server vs Desktop Implications

Servers:

* Designed for many users
* Long-running processes
* Remote access (SSH)
* Stability over UI responsiveness

Desktops:

* Usually single-user
* Interactive workloads
* Focus on UI performance

This distinction explains many Linux server defaults.

---

## 8. DevOps and Cloud Relevance

Multi-user and multitasking concepts directly map to:

* SSH access control
* CI/CD runners sharing hosts
* Containers running on the same node
* Kubernetes pods sharing kernels

Most cloud outages involve **resource contention**, not crashes.

---

## 9. Failure Scenarios You Will Encounter

* One user fills disk, impacting all services
* One process consumes all CPU
* Misconfigured permissions break deployments

Understanding these prevents panic-driven fixes.

---

## 10. You Should Now Clearly Understand

You should be able to explain:

* How multiple users safely share a system
* How processes run concurrently
* Difference between processes and threads
* How fairness and isolation are enforced
* Why resource limits exist in containers

---

## Next Topic

Proceed with:

[**Kernel vs User Space**](../05-kernel-vs-user-space/README.md)

This will formalize the boundary between:

* What applications can do
* What only the OS can do

Theory first. Labs later.
