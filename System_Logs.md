# 📝 System Logs on Linux (For Pentesters & Admins)

System logs are a vital part of Linux system administration and security monitoring. These logs record events from various parts of the system, such as kernel messages, authentication attempts, application errors, and security events.

Understanding and monitoring these logs helps identify vulnerabilities, detect intrusions, and verify the effectiveness of security measures during penetration testing or system audits.

---

## 📁 Why Logs Matter

Logs provide:

* 📊 System behavior insights
* 🔐 Authentication attempts
* 🚨 Intrusion alerts
* ⚠️ Application errors
* 🧪 Feedback on testing activities

Proper log configuration ensures integrity, confidentiality, and visibility into system events.

---

## 📂 Types of Logs

### 🧠 Kernel Logs (`/var/log/kern.log`)

Contain:

* Hardware events
* Driver issues
* Kernel calls and system crashes

Useful for spotting:

* Crashes or system faults
* Malicious system calls
* DoS indicators

### ⚙️ System Logs (`/var/log/syslog` or `/var/log/messages`)

Contain:

* Service start/stop messages
* Login events
* Cron jobs

Example:

```text
Feb 28 15:00:01 CRON[2715]: (root) CMD (/usr/local/bin/backup.sh)
Feb 28 15:04:22 sshd[3010]: Failed password for htb-student from 10.14.15.2 port 50223 ssh2
Feb 28 15:07:19 sshd[3010]: Accepted password for htb-student from 10.14.15.2 port 50223 ssh2
```

### 🔐 Authentication Logs (`/var/log/auth.log`)

Contain:

* Successful/failed logins
* sudo activity
* SSH key logins

Example:

```text
Feb 28 18:15:01 sshd[5678]: Accepted publickey for admin from 10.14.15.2 port 43210 ssh2
Feb 28 18:15:03 sudo: admin : TTY=pts/1 ; COMMAND=/bin/bash
```

### 📦 Application Logs

Locations vary by application:

* Apache: `/var/log/apache2/error.log`
* MySQL: `/var/log/mysql/error.log`
* PostgreSQL: `/var/log/postgresql/postgresql-*.log`

Access logs reveal usage patterns and potential exploit attempts.

Example:

```text
2023-03-07T10:15:23 privileged.sh: htb-student accessed /root/hidden/api-keys.txt
```

Common access log locations:

| Service    | Log File Path                         |
| ---------- | ------------------------------------- |
| Apache     | /var/log/apache2/access.log           |
| Nginx      | /var/log/nginx/access.log             |
| OpenSSH    | /var/log/auth.log or /var/log/secure  |
| MySQL      | /var/log/mysql/mysql.log              |
| PostgreSQL | /var/log/postgresql/postgresql-\*.log |
| Systemd    | /var/log/journal/                     |

### 🛡️ Security Logs

Security tools log activity in various files:

* **Fail2ban**: `/var/log/fail2ban.log`
* **UFW**: `/var/log/ufw.log`
* Other alerts may appear in `/var/log/syslog` or `/var/log/auth.log`

Use these logs to:

* Detect brute force attacks
* Monitor firewall activity
* Check audit and access records

---

## 🔍 Tools for Log Analysis

Use command-line tools:

```bash
tail -f /var/log/syslog         # Live view
grep 'Failed' /var/log/auth.log # Search for failed logins
less /var/log/kern.log          # Read with navigation
```

Or log viewers like `journalctl` for systemd logs:

```bash
journalctl -xe    # Show most recent logs
```

---

## ✅ Best Practices

* 🔐 Protect log file permissions
* 🔁 Enable log rotation (`/etc/logrotate.conf`)
* 📆 Review logs regularly
* 🚨 Set up log monitoring alerts

> 🧠 Logs don’t lie. They’re your first line of defense when things go wrong.

---

By mastering Linux logs, you gain visibility into both normal and malicious behavior. Whether you're securing systems or breaking into them (ethically!), logs are your map of activity. 🕵️
