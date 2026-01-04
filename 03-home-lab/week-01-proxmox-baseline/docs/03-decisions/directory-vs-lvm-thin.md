# Directory vs LVM-Thin in Home Lab

### Decision ID

DEC-2026-WEEK-01

### Date

January 01, 2026

### Context

Setting up a Proxmox VE home lab on a single node (or small cluster) with a modest number of VMs (typically 5–20). Primary uses include experimentation, learning, running personal services (e.g., Pi-hole, Nextcloud, media servers), occasional testing of new OSes, and light development. The lab runs on consumer-grade hardware (e.g., old desktop and Rasperry pie 3 B+). Snapshots and clones are used occasionally but not heavily. Backups are performed regularly to external drives or NAS. Ease of management, troubleshooting, and data recovery are high priorities for a home user who is not a full-time sysadmin.

### Decision Made

Use Directory-based storage (file-based, typically on ext4 or XFS) for storing VM disk images instead of the default LVM-Thin storage.

### Rationale

* **Simplicity and ease of access**: VM disks are stored as regular files (e.g., vm-100-disk-0.qcow2 or .raw) in a directory (default /var/lib/vz/images/). This allows direct browsing, copying, moving, or mounting disks using standard Linux tools without needing LVM expertise. In a home lab, this drastically reduces troubleshooting time when something goes wrong.

* **Flexible mixed content**: The same "local" directory storage can hold VM disks, ISO images, backups, container templates, and snippets. No need to manage multiple separate storage pools.

* **Easy backups and recovery**: Individual disk files can be copied manually with rsync, cp, or even dragged via GUI file managers (e.g., over SMB). Restoring a single VM or disk is as simple as copying the file back. This aligns well with common home-lab backup strategies (external USB drive, NAS, or cloud sync).

* **Straightforward migration and portability**: Moving a VM to another Proxmox node, exporting to another hypervisor, or sharing a disk image is trivial—just copy the file(s).

* **Thin provisioning still available**: Using the qcow2 format provides efficient thin provisioning (space grows as needed) and supports internal snapshots when required, without relying on LVM-Thin features.
Lower complexity for beginners/intermediate users: Home labs often involve frequent experimentation. Avoiding block-device abstraction reduces the chance of accidentally breaking the thin pool or running into LVM-specific issues.

* **Performance is acceptable**: On modern SSDs, the slight overhead of file-on-filesystem is negligible for typical home-lab workloads (light servers, desktop VMs). The convenience outweighs the small performance gain of LVM-Thin.

### Risk

* Slightly lower I/O performance compared to LVM-Thin (extra filesystem layer).
* Potential for filesystem fragmentation over time with many create/delete operations (mitigated by using XFS or regular maintenance).
* Snapshots via qcow2 are slower and more resource-intensive than LVM-Thin snapshots.
* Instant linked clones are not available (must use full clone or backup/restore).
* Over-provisioning is possible with qcow2 but less aggressive than LVM-Thin (risk of running out of space if not monitored).

### Outcome

Expected: A more approachable, forgiving, and portable storage setup that prioritizes ease of use and quick recovery over maximum performance or advanced block-level features. The home lab remains reliable, easy to maintain, and simple to back up, with minimal risk of data loss due to storage complexity. Performance remains more than adequate for typical home-lab workloads.