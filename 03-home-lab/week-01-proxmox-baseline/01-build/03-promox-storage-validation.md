# Build Phase 3 – Proxmox Storage Validation

## Objective

Validate that Proxmox storage is **healthy, correctly configured, and predictable** before any VM creation or automation work.

Storage errors at the hypervisor level have a **high blast radius** and must be detected early.

---

## Purpose

* Confirm underlying disk health and availability
* Verify Proxmox storage backends are functional
* Ensure sufficient space for VM disks, ISOs, and backups
* Establish storage as a trusted platform layer

---

## Preconditions

* Proxmox host is fully updated and rebooted (Build Phase 1 completed)
* Access to Proxmox Web UI or console

---

## Storage Concepts (Context)

Before validating, understand:

* **Local storage**: typically used for ISOs, templates, and backups
* **LVM / LVM-Thin**: commonly used for VM disks
* **Directory storage**: file-based VM images and backups

Each backend has different performance and recovery characteristics.

---

## Actions

### 1. Identify Available Storage Backends

From the Proxmox host:

```bash
pvesm status
```

**Validate:**

* Storage backends are listed
* Status is `active`
* No error messages

---

### 2. Check Disk and Filesystem Health

```bash
lsblk

df -h
```

**Validate:**

* Expected disks are present
* Filesystems are mounted
* No unexpected 100% usage

---

### 3. Verify LVM / LVM-Thin (If Present)

```bash
vgs
lvs
```

**Validate:**

* Volume groups are active
* Thin pool has free space
* No degraded or inactive volumes

---

### 4. Confirm ISO and Template Storage

Via Web UI or CLI:

* Ensure an ISO storage location exists
* Verify ability to upload ISOs

CLI check:

```bash
ls /var/lib/vz/template/iso
```

---

### 5. Test Write Capability (Non-Destructive)

Create and remove a test file:

```bash
touch /var/lib/vz/test-write
rm /var/lib/vz/test-write
```

**Why:**

* Confirms filesystem is writable
* Detects permission or mount issues

---

## Validation Checklist

* [x] All storage backends show `active`
* [x] Disk usage within safe limits (<80%)
* [x] LVM volumes healthy
* [x] ISO/template storage accessible
* [x] No filesystem errors

---

## Expected Outcome

* Storage layer confirmed healthy
* Proxmox ready for VM provisioning
* Reduced risk of disk-related incidents

---

## Failure Awareness

Common storage-related failures:

* Thin pool exhaustion
* Filesystem mounted read-only
* Misconfigured storage backend

If detected:

* Stop further provisioning
* Create an incident record
* Recover before proceeding

---

## Engineering Principle Reinforced

> Never provision workloads on unvalidated storage.

Storage is a platform dependency, not an implementation detail.
