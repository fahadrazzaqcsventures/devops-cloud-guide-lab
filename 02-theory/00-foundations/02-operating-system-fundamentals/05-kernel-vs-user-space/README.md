# Kernel vs User Space

This document explains the **most important boundary in any operating system**: the separation between the kernel and user space. This boundary is foundational for Linux, containers, virtualization, security, and incident response.

This is not theory trivia. This boundary explains *why* systems remain stable, *why* permissions exist, and *why* some failures crash applications while others crash entire machines.

---

## 1. Why This Matters

When something goes wrong, junior engineers ask:

> “Why did my command fail?”

Senior engineers ask:

> “Did this fail in user space or kernel space?”

Knowing the answer determines:

* Blast radius
* Recovery strategy
* Whether a reboot is required
* Whether data integrity is at risk

---

## 2. What Is the Kernel?

The **kernel** is the core of the operating system.

It runs in **privileged mode** and has unrestricted access to hardware.

The kernel is responsible for:

* CPU scheduling
* Memory management
* Process isolation
* Filesystems
* Networking stack
* Device drivers
* Security enforcement

> There is exactly **one kernel** controlling the machine.

---

## 3. What Is User Space?

**User space** is where all applications run, including:

* Shells (bash, zsh)
* System utilities (ls, cp, ps)
* Web servers (nginx, apache)
* Databases
* Containers
* CI/CD agents

User space programs:

* Cannot access hardware directly
* Cannot access kernel memory
* Must request services from the kernel

---

## 4. Privilege Levels (CPU Rings)

Most modern CPUs implement privilege rings:

* **Ring 0** → Kernel mode (highest privilege)
* **Ring 3** → User mode (applications)

Linux primarily uses these two rings.

This separation prevents:

* Applications crashing the system
* Malicious code taking over hardware
* Accidental damage from user commands

---

## 5. How User Space Talks to the Kernel

User space cannot execute privileged operations directly.

Instead, it uses:

### System Calls

System calls are controlled entry points into the kernel.

Examples:

* `open()` → request file access
* `read()` / `write()` → I/O operations
* `fork()` → create process
* `exec()` → execute program
* `socket()` → network operations

Every command eventually becomes **system calls**.

---

## 6. Shell Commands vs Kernel Operations

Example:

```bash
ls
```

What actually happens:

1. Shell runs `ls` in user space
2. `ls` requests directory metadata via system calls
3. Kernel checks permissions
4. Kernel reads filesystem structures
5. Results returned to user space

The shell never touches the disk directly.

---

## 7. Failure Domains

### User Space Failure

Examples:

* Application crash
* Service exits
* Memory leak
* Misconfiguration

Impact:

* Process dies
* System remains stable
* Restart usually fixes

---

### Kernel Space Failure

Examples:

* Kernel panic
* Driver crash
* Filesystem corruption
* Network stack bug

Impact:

* System instability
* Possible data loss
* Reboot required

> Senior engineers fear kernel failures — not app crashes.

---

## 8. Security Implications

The kernel enforces:

* File permissions
* Process isolation
* Capability boundaries
* Namespaces and cgroups

Security vulnerabilities that escape user space are called:

> **Kernel privilege escalation bugs**

These are severe and often patched urgently.

---

## 9. Containers and This Boundary

Containers:

* Run in user space
* Share the host kernel
* Use kernel features (namespaces, cgroups)

This is why:

* Containers are lightweight
* A kernel bug affects all containers
* You cannot run Windows containers on a Linux kernel

---

## 10. Mapping to DevOps & Cloud

| Concept      | Reality                            |
| ------------ | ---------------------------------- |
| VM           | Own kernel                         |
| Container    | Shared kernel                      |
| Kubernetes   | Kernel resource orchestration      |
| Cloud outage | Often kernel or networking related |

Understanding this boundary prevents:

* Blind reboots
* Over-permissioning
* Security misconfigurations

---

## 11. You Should Now Clearly Understand

* What the kernel is responsible for
* What user space is allowed to do
* Why permissions exist
* Why some failures are catastrophic
* Why containers behave differently from VMs

---

## Next Topic

[**System calls vs shell commands**](../06-system-calls-vs-shell-commands/README.md)

This connects everything you’ve learned so far and prepares you for:

* strace
* debugging
* performance analysis
* real incident response
