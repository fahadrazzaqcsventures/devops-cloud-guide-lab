# Hard Links vs Soft Links

This document explains **how Linux links work at the filesystem level**, why they exist, and how misunderstanding them causes real production failures.

This is not a command cheat sheet. This is **filesystem engineering knowledge**.

---

## 1. Why This Matters

Engineers often treat files as if they are:

> "Just names pointing to data"

In Linux, this is **incorrect and dangerous**.

Understanding links explains:

* Why deleting a file does not always free disk space
* Why some files cannot be linked across filesystems
* Why containers and logs behave unexpectedly
* Why backups sometimes miss data

Senior engineers reason in **inodes and references**, not filenames.

---

## 2. The Core Concept (Recap)

A Linux file consists of:

* **Inode** → metadata + pointer to data blocks
* **Directory entry** → filename → inode number

A link is simply **another reference to an inode**.

---

## 3. Hard Links

### What Is a Hard Link?

A hard link is:

> An additional directory entry pointing to the **same inode**

All hard links are **equal peers**.

There is no "original" file.

---

### Hard Link Characteristics

* Points directly to the same inode
* Shares the same data blocks
* Inode link count increases
* File exists until **last hard link is removed**

Deleting one name does **not** delete the data.

---

### Hard Link Example

```
ln fileA fileB
```

Now:

* `fileA` → inode 12345
* `fileB` → inode 12345

Deleting `fileA` leaves `fileB` fully functional.

---

### Hard Link Limitations

Hard links:

* ❌ Cannot span filesystems
* ❌ Cannot link directories (to prevent loops)
* ✅ Are fast and storage-efficient

---

## 4. Soft Links (Symbolic Links)

### What Is a Soft Link?

A soft link is:

> A special file that contains a **path to another file**

It does **not** point to the inode directly.

---

### Soft Link Characteristics

* Has its own inode
* Stores a path string
* Can cross filesystems
* Can link directories
* Can become **dangling**

---

### Soft Link Example

```
ln -s /var/log/app.log current.log
```

If `/var/log/app.log` is deleted:

* `current.log` still exists
* But points to **nothing**

---

## 5. Key Differences

| Feature                     | Hard Link | Soft Link |
| --------------------------- | --------- | --------- |
| Points to inode             | Yes       | No        |
| Own inode                   | No        | Yes       |
| Cross filesystems           | No        | Yes       |
| Link directories            | No        | Yes       |
| Dangling possible           | No        | Yes       |
| Affected by target deletion | No        | Yes       |

---

## 6. Real Production Scenarios

### Scenario 1: Disk Full but Files Deleted

Cause:

* Large file deleted
* Process still holding a hard-linked inode

Result:

* Disk space not freed

---

### Scenario 2: Broken Config or Binary

Cause:

* Soft link pointing to versioned file
* Target removed during upgrade

Result:

* Service fails to start

---

### Scenario 3: Log Rotation Confusion

Cause:

* Application writes to inode
* Logrotate replaces filename

Result:

* Logs grow invisibly

---

## 7. Containers and Links

Containers heavily use:

* Hard links for shared layers

* Soft links for versioned binaries
  n
  Breaking these assumptions causes:

* Image corruption

* Unexpected disk usage

---

## 8. Mental Model (Senior Engineer Level)

Think this way:

* Filenames are **labels**
* Inodes own data
* Hard links share ownership
* Soft links are fragile pointers

If you reason in filenames, you will misdiagnose incidents.

---

## 9. You Should Now Clearly Understand

* Difference between hard and soft links
* Why deleting files doesn’t always free space
* Why soft links break and hard links don’t
* When each type is appropriate
* How links affect production incidents

---

## Next Step

Proceed to:

**Permissions & Ownership**

You now understand *what* files are. Next, you learn *who can access them and why*.
