## Package Management

Package management is a crucial part of working with Linux. Whether you're maintaining a home system, managing a server, or building a penetration testing distro, you’ll need to install, update, and remove software — and for that, you use **package managers**.

---

### 🔍 Concept Explanation

* A **package** is a bundle of software files — including binaries, configuration files, metadata, and dependencies.
* A **package manager** is a tool that helps you:

  * Download software
  * Resolve dependencies automatically
  * Install/remove/configure software

Different Linux distros use different package formats:

* `.deb` for Debian-based (like Ubuntu, Kali, Parrot OS)
* `.rpm` for RedHat-based (like Fedora, CentOS)

**Dependencies** are other packages required for a program to run. A good package manager will detect and install them automatically.

---

### ⚙️ Common Package Management Tools

| Command    | Description                                                                  |
| ---------- | ---------------------------------------------------------------------------- |
| `dpkg`     | Low-level tool to install/manage `.deb` packages.                            |
| `apt`      | High-level tool for package installation with automatic dependency handling. |
| `aptitude` | Alternative to `apt`, with a text-based interface.                           |
| `snap`     | Manage Snap packages (used for cross-distro app distribution).               |
| `pip`      | Python’s package manager (used to install Python modules).                   |
| `gem`      | Ruby’s package manager.                                                      |
| `git`      | Version control tool, often used to clone/download source code.              |

---

### 📦 APT – Advanced Package Tool (for Debian-based systems)

#### View active repositories:

```bash
cat /etc/apt/sources.list.d/parrot.list
```

These lines show where your system pulls packages from.

#### Search for a package:

```bash
apt-cache search impacket
```

#### Show detailed info about a package:

```bash
apt-cache show impacket-scripts
```

#### List all installed packages:

```bash
apt list --installed
```

#### Install a package:

```bash
sudo apt install impacket-scripts -y
```

* `-y` auto-confirms the install prompt.

---

### 📂 Git (for Cloning Repositories)

Git allows you to download projects/tools directly from GitHub.

#### Example: Clone Nishang repository

```bash
mkdir ~/nishang && git clone https://github.com/samratashok/nishang.git ~/nishang
```

This downloads the **Nishang** PowerShell exploitation framework into your `~/nishang` folder.

---

### 📦 DPKG – Debian Package Tool (Manual Install)

You can manually download `.deb` files and install them using `dpkg`.

#### Download a `.deb` package:

```bash
wget http://archive.ubuntu.com/ubuntu/pool/main/s/strace/strace_4.21-1ubuntu1_amd64.deb
```

#### Install the package with `dpkg`:

```bash
sudo dpkg -i strace_4.21-1ubuntu1_amd64.deb
```

#### Verify installation:

```bash
strace -h
```

---

### 🧪 Try It Yourself

#### ✅ Task 1: Install `git` using APT

```bash
sudo apt install git -y
```

#### ✅ Task 2: Clone a repository using `git`

```bash
git clone https://github.com/samratashok/nishang.git ~/nishang
```

#### ✅ Task 3: Manually download and install a `.deb` package

```bash
wget http://archive.ubuntu.com/ubuntu/pool/main/s/strace/strace_4.21-1ubuntu1_amd64.deb
sudo dpkg -i strace_4.21-1ubuntu1_amd64.deb
```

#### ✅ Optional Task:

Search for **evil-winrm** on GitHub. Try cloning it and installing using both `git` and package manager (if available).

---

### 🧠 Quick Recap

✔ APT = Full-featured package manager for Debian-based systems.
✔ DPKG = Low-level tool for installing local `.deb` files.
✔ GIT = Download projects from GitHub.
✔ `apt-cache`, `apt list`, `apt install`, `dpkg -i` — Know these commands.
✔ Always update your repositories before installing:

```bash
sudo apt update
```

---
