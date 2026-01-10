# Linux File Types

This document explains **the different types of files in Linux**, what they represent at the kernel level, and how misunderstanding them leads to common production failures.

File types are **not cosmetic** — they define how the kernel treats data, devices, and communication channels.

---

## 1. Why This Matters

Junior engineers think:

> “Everything is a file.”

Senior engineers add:

> “But not every file behaves the same.”

Misunderstanding file types causes:

* Broken services
* Permission errors that make no sense
* Accidental deletion of critical interfaces
* Container and Kubernetes failures

---

## 2. Core Principle: Everything Is a File (But Typed)

Linux represents:

* Disks
* Terminals
* Sockets
* Processes

as files — **with different file types handled by the kernel**.

You must know which types are safe to edit, delete, or redirect.

---

## 3. Regular Files (`-`)

### Description

* Standard data files
* Text or binary

Examples:

* Scripts
* Logs
* Configuration files

Command:

```
ls -l
-rw-r--r-- 1 root root 4096 app.conf
```

Safe operations:

* Read
* Write
* Copy

---

## 4. Directories (`d`)

### Description

* Containers for file names and inode references

Command:

```
ls -ld /etc
drwxr-xr-x 1 root root
```

Key rule:

> Permissions on directories control **access to files inside**.

---

## 5. Symbolic Links (`l`)

### Description

* Pointer to another file path
* Breaks if target is removed

Command:

```
ls -l
lrwxrwxrwx 1 root root file -> /etc/file
```

Common usage:

* Versioned binaries
* Config indirection

---

## 6. Character Devices (`c`)

### Description

* Stream-based device access
* No buffering

Examples:

* `/dev/null`
* `/dev/tty`

Command:

```
crw-rw-rw- 1 root root 1,3 /dev/null
```

Deleting device files breaks system behavior.

---

## 7. Block Devices (`b`)

### Description

* Buffered device access
* Storage devices

Examples:

* `/dev/sda`
* `/dev/vda`

Command:

```
brw-rw---- 1 root disk 8,0 /dev/sda
```

Used by:

* Filesystems
* LVM
* Mount operations

---

## 8. Named Pipes / FIFOs (`p`)

### Description

* One-way inter-process communication

Example:

```
mkfifo mypipe
```

Common pitfall:

> Commands hang waiting for input.

---

## 9. Sockets (`s`)

### Description

* Two-way communication endpoints

Examples:

* systemd sockets
* Docker socket `/var/run/docker.sock`

Deleting sockets can stop services.

---

## 10. Special Virtual Files

### `/proc` and `/sys`

* Kernel-exposed interfaces
* Not real files on disk

Writing incorrect values can crash systems.

---

## 11. Production Failure Mapping

| Symptom                   | Likely File Type Issue   |
| ------------------------- | ------------------------ |
| Service won’t start       | Socket or config missing |
| Disk not mounting         | Block device issue       |
| Script hangs              | FIFO waiting             |
| Permissions make no sense | Directory execute bit    |

---

## 12. You Should Now Clearly Understand

* All Linux file types and identifiers
* Which files are safe vs dangerous to modify
* Why device files matter
* How IPC uses file abstractions
* How file types impact services and containers

---

## Next Topic

👉 **Inodes**

You must understand inodes before links, permissions, and disk usage.

Say:
**Next: Inodes**
