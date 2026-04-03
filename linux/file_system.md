# Linux Filesystem

## 1. Overview

The Linux filesystem is a hierarchical, unified structure that organizes all system resources under a single directory tree. It follows the core design principle:

> **“Everything is a file.”**

This abstraction enables consistent interaction with hardware devices, processes, and data through a common interface.

---

## 2. Filesystem Architecture

At the highest level, the Linux filesystem is structured as a tree:

```
/
├── bin
├── etc
├── home
├── var
├── usr
└── ...
```

* The root directory (`/`) is the entry point.
* Every file and directory exists within this tree.
* There are no separate drive letters (like `C:` or `D:` in Windows).

---

## 3. Filesystem Hierarchy Standard (FHS)

Linux distributions generally follow the **Filesystem Hierarchy Standard (FHS)**, which defines directory purposes.

### Key Directories

#### `/`

* Root of the entire filesystem.
* Contains all other directories.

#### `/home`

* User home directories.
* Example: `/home/user`

#### `/root`

* Home directory for the root user.

#### `/etc`

* System-wide configuration files.
* Typically text-based and editable.

#### `/bin`

* Essential user binaries (e.g., `ls`, `cp`, `mv`).

#### `/sbin`

* System binaries (used for administration).

#### `/usr`

* Secondary hierarchy for user applications and data.
* Not intended for direct modification by users.

Subdirectories:

* `/usr/bin` → user commands
* `/usr/lib` → libraries
* `/usr/share` → shared data

#### `/var`

* Variable data (logs, spool files, caches).
* Example: `/var/log`

#### `/tmp`

* Temporary files.
* Often cleared on reboot.

#### `/dev`

* Device files representing hardware components.

#### `/proc`

* Virtual filesystem exposing process and kernel data.

#### `/sys`

* Interface to kernel and hardware (sysfs).

#### `/mnt` and `/media`

* Mount points for external storage.

---

## 4. File Types in Linux

Each file has a type indicated by the first character in `ls -l` output.

| Symbol | Type              |
| ------ | ----------------- |
| `-`    | Regular file      |
| `d`    | Directory         |
| `l`    | Symbolic link     |
| `c`    | Character device  |
| `b`    | Block device      |
| `s`    | Socket            |
| `p`    | Named pipe (FIFO) |

Example:

```bash id="c1a9e2"
ls -l
```

---

## 5. Inodes

An **inode** (index node) is a data structure that stores metadata about a file.

### Contains:

* File size
* Ownership (UID, GID)
* Permissions
* Timestamps:

  * `atime` (access)
  * `mtime` (modification)
  * `ctime` (change)
* Pointers to data blocks

### Does NOT contain:

* Filename ❗

The mapping between filenames and inodes is stored in directories.

### Inspect inode:

```bash id="a8f3d1"
ls -i
```

---

## 6. Mounting and Filesystem Integration

Linux integrates multiple storage devices into a single directory tree using **mounting**.

### Manual mount:

```bash id="b7d2c4"
mount /dev/sdb1 /mnt
```

### Automatic mount configuration:

```bash id="d4e9fa"
cat /etc/fstab
```

Each entry defines:

* Device
* Mount point
* Filesystem type
* Mount options

---

## 7. Permissions and Ownership

Each file has:

* **User (owner)**
* **Group**
* **Others**

### Permission types:

* `r` → read
* `w` → write
* `x` → execute

Example:

```bash id="f2c7e1"
-rwxr-xr-- 1 user group file.sh
```

### Modify permissions:

```bash id="e6a4b9"
chmod 755 file.sh
```

### Change ownership:

```bash id="c9d1f8"
chown user:group file.sh
```

---

## 8. Links

### Hard Links

* Share the same inode.
* Data persists even if original filename is deleted.

```bash id="g3f8a1"
ln file.txt hardlink.txt
```

### Symbolic Links

* Reference another file path.
* Break if target is deleted.

```bash id="h7d2e6"
ln -s file.txt symlink.txt
```

---

## 9. Virtual Filesystems

Linux includes pseudo-filesystems that do not exist on disk.

### `/proc`

* Runtime process information.
* Example:

```bash id="k4b8f2"
cat /proc/cpuinfo
```

### `/sys`

* Kernel and hardware interface.

### `/run`

* Runtime state information (stored in RAM).

---

## 10. Disk Usage and Monitoring

### Disk free space:

```bash id="m8a3d7"
df -h
```

### Directory size:

```bash id="n1c9b4"
du -sh /var/log
```

---

## 11. Filesystem Types

Common Linux filesystems:

| Filesystem | Description                   |
| ---------- | ----------------------------- |
| ext4       | Default, stable, journaling   |
| xfs        | High performance, scalable    |
| btrfs      | Advanced (snapshots, pooling) |
| vfat       | FAT compatibility             |
| ntfs       | Windows interoperability      |

---

## 12. Journaling

Journaling filesystems maintain a log of changes before committing them.

### Benefits:

* Faster recovery after crashes
* Reduced risk of corruption

Common journaling filesystems:

* ext4
* xfs

---

## 13. Advanced Concepts

### File Descriptors

* Integers representing open files in a process.
* Standard descriptors:

  * `0` → stdin
  * `1` → stdout
  * `2` → stderr

---

### Access Control Lists (ACLs)

Provide more fine-grained permissions beyond traditional `rwx`.

```bash id="p2d7c9"
setfacl -m u:john:r file.txt
```

---

### Extended Attributes

Metadata stored beyond standard inode fields.

```bash id="q8e1f6"
getfattr -d file.txt
```

---

## 14. Best Practices

* Separate `/home`, `/var`, and `/` into different partitions in production systems.
* Monitor disk usage regularly (`df`, `du`).
* Rotate and manage logs (`/var/log`).
* Use journaling filesystems for reliability.
* Avoid running out of inodes (important in large-scale systems).
* Always back up before performing filesystem operations.

---

## 15. Summary

The Linux filesystem provides:

* A unified abstraction layer
* Strong modularity via mounting
* Fine-grained access control
* Flexibility for both small and large-scale systems

Understanding the filesystem deeply is essential for:

* System administration
* DevOps engineering
* Backend development
* Performance optimization

It forms the foundation of nearly all operations in a Linux environment.
