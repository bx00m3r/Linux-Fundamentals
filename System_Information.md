# Linux System Information and Basic Commands

## Introduction
Welcome to this guide on learning Linux system basics! Here, you'll find essential commands to get started with Linux, useful for both beginners and cybersecurity enthusiasts. If you're ever stuck, use the `-h`, `--help`, or `man` commands to access built-in help.

---

## Gathering System Information
Understanding your Linux system is important for performing basic tasks, securing configurations, and identifying potential vulnerabilities. Below are key commands to check system details, processes, network settings, users, and directories.

| **Command**   | **Description** |
|--------------|----------------|
| `whoami`     | Shows the current logged-in user. |
| `id`         | Displays user ID, group ID, and group memberships. |
| `hostname`   | Prints the system's hostname. |
| `uname`      | Provides system information such as OS and hardware details. |
| `pwd`        | Shows the current working directory. |
| `ifconfig`   | Displays or configures network interfaces (deprecated, use `ip` instead). |
| `ip`         | Shows/manages network interfaces, routing, and tunnels. |
| `netstat`    | Shows active network connections and listening services. |
| `ss`         | Alternative to `netstat`, useful for investigating sockets. |
| `ps`         | Displays active processes running on the system. |
| `who`        | Lists users currently logged into the system. |
| `env`        | Prints environment variables. |
| `lsblk`      | Lists block storage devices (e.g., hard drives, partitions). |
| `lsusb`      | Lists USB devices connected to the system. |
| `lsof`       | Lists open files (useful for debugging and security checks). |
| `lspci`      | Lists PCI devices (e.g., network cards, graphics cards). |

---

## Connecting via SSH
SSH (Secure Shell) is a protocol that allows secure remote access to Linux systems. It’s widely used by system administrators and cybersecurity professionals.

To connect to a remote machine, use:

```bash
ssh username@IP_address
```

Example:

```bash
ssh htb-student@192.168.1.100
```

This command lets you access the target system remotely via the terminal.

---

## Exploring System Information

### 1. Checking Hostname
The `hostname` command displays the name of the system.

```bash
hostname
```

Example output:
```
nixfund
```

---

### 2. Finding Your Username
To check the currently logged-in user, use:

```bash
whoami
```

Example output:
```
cry0l1t3
```

---

### 3. Checking User and Group IDs
The `id` command provides details about the user ID, group ID, and group memberships.

```bash
id
```

Example output:
```
uid=1000(cry0l1t3) gid=1000(cry0l1t3) groups=1000(cry0l1t3),1337(hackthebox),4(adm),27(sudo)
```
- Users in the `sudo` group have administrative privileges.
- `adm` group users can read log files.
- Membership in non-standard groups (e.g., `hackthebox`) may indicate special permissions.

---

### 4. Getting System Details
To view general system information, use:

```bash
uname -a
```

Example output:
```
Linux box 4.15.0-99-generic #100-Ubuntu SMP Wed Apr 22 20:32:56 UTC 2020 x86_64 GNU/Linux
```
This prints details like:
- **Kernel name**: Linux
- **Hostname**: box
- **Kernel version**: 4.15.0-99-generic
- **System architecture**: x86_64

To check only the kernel version:

```bash
uname -r
```

Example output:
```
4.15.0-99-generic
```
This is useful when searching for potential kernel exploits.

---

## Learning Through Practice
Studying Linux commands is crucial for system administration, penetration testing, and troubleshooting. To gain confidence:
1. Try executing these commands in a terminal.
2. Explore the `man` pages to learn more about each command (`man command`).
3. Experiment in a safe environment, such as a virtual machine.

### 🚀 Keep Practicing!
Every challenge helps you learn more. Don't hesitate to explore beyond what's listed here. Cybersecurity and Linux mastery come with continuous hands-on practice!

---
Happy learning! 🐧🚀
