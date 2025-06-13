# ☀️ Solaris Overview (For Sysadmins & Security Pros)

Solaris is a powerful Unix-based operating system developed by **Sun Microsystems** (later acquired by **Oracle Corporation**). Known for its **stability, scalability**, and support for **enterprise-grade workloads**, it's used in mission-critical environments like finance, government, and cloud infrastructure.

---

## 🎯 Why Solaris?

* ✅ Robust OS for high-end servers
* 🧠 Built-in hypervisor (Oracle VM Server for SPARC)
* 🔐 Advanced security: RBAC, Mandatory Access Controls
* ⚙️ Ideal for database, virtualization, and big data workloads

---

## 🆚 Solaris vs Linux Distros

| Feature            | Solaris                             | Linux (Ubuntu, CentOS, etc.) |
| ------------------ | ----------------------------------- | ---------------------------- |
| Licensing          | Proprietary (Oracle)                | Mostly Open Source           |
| Package Manager    | IPS / pkgadd                        | APT / YUM / DNF              |
| Filesystem Tools   | ZFS native, SMF for service control | Ext4/XFS, systemd            |
| Process Monitoring | `truss`, `pfiles`                   | `strace`, `lsof`             |
| NFS Management     | `share`, `/etc/dfs/dfstab`          | `exportfs`, `/etc/exports`   |
| Privilege Mgmt     | Role-Based Access Control (RBAC)    | sudo                         |

---

## 🗂️ Key Solaris Directories

| Directory | Purpose                           |
| --------- | --------------------------------- |
| `/`       | Root of filesystem                |
| `/bin`    | Essential system binaries         |
| `/kernel` | Kernel modules and files          |
| `/etc`    | System configuration              |
| `/opt`    | Optional 3rd-party software       |
| `/proc`   | Kernel and process information    |
| `/var`    | Logs, mail, printer spools        |
| `/usr`    | System-wide read-only data, tools |
| `/home`   | User home directories             |
| `/mnt`    | Temporary mount points            |
| `/tmp`    | Temporary files                   |

---

## 🧰 Common Admin Tasks in Solaris

### 🔍 System Info

```bash
uname -a               # Linux
showrev -a             # Solaris
```

### 📦 Package Installation

```bash
sudo apt-get install apache2     # Ubuntu
pkgadd -d SUNWapchr              # Solaris
```

### 🔐 File Permissions

```bash
chmod 700 file
find / -perm -4000               # Solaris SUID files
```

### 🌐 NFS Sharing

```bash
share -F nfs -o rw /export/home                      # Solaris Share
mount -F nfs server:/nfs_share /mnt/local            # Solaris Mount
cat /etc/dfs/dfstab                                  # Solaris NFS config
```

---

## 🔎 Process & Syscall Tracing

### Solaris

```bash
pfiles `pgrep httpd`          # Open files by process
truss ls                      # Trace syscalls (like strace)
```

### Ubuntu

```bash
lsof -c apache2               # Open files by process
strace -p $(pgrep apache2)    # Syscall tracing
```

---

## 🛡️ Security in Solaris

* Uses **RBAC** instead of sudo for finer control
* Supports **MAC** and audit trails
* Enterprise-grade **ZFS** with snapshots & rollback

---

Solaris may not be as trendy as Linux, but it's a beast in the enterprise world. If you're in a pentest, system hardening gig, or just curious about legacy and high-performance systems—understanding Solaris gives you a serious edge.

> 🧠 Know your \*nix. Know your battlefield.
