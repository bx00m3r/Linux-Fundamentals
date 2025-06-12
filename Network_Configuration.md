# 🌐 Linux Network Configuration

Understanding how to configure networks on Linux is *super important* — especially if you’re into ethical hacking, CTFs, or pentesting. Whether it’s setting up a test lab or manipulating traffic to find a vulnerability, knowing how to work with Linux networking will give you serious control over your testing environments and outcomes.

---

## 🛀 Network Interfaces: Your First Touchpoint

Think of network interfaces like the physical ports (Ethernet or Wi-Fi) on your device — except in Linux, they’re software-controlled and can be configured however we like.

Some common commands:

```bash
ifconfig             # Shows info about network interfaces
ip addr              # Modern replacement for ifconfig
```

Example output (shortened):

```bash
eth0: inet 192.168.1.2  netmask 255.255.255.0  broadcast 192.168.1.255
lo:   inet 127.0.0.1    (Loopback)
```

> **Note:** `ifconfig` is still widely used but technically deprecated. Prefer `ip` for modern systems.

---

## ⚙️ Common Interface Commands

**Activate an interface:**

```bash
sudo ifconfig eth0 up
# or
sudo ip link set eth0 up
```

**Assign an IP address:**

```bash
sudo ifconfig eth0 192.168.1.2
```

**Set a netmask:**

```bash
sudo ifconfig eth0 netmask 255.255.255.0
```

**Set default gateway:**

```bash
sudo route add default gw 192.168.1.1 eth0
```

These are basic but essential for manual configurations or during pentest setups when DHCP isn’t doing its job.

---

## 📶 DNS Configuration

Without DNS, your system doesn’t know that `google.com` means `142.250.182.78`.

To temporarily set DNS:

```bash
sudo vim /etc/resolv.conf
```

Inside:

```txt
nameserver 8.8.8.8
nameserver 8.8.4.4
```

🚨 *Heads up:* These changes may not survive a reboot, because `/etc/resolv.conf` might be auto-managed by tools like `NetworkManager`. For permanent changes, use:

```bash
sudo vim /etc/network/interfaces
```

Example static setup:

```txt
auto eth0
iface eth0 inet static
  address 192.168.1.2
  netmask 255.255.255.0
  gateway 192.168.1.1
  dns-nameservers 8.8.8.8 8.8.4.4
```

Apply changes:

```bash
sudo systemctl restart networking
```

---

## 🔒 Network Access Control (NAC)

Controlling *who* can access *what* is at the heart of security. In Linux, we use a few models:

| NAC Type                               | Description                                                              |
| -------------------------------------- | ------------------------------------------------------------------------ |
| **DAC** (Discretionary Access Control) | Owner sets permissions. Simple, but not very secure.                     |
| **MAC** (Mandatory Access Control)     | OS-enforced rules. More secure, less flexible. Think SELinux & AppArmor. |
| **RBAC** (Role-Based Access Control)   | Based on user roles. Great for teams.                                    |

We often enforce these using tools like:

* `SELinux` or `AppArmor` for MAC
* `TCP Wrappers` for IP-based service access
* `firewalld` / `iptables` to filter traffic

---

## 🛠️ Monitoring Traffic (A Pentester’s Binoculars)

Good networking is not just about configuration — it’s also about *observation*. Here are some key tools to watch the wires:

* `ss`: View open sockets and connections
* `lsof`: List open files (including sockets)
* `tcpdump`: Packet capture (like Wireshark in terminal)
* `ELK Stack` (Elastic + Logstash + Kibana): For log analysis and visualization

---

## 🏢 Networking = Building Infrastructure

Here’s a quick analogy to wrap this up:

> 🏗️ **Network interfaces** = the wires and ports in a smart office
> 🔐 **Access control** = security guards and room keys
> 📹 **Monitoring** = CCTV and alarms
> 🛠️ **Troubleshooting** = your toolkit (ping, nmap, nslookup)

Mastering these will give you the power to design, secure, and break networks—all from your Linux terminal. 💥

# 🛡️ Network Access Control (NAC)

Network Access Control (NAC) is a vital part of any secure network environment, especially in penetration testing. It ensures only authorized and compliant devices can connect, helping to prevent unauthorized access, data breaches, and security incidents.

## 🔐 NAC Technologies

### 1. Discretionary Access Control (DAC)

* **What it is**: Grants access control to resource owners.
* **How it works**: Owners assign permissions to users/groups.
* **Use case**: Common in user-level file and resource access scenarios.

### 2. Mandatory Access Control (MAC)

* **What it is**: Enforces access control based on security labels.
* **How it works**: A user's or process's clearance must match the resource's classification.
* **Use case**: High-security environments like military, healthcare, or finance.

### 3. Role-Based Access Control (RBAC)

* **What it is**: Assigns permissions based on user roles.
* **How it works**: Roles are mapped to permissions, and users are mapped to roles.
* **Use case**: Scalable environments like enterprise IT, large organizations.

---

## 📡 Network Monitoring

Used to capture and analyze traffic to detect threats, misconfigurations, or gather useful credentials.

### Tools:

* **Wireshark**
* **tshark**
* **Tcpdump**

🧠 Learn more in the *Intro to Network Traffic Analysis* module.

---

## 🛠️ Network Troubleshooting

Identify, diagnose, and resolve issues like:

* Network connectivity problems
* DNS resolution failures
* Packet loss and performance degradation

### Common Tools:

#### 🔁 `ping`

```bash
ping 8.8.8.8
```

#### 🌐 `traceroute`

```bash
traceroute www.inlanefreight.com
```

#### 📊 `netstat`

```bash
netstat -a
```

Common causes:

* Misconfigured firewalls
* Faulty cables or DNS settings
* Hardware failures or unpatched software

---

## 🔐 Hardening Linux Systems

Tools and modules to tighten security and protect against unauthorized access.

### 🔸 SELinux (Security-Enhanced Linux)

* Type: MAC
* Integrated into the kernel
* Offers fine-grained control but complex

### 🔹 AppArmor

* Type: MAC
* Easier to configure than SELinux
* Profile-based control over application access

### 🟩 TCP Wrappers

* Type: Network ACL
* Simple host-based access control
* Based on IP addresses

| Tool         | Type | Control Scope     | Complexity |
| ------------ | ---- | ----------------- | ---------- |
| SELinux      | MAC  | System-wide       | High       |
| AppArmor     | MAC  | Application-level | Medium     |
| TCP Wrappers | ACL  | Network services  | Low        |

---

## 🧪 Practice Tasks (Recommended on a VM with snapshots)

### SELinux

1. Install SELinux.
2. Restrict file access to specific users.
3. Allow one user to access a service, deny others.
4. Deny a group from accessing a service.

### AppArmor

5. Prevent file access using profiles.
6. Allow a specific user access to a network service.
7. Deny access to a group for a service.

### TCP Wrappers

8. Allow service access from a specific IP.
9. Deny service access from a specific IP.
10. Allow access from an IP range.

---

💬 **Tip**: Share your configuration approaches or issues in a community like Discord! Explaining what you’ve learned helps solidify your understanding.

---

📘 [Back to Linux Fundamentals Roadmap](https://github.com/bx00m3r/linux-fundamentals)

🔗 Find more such walkthroughs, summaries, and challenges at: [GitHub @bx00m3r](https://github.com/bx00m3r)

Happy Hacking! 🧑‍💻
