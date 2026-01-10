# Filesystem Hierarchy Standard (FHS)

This document explains **how Linux organizes files and directories**, why this structure exists, and how it impacts operations, security, troubleshooting, and automation.

Understanding FHS is mandatory for:

* Debugging production issues
* Writing safe automation
* Managing services and logs
* Operating containers and Kubernetes nodes

---

## 1. Why This Matters

Junior engineers memorize paths.

Senior engineers understand **intent**:

> “What belongs where, why it lives there, and what breaks if it doesn’t.”

Misplacing files causes:

* Services not starting
* Log rotation failures
* Disk-full incidents
* Security exposures

FHS gives Linux **predictability at scale**.

---

## 2. What Is FHS?

The **Filesystem Hierarchy Standard** defines:

* Directory purposes
* Separation of concerns
* Upgrade-safe layouts

It ensures Linux systems behave consistently across:

* Servers
* Cloud VMs
* Containers
* Kubernetes nodes

---

## 3. Root Filesystem (`/`)

Everything starts at `/`.

It contains only **essential directories** required to:

* Boot
* Mount filesystems
* Enter rescue mode

If `/` is corrupted or full → **system instability**.

---

## 4. Critical Directories (Know These Cold)

### `/bin` and `/sbin`

* Essential user and system binaries
* Required for boot and rescue

Examples:

* `ls`, `cp`, `mv`
* `ip`, `mount`, `fsck`

> On modern systems, these may be symlinked to `/usr/bin`.

---

### `/boot`

* Kernel images
* initramfs
* Bootloader files

Failure impact:

* System will not boot

Never casually modify `/boot`.

---

### `/etc`

* System-wide configuration
* Text-based, human-readable

Examples:

* `/etc/ssh/sshd_config`
* `/etc/passwd`
* `/etc/systemd/`

> Configuration belongs here — **never binaries**.

---

### `/var`

* Variable data that changes at runtime

Includes:

* Logs (`/var/log`)
* Spool files
* Package caches

Common incident:

> `/var` fills up → services fail silently

---

### `/home`

* User home directories
* Non-system data

Servers may have minimal `/home` usage.

---

### `/usr`

* User-space programs and libraries
* Majority of installed software

Subdirectories:

* `/usr/bin`
* `/usr/lib`
* `/usr/share`

> `/usr` should be **read-only at runtime** on hardened systems.

---

### `/lib` and `/lib64`

* Shared libraries required for boot
* Kernel modules

Missing libraries here → kernel or service failures.

---

### `/proc`

* Virtual filesystem
* Kernel state exposed as files

Examples:

* `/proc/cpuinfo`
* `/proc/meminfo`

Used heavily for diagnostics.

---

### `/sys`

* Kernel device and driver interface
* Hardware-level controls

Used by:

* systemd
* udev
* container runtimes

---

### `/tmp`

* Temporary files
* Often cleared on reboot

Never store important data here.

---

## 5. Runtime Directories

### `/run`

* Runtime state since boot
* PID files, sockets

Replaces legacy `/var/run`.

---

## 6. Containers & Cloud Mapping

| FHS Path   | Container / Cloud Meaning    |
| ---------- | ---------------------------- |
| `/etc`     | ConfigMaps / user-data       |
| `/var/log` | Centralized logging          |
| `/proc`    | Container isolation boundary |
| `/run`     | Ephemeral runtime state      |

This is why mis-mounted volumes break containers.

---

## 7. Common Production Mistakes

* Writing logs to `/`
* Hardcoding paths in scripts
* Storing secrets in `/home`
* Installing binaries in `/etc`

All of these cause outages.

---

## 8. You Should Now Clearly Understand

* Purpose of major Linux directories
* What belongs where (and what doesn’t)
* Why `/var` causes outages
* How filesystem layout affects services
* How FHS maps to cloud and containers

---

## Next Topic

👉 **File Types**

You must understand file types before permissions, links, and inodes.

Say:
**Next: File Types**
