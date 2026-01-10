# Inodes (Index Nodes)

This document explains **what inodes are, why they exist, and how they impact real Linux systems**. Inodes are one of the most misunderstood yet operationally critical Linux concepts.

This is **filesystem engineering knowledge**, not command memorization.

---

## 1. Why This Matters

Many production incidents are caused by inode-related misunderstandings:

* Disk shows space available but cannot create files
* Files appear deleted but disk usage does not drop
* Log rotation fails silently
* Applications crash with `ENOSPC` despite free disk space

Senior engineers do not ask:

> “Why is disk full?”

They ask:

> “Is this a block exhaustion problem or an inode exhaustion problem?”

---

## 2. What Is an Inode?

An **inode (index node)** is a **data structure used by Linux filesystems** to store metadata about a file.

An inode does **not** store:

* File name
* File contents

An inode **does** store:

* File type (regular, directory, symlink, etc.)
* Permissions (mode bits)
* Owner UID and GID
* File size
* Timestamps (atime, mtime, ctime)
* Link count
* Pointers to data blocks on disk

The filename is simply a **mapping to an inode number** stored inside a directory.

---

## 3. Filename vs Inode (Critical Distinction)

In Linux:

```
filename → inode → data blocks
```

Key implications:

* Multiple filenames can point to the same inode
* Removing a filename does not necessarily delete the data
* Data is freed only when:

  * Link count reaches zero **and**
  * No process is holding the file open

This explains many “ghost disk usage” incidents.

---

## 4. Inode Numbers in Practice

Every inode has a **unique inode number per filesystem**.

View inode numbers:

```
ls -i
```

Check inode usage:

```
df -i
```

Example output:

```
Filesystem  Inodes  IUsed   IFree IUse%
/dev/sda1  655360  655360      0  100%
```

This system is **inode-exhausted**, even if disk space is available.

---

## 5. Inode Exhaustion (Common Production Failure)

### How It Happens

* Millions of small files (logs, cache, temp files)
* Misconfigured applications writing tiny files
* Containers writing unbounded logs
* CI/CD artifacts not cleaned up

### Symptoms

* `touch file` fails
* `No space left on device` error
* Package installs fail
* Services refuse to start

Even though `df -h` shows free space.

---

## 6. Inodes and Directories

Directories are special files that contain:

```
filename → inode number
```

A directory does **not** store file metadata — it only maps names to inodes.

This is why:

* Renaming a file does not change inode
* Moving a file within the same filesystem is instant
* Moving across filesystems creates a new inode

---

## 7. Deleted Files Still Using Disk Space

One of the most critical inode-related incidents:

* File is deleted
* Disk usage remains high

Why?

* A running process still holds the inode open
* Link count = 0, but process reference > 0

Diagnose with:

```
lsof | grep deleted
```

Resolution:

* Restart the offending process
* Disk space is freed only after process exits

---

## 8. Inodes and Filesystem Design

Inodes are **pre-allocated** when a filesystem is created.

This means:

* You can run out of inodes before disk space
* Filesystem tuning matters

Example:

* ext4 on log-heavy systems
* CI runners
* Mail servers

Filesystem design is an **architectural decision**, not an afterthought.

---

## 9. Mapping Inodes to Cloud & Containers

| Linux Concept           | Cloud / Container Equivalent |
| ----------------------- | ---------------------------- |
| Inode exhaustion        | Pod crash / volume full      |
| Deleted open file       | Log container disk leak      |
| Millions of small files | Object store misuse          |

Inodes remain relevant even in Kubernetes.

---

## 10. Senior Engineer Mental Model

Always think in layers:

* Filesystem blocks (disk space)
* Inodes (file count)
* Open file descriptors

When disk issues appear, check **all three**.

---

## 11. You Should Now Clearly Understand

* What an inode is and what it stores
* Why filenames are not files
* How inode exhaustion occurs
* Why deleted files may still consume disk
* How inode issues cause real outages

---

## Next Step

Proceed to:

**Hard Links vs Soft Links**

That topic builds directly on inode mechanics and explains:

* Shared data blocks
* Symlink breakage
* Backup and restore pitfalls

This is where inode theory becomes operational muscle memory.
