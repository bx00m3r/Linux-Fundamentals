# 🗂️ File System Management in Linux

Managing file systems on Linux is a crucial task that involves organizing, storing, and maintaining data on a disk or other storage device. Linux supports various file systems, each suited for different use cases:

* **ext2**: Older file system, lacks journaling; useful for low-overhead use like USB drives.
* **ext3/ext4**: Includes journaling. ext4 is default in most Linux distros, offering reliability and performance.
* **Btrfs**: Advanced features like snapshots and data integrity checks; great for complex setups.
* **XFS**: High-performance file system for large files and high I/O environments.
* **NTFS**: Native to Windows, useful for dual-boot and external drives.

Choosing a file system depends on your needs: performance, compatibility, and reliability.

---

## 📁 Linux File System Architecture

Linux follows a Unix-like hierarchical file structure, anchored at the root `/`. Key concept: **Inodes**.

### 📌 Inodes

Inodes are metadata holders containing:

* File permissions, ownership, timestamps
* Pointers to data blocks (but not the data or file name itself)

Think of inodes as library catalog cards pointing to where the books (files) are stored.

```bash
$ ls -il
```

Example output:

```
10678872 -rw-r--r-- 1 cry0l1t3 htb 234123 Feb 14 19:30 myscript.py
10678869 -rw-r--r-- 1 cry0l1t3 htb  43230 Feb 14 11:52 notes.txt
```

---

## 📂 File Types in Linux

* **Regular files**: Text, binaries, etc.
* **Directories**: Containers for files or other directories.
* **Symbolic links**: Pointers to files or directories.

Permissions vary per user category (owner, group, others).

---

## 💽 Disk & Partition Management

Linux tools for disk and partition handling:

### 📊 `fdisk`

```bash
sudo fdisk -l
```

Lists disk info and partition tables.

Example:

```
/dev/vda1  *    2048 158974027 75.8G Linux
/dev/vda2       ...     4.2G Linux swap
```

Other tools: `gpart`, `GParted` (GUI).

---

## 🔗 Mounting File Systems

Mounting links a device/partition to a directory (mount point).

```bash
sudo mount /dev/sdb1 /mnt/usb
cd /mnt/usb && ls -l
```

To unmount:

```bash
sudo umount /mnt/usb
```

To check what's mounted:

```bash
mount
```

For permanent mounts, edit `/etc/fstab`:

```bash
cat /etc/fstab
```

Example entry:

```
/dev/sdb1 /mnt/usb ext4 rw,noauto,user 0 0
```

Use `lsof` to check if a mount is in use:

```bash
lsof | grep /mnt/usb
```

---

## 🔄 Swap Space in Linux

Swap acts as overflow memory when RAM is full.

### 🧱 Create Swap Space

```bash
sudo mkswap /swapfile
sudo swapon /swapfile
```

To make permanent, add to `/etc/fstab`:

```
/swapfile none swap sw 0 0
```

Swap is also used for hibernation.

---

## 🧪 Lab Task

👉 **How many partitions exist in our Pwnbox?**
✅ **Answer:** `3`
📌 **Command Used:**

```bash
sudo fdisk -l
```

---

📁 This document is part of my Linux Fundamentals series. More walkthroughs and notes available in my GitHub.

🔗 Happy Learning!
