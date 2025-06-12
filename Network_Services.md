# Linux Network Services

This document serves as a detailed summary of key network services in Linux, especially from a penetration tester's and sysadmin's perspective. It combines practical usage, real-world relevance, installation/configuration steps, and the role of each service in security assessments.

---

## 📌 Overview

Managing network services is crucial in Linux environments. These services enable remote operations, file sharing, traffic analysis, and secure communication. Understanding them helps:

* Identify misconfigurations
* Conduct effective penetration tests
* Strengthen system and network security

### 💡 Scenario:

Imagine a penetration test on a Linux host. Monitoring network traffic reveals that a user connects to another server using **unencrypted FTP**. As a result, their credentials are visible in plain text. This vulnerability could've been avoided if secure protocols like **SFTP** or **SCP** were used instead.

---

## 🔐 SSH (Secure Shell)

SSH is a secure protocol to access remote machines and transmit data safely over the network.

### ➕ Install OpenSSH Server

```bash
sudo apt install openssh-server -y
```

### ✅ Check SSH Server Status

```bash
systemctl status ssh
```

**Sample Output:**

```
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/system/system/ssh.service; enabled)
     Active: active (running) since...
```

### 🔗 Logging into Remote System

```bash
ssh username@IP_address
```

You may get a warning about authenticity if it's the first time connecting:

```
ECDSA key fingerprint is SHA256:...
Are you sure you want to continue connecting (yes/no)?
```

After confirmation, you're prompted for a password.

### ⚙️ Configuration

The main config file is:

```bash
/etc/ssh/sshd_config
```

Here you can adjust settings like:

* Login methods (password/key)
* Max sessions
* Root login permissions

SSH also allows tunneling and port forwarding for secure traffic redirection.

---

## 📁 NFS (Network File System)

NFS allows access to remote file systems as if they were local. Useful in shared environments and can be leveraged during a pentest if FTP isn't available.

### ➕ Install NFS

```bash
sudo apt install nfs-kernel-server -y
```

### ✅ Check NFS Server Status

```bash
systemctl status nfs-kernel-server
```

### 🛠 Config File

```bash
/etc/exports
```

Sample Entry:

```bash
/home/username/nfs_sharing hostname(rw,sync,no_root_squash)
```

### 🔗 Mounting on Client

```bash
mkdir ~/target_nfs
mount <server_ip>:/shared_directory ~/target_nfs
```

**Permissions Overview:**

| Permission       | Description                        |
| ---------------- | ---------------------------------- |
| `rw`             | Read/Write access                  |
| `ro`             | Read-only access                   |
| `no_root_squash` | Keep root privileges from client   |
| `root_squash`    | Map client root to normal user     |
| `sync`           | Write data immediately             |
| `async`          | Queue writes for speed (less safe) |

---

## 🌐 Web Servers

Web servers are central to hosting applications, transferring files, and even phishing simulations during a pentest.

### 📦 Apache Installation

```bash
sudo apt install apache2 -y
```

### ⚙️ Apache Configuration

```apacheconf
<Directory /var/www/html>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>
```

Apache settings are in:

```bash
/etc/apache2/apache2.conf
```

Drop files into `/var/www/html/` for download via `wget` or `curl`.

### 🔐 .htaccess

Use this file to set directory-specific controls like redirects or access restrictions without editing the main Apache config.

### 🔌 Useful Modules

* `mod_rewrite`
* `mod_security`
* `mod_ssl`

These add security features like URL rewriting, WAF rules, and HTTPS support.

---

## ⚙️ Python Web Server

A lightweight alternative to Apache for quick file transfers.

### 📦 Install Python

```bash
sudo apt install python3 -y
```

### 🚀 Launch Server

```bash
python3 -m http.server
```

### ➕ Serve a Different Folder

```bash
python3 -m http.server --directory /home/user/target_files
```

### 🔁 Use Custom Port

```bash
python3 -m http.server 443
```

Default port is `8000` unless specified. Access it via browser or `wget`.

---

## 🛡️ VPN (Virtual Private Network)

VPNs encrypt your traffic and connect you to internal networks as if you were physically present.

### 📦 Install OpenVPN

```bash
sudo apt install openvpn -y
```

### ⚙️ Configuration File

```bash
/etc/openvpn/server.conf
```

Edit to change:

* Encryption settings
* Port
* Protocol
* Routing behavior

### 🔗 Connect with .ovpn

```bash
sudo openvpn --config internal.ovpn
```

Once connected, you'll be part of the internal network—ideal for remote penetration tests.

---

## 📎 Final Words

Misconfigured or insecure network services are often exploited in real-world attacks. As penetration testers or system administrators, mastering these services allows us to:

* Harden systems against abuse
* Perform deeper, more efficient audits
* Build secure, reliable infrastructure

This guide summarizes the most practical tools and steps needed to work with SSH, NFS, Web Servers, Python HTTP Server, and OpenVPN in Linux environments.

> 👨‍💻 This summary is based on my learning from the Linux Fundamentals module on HTB Academy.

Feel free to fork, reference, or contribute. Happy hacking! 🐧🔐
