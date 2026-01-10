# Linux Boot Process (BIOS/UEFI → GRUB → Kernel → init/systemd)

This document explains **how a Linux system boots from power-on to a usable operating system**. Understanding this flow is critical for diagnosing boot failures, kernel panics, cloud VM startup issues, and rescue-mode recoveries.

This is **systems engineering knowledge**, not just administration.

---

## 1. Why This Matters

When a Linux system fails to start, junior engineers ask:

> “Why is my server not booting?”

Senior engineers ask:

> “At which boot stage did the failure occur?”

Every Linux boot issue maps to **one specific phase**. Knowing the phases turns panic into structured diagnosis.

---

## 2. High-Level Boot Flow

```
Power On
  ↓
Firmware (BIOS / UEFI)
  ↓
Bootloader (GRUB)
  ↓
Linux Kernel
  ↓
init / systemd (PID 1)
  ↓
User Space Services
  ↓
Login / Application Workloads
```

Each step hands control to the next. Failure at any step **prevents the next stage from executing**.

---

## 3. Firmware Stage (BIOS / UEFI)

### Responsibilities

* Initialize CPU, RAM, and basic hardware
* Perform hardware checks (POST)
* Locate a bootable device
* Transfer control to the bootloader

### BIOS vs UEFI

| BIOS             | UEFI                     |
| ---------------- | ------------------------ |
| Legacy firmware  | Modern firmware          |
| MBR-based boot   | GPT-based boot           |
| Limited features | Secure Boot, faster boot |

### Failure Symptoms

* System powers on but shows no boot menu
* “No bootable device found”
* Firmware setup loops

**These are not Linux problems.**

---

## 4. Bootloader Stage (GRUB)

### What GRUB Does

* Displays boot menu
* Loads Linux kernel into memory
* Loads initramfs (initial RAM filesystem)
* Passes kernel parameters

GRUB is the **bridge between firmware and kernel**.

### Key Files

* `/boot/grub/grub.cfg`
* `/boot/vmlinuz-*` (kernel)
* `/boot/initrd.img-*` (initramfs)

### Failure Symptoms

* GRUB rescue prompt
* Kernel not found
* Wrong kernel version boots

At this stage, the kernel has **not started yet**.

---

## 5. Kernel Stage

### Kernel Responsibilities at Boot

* Decompress itself into memory
* Initialize CPU scheduling
* Initialize memory management
* Detect hardware
* Mount root filesystem (via initramfs)

Once the kernel starts, **firmware and GRUB are done**.

### initramfs Role

initramfs is a temporary root filesystem that:

* Loads storage drivers
* Finds real root filesystem
* Hands control to systemd

### Failure Symptoms

* Kernel panic
* Unable to mount root filesystem
* Stuck at “Loading initial ramdisk”

These are **kernel or storage driver problems**.

---

## 6. init / systemd Stage (PID 1)

### What systemd Does

* Becomes **PID 1**
* Mounts remaining filesystems
* Starts system services
* Manages dependencies
* Transitions system to target state

systemd is the **userspace orchestrator**.

### Targets (Simplified)

| Target              | Purpose            |
| ------------------- | ------------------ |
| `rescue.target`     | Single-user rescue |
| `multi-user.target` | CLI server         |
| `graphical.target`  | Desktop            |

### Failure Symptoms

* System boots but services fail
* Stuck at “Reached target…”
* Endless service restart loops

These are **userspace service issues**, not kernel issues.

---

## 7. User Space & Login

Once systemd completes:

* Network starts
* SSH becomes available
* Applications launch
* Users can log in

From here onward, failures are **application-level or configuration-level**.

---

## 8. Cloud & Proxmox Mapping

| Linux Boot Stage | Cloud / Proxmox Equivalent |
| ---------------- | -------------------------- |
| BIOS/UEFI        | Hypervisor firmware        |
| GRUB             | VM bootloader              |
| Kernel           | Guest OS kernel            |
| systemd          | VM service orchestration   |

This is why cloud VMs can fail before SSH ever comes up.

---

## 9. Common Real-World Failure Mapping

| Symptom          | Likely Stage       |
| ---------------- | ------------------ |
| No boot device   | BIOS/UEFI          |
| GRUB rescue      | Bootloader         |
| Kernel panic     | Kernel             |
| SSH never starts | systemd / services |

This table alone is worth memorizing.

---

## 10. You Should Now Clearly Understand

* Exact Linux boot sequence
* Responsibility of each boot stage
* How to map symptoms to boot layers
* Why rescue mode exists
* Why cloud VM failures look “silent”

---

## Next Topic

👉 **Filesystem Hierarchy (FHS)**

You must understand filesystem layout **before** learning files, permissions, and services.

Say:
**Next: Filesystem Hierarchy (FHS)**
