# 🔐 Linux Security (for Pentesters & Admins)

All systems carry some risk of intrusion. Linux, while generally more secure and less virus-prone than Windows, still needs proactive hardening — especially for systems exposed to the internet or used in sensitive environments.

---

## 📦 System Updates First!

Keeping the OS and installed packages updated is essential.

```bash
sudo apt update && sudo apt dist-upgrade
```

---

## 🔥 Firewalls & SSH Hardening

* Use `ufw`, `firewalld`, or `iptables` to restrict incoming/outgoing traffic.
* If SSH is enabled:

  * Disable root login
  * Disable password auth, use key-based login

```bash
sudo vim /etc/ssh/sshd_config
```

Inside:

```txt
PermitRootLogin no
PasswordAuthentication no
```

Then restart the service:

```bash
sudo systemctl restart sshd
```

---

## 👮 Principle of Least Privilege

* Don't use `root` unnecessarily.
* Limit sudo rights using `/etc/sudoers`.
* Define exact commands users can run with `sudo`.

Use `visudo` for safety:

```bash
sudo visudo
```

---

## 🚫 Fail2Ban: Protect From Brute Force

Fail2ban helps block IPs with too many failed login attempts.

```bash
sudo apt install fail2ban
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

---

## 🧾 Regular Audits & Checks

Check for:

* Kernel version vulnerabilities
* Misconfigured cron jobs
* World-writable files
* User permission issues

Tools:

* `chkrootkit`, `rkhunter`, `Lynis`
* `unattended-upgrades` for auto-patching

---

## 🛡️ MAC with SELinux & AppArmor

Use **Mandatory Access Control (MAC)** via SELinux or AppArmor.

* SELinux assigns *labels* to every process, file, and system object
* Rules define what access is permitted

You can manage SELinux with:

```bash
sestatus         # Check status
setenforce 1     # Enforce mode
```

---

## ✂️ Basic Hardening Checklist

✅ Remove unused services/software
✅ Disable plaintext auth services
✅ Enforce strong password policies
✅ Enable NTP & syslog
✅ Setup password aging policies
✅ Disable unused SUID/SGID binaries
✅ Use one account per user

> 🔁 Security is not a product, it’s a process.

---

## 📋 TCP Wrappers

TCP Wrappers control service access via IP/host rules using two config files:

* `/etc/hosts.allow`
* `/etc/hosts.deny`

Rules:

**Example `/etc/hosts.allow`**

```bash
sshd : 10.129.14.0/24
ftpd : 10.129.14.10
telnetd : .inlanefreight.local
```

**Example `/etc/hosts.deny`**

```bash
ALL : .inlanefreight.com
sshd : 10.129.22.22
ftpd : 10.129.22.0/24
```

> 📌 The first matching rule applies. Order matters!

TCP Wrappers are *not a firewall* replacement. They only control access to services — not specific ports.

---

## 🧠 Final Thoughts

The stronger your knowledge of Linux, the better your defenses. Keep learning, keep hardening. 🔒💪
