## Service and Process Management ⚙️🖥️

Services, also known as **daemons**, are background processes that run silently on Linux systems. These are essential for the system to function smoothly, performing tasks such as managing network connections 🌐, serving web pages 🌍, or automating regular updates 🔄.

There are two types of services:

### System Services 🧠

These start during system boot and handle critical operations — similar to an engine that powers a car 🚗.

### User-Installed Services 🎛️

These are extra functionalities added by users, like installing a web server or database — like adding GPS or music systems to a car 🎵🗺️.

Services often end in **`d`**, like `sshd` or `systemd`.

### Common Goals When Managing Services/Processes ✅

* Start or restart a service/process 🔄
* Stop a service/process 🛑
* View service/process status 📊
* Enable/disable service/process at boot 🚦
* Find and monitor services/processes 🔍

### systemd and systemctl 🛠️

Most modern Linux systems use **systemd** as their init system. It’s the first process to start and has PID 1. You can interact with it using the `systemctl` command.

```bash
# Start SSH service 🚀
systemctl start ssh

# Check status 📈
systemctl status ssh

# Enable on boot 🔁
systemctl enable ssh

# List running services 📋
systemctl list-units --type=service
```

### Checking SSH Logs 📜

Use `journalctl` to inspect logs related to a service:

```bash
journalctl -u ssh.service --no-pager
```

---

## Killing a Process 💀

Processes can be in states like **running**, **waiting**, **stopped**, or **zombie** 🧟. You can control them using:

* `kill` 🗡️
* `killall` 🚫
* `pgrep` 🔎
* `pkill` 💣

List all signal types:

```bash
kill -l
```

Common Signals:

* `SIGKILL (9)` – Force kill ❌
* `SIGTERM (15)` – Graceful stop 🛑
* `SIGSTOP (19)` – Pause ⏸️
* `SIGTSTP (20)` – Sent by Ctrl + Z 💤

Kill example:

```bash
kill -9 <PID>
```

---

## Background a Process 🧩

Use `[Ctrl + Z]` to suspend a foreground process.

```bash
ping -c 10 www.hackthebox.eu &
```

Check background jobs:

```bash
jobs
```

Resume suspended process in background:

```bash
bg
```

Bring it back to foreground:

```bash
fg <job_id>
```

---

## Execute Multiple Commands 🧠

* `;` runs all commands regardless of errors ⚠️
* `&&` runs next only if previous succeeds ✅
* `|` passes output of one as input to the next 🔗

Examples:

```bash
echo '1'; echo '2'; echo '3'
echo '1' && echo '2'
echo '1' && ls MISSING_FILE && echo '3'
```

---

## Practice Task 🧪📝

Use the following command in HTB Academy lab to find the unit name:

```bash
systemctl list-units --type=service
```

Answer: `snapd.apparmor.service` – Load AppArmor profiles managed internally by snapd 🔐
