# 🗄️ Backup and Restore on Linux

Linux systems provide a range of powerful tools for backing up and restoring data, designed to be both efficient and secure. These tools help ensure that our data is not only protected from loss or corruption, but also easily accessible when we need it.

---

## 🧰 Backup Tools Overview

When backing up data on an Ubuntu system, we have several options, including:

* **Rsync** – Efficient, delta-based backup tool.
* **Deja Dup** – GUI-based backup solution.
* **Duplicity** – Encrypted, bandwidth-efficient backup utility.

---

## 🔄 Rsync

Rsync is an open-source tool that allows for fast and secure backups, whether locally or to a remote location.

### ✅ Install Rsync

```bash
sudo apt install rsync -y
```

### 📁 Backup a Local Directory to a Remote Server

```bash
rsync -av /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

### 📦 Compressed & Incremental Backup with Rsync

```bash
rsync -avz --backup --backup-dir=/path/to/backup/folder --delete /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

### 🔁 Restore from Remote Backup

```bash
rsync -av user@remote_host:/path/to/backup/directory /path/to/mydirectory
```

### 🔐 Encrypted Rsync via SSH

```bash
rsync -avz -e ssh /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

---

## 🤖 Automating Rsync with Cron

### 🔑 Generate SSH Key

```bash
ssh-keygen -t rsa -b 2048
ssh-copy-id user@backup_server
```

### 📝 RSYNC\_Backup.sh Script

```bash
#!/bin/bash
rsync -avz -e ssh /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

### 🔓 Make Script Executable

```bash
chmod +x RSYNC_Backup.sh
```

### ⏱️ Add to Crontab for Hourly Sync

```bash
crontab -e
```

Insert:

```cron
0 * * * * /path/to/RSYNC_Backup.sh
```

---

## 🧪 Local Rsync Lab (Pwnbox)

Create two directories:

```bash
mkdir ~/to_backup ~/synced_backup
```

Sync using loopback IP:

```bash
rsync -av ~/to_backup/ 127.0.0.1:~/synced_backup/
```

Automate with Cron every minute:

```cron
* * * * * rsync -av ~/to_backup/ 127.0.0.1:~/synced_backup/
```

---

## 🔐 Duplicity

Duplicity builds on Rsync and adds encryption. It works well with remote and cloud-based targets.

```bash
sudo apt install duplicity -y
```

Example usage:

```bash
duplicity /path/to/data file:///path/to/backup
```

For remote and encrypted backups:

```bash
duplicity /path/to/data sftp://user@host//remote/path
```

---

## 🖥️ Deja Dup

Deja Dup provides a user-friendly GUI for performing backups.

### 📦 Install

```bash
sudo apt install deja-dup -y
```

### 🔐 Features

* Scheduled backups
* Encryption
* Cloud support (Google Drive, etc.)

---

## 🧠 Final Thoughts

Think of your data as valuable treasures. Rsync is the fast courier, Duplicity is the armored truck with locks, and Deja Dup is the easy-to-use vault with automation. No matter your use case, Linux has a backup solution that suits your needs.

🔐 **Tip:** Always encrypt sensitive backups, especially if storing them remotely.

📁 This guide is part of my Linux Fundamentals journey. You can find other modules and resources in this repo. Happy Hacking!
