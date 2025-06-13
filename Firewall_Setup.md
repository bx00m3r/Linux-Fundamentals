# 🔥 Linux Firewall Setup (iptables & More)

Firewalls are essential for controlling and monitoring network traffic. On Linux, they help prevent unauthorized access, block malicious packets, and enforce network segmentation. Whether you're a sysadmin or a pentester, understanding firewalls is vital to securing any environment.

---

## 🎯 Purpose of Firewalls

* Control traffic between network zones (e.g., internal ↔ external)
* Prevent unauthorized access and data exfiltration
* Enforce security policies

Linux has several firewall tools:

* `iptables` (classic, highly flexible)
* `nftables` (modern replacement for `iptables`)
* `ufw` (Uncomplicated Firewall – user-friendly)
* `firewalld` (zone-based dynamic firewall)

---

## 📜 A Brief History

* `ipfwadm` → `ipchains` → `iptables` (Linux 2.4+)
* `iptables` is based on the Netfilter framework (built into the kernel)
* `nftables` is the successor, offering better performance and cleaner syntax

---

## 🧱 Key Components of iptables

| Component   | Description                                           |
| ----------- | ----------------------------------------------------- |
| **Tables**  | Organize rules (e.g., `filter`, `nat`, `mangle`)      |
| **Chains**  | Group rules by traffic type (e.g., `INPUT`, `OUTPUT`) |
| **Rules**   | Define filtering criteria and actions                 |
| **Matches** | Conditions for filtering traffic (IP, port, protocol) |
| **Targets** | What to do when a rule matches (ACCEPT, DROP, etc.)   |

---

## 🧩 Tables and Built-in Chains

| Table  | Purpose                                 | Chains                                          |
| ------ | --------------------------------------- | ----------------------------------------------- |
| filter | Basic packet filtering                  | INPUT, OUTPUT, FORWARD                          |
| nat    | Network address translation             | PREROUTING, POSTROUTING                         |
| mangle | Modify packet headers                   | PREROUTING, INPUT, FORWARD, OUTPUT, POSTROUTING |
| raw    | Exempt packets from connection tracking | PREROUTING, OUTPUT                              |

---

## 📥 Chains

* **INPUT**: Incoming packets destined for the local system
* **OUTPUT**: Outgoing packets from the local system
* **FORWARD**: Packets routed through the system (not for local use)
* **PREROUTING**/**POSTROUTING**: For modifying packets before/after routing

User-defined chains can help organize complex rule sets.

---

## 📏 Rules & Targets

Each rule has:

* **Matches**: e.g., protocol, port, IP
* **Target**: action to take (ACCEPT, DROP, etc.)

**Example:** Allow incoming SSH on port 22

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

| Target     | Action                          |
| ---------- | ------------------------------- |
| ACCEPT     | Allow packet through            |
| DROP       | Silently discard packet         |
| REJECT     | Discard and notify source       |
| LOG        | Log packet to syslog            |
| SNAT/DNAT  | Source/Destination NAT          |
| MASQUERADE | Dynamic SNAT                    |
| REDIRECT   | Redirect to local port          |
| MARK       | Tag packet for later processing |

---

## 🧪 Matches: Filter Criteria

| Match                 | Description                                |
| --------------------- | ------------------------------------------ |
| `-p`                  | Protocol (tcp, udp, icmp)                  |
| `--dport` / `--sport` | Destination / Source Port                  |
| `-s` / `-d`           | Source / Destination IP                    |
| `-m state`            | Match connection states (NEW, ESTABLISHED) |
| `-m multiport`        | Match multiple ports                       |
| `-m string`           | Match string in packet                     |
| `-m limit`            | Rate-limit traffic                         |
| `-m mac`              | Match MAC addresses                        |

**Example:** Allow HTTP traffic:

```bash
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

---

## 🧰 Practical Tasks

1. **Block TCP/8080:**

```bash
sudo iptables -A INPUT -p tcp --dport 8080 -j DROP
```

2. **Allow TCP/8080:**

```bash
sudo iptables -D INPUT -p tcp --dport 8080 -j DROP
sudo iptables -A INPUT -p tcp --dport 8080 -j ACCEPT
```

3. **Block traffic from IP:**

```bash
sudo iptables -A INPUT -s 192.168.1.100 -j DROP
```

4. **Allow traffic from IP:**

```bash
sudo iptables -A INPUT -s 192.168.1.100 -j ACCEPT
```

5. **Block a protocol (e.g., ICMP):**

```bash
sudo iptables -A INPUT -p icmp -j DROP
```

6. **Allow a protocol:**

```bash
sudo iptables -A INPUT -p udp -j ACCEPT
```

7. **Create new chain:**

```bash
sudo iptables -N MYCHAIN
```

8. **Forward to custom chain:**

```bash
sudo iptables -A INPUT -j MYCHAIN
```

9. **Delete a rule (by line number):**

```bash
sudo iptables -L --line-numbers
sudo iptables -D INPUT <line_number>
```

10. **List all rules:**

```bash
sudo iptables -L -v -n
```

---

## ✅ Summary

Understanding and configuring Linux firewalls is essential to locking down a system. While `iptables` remains widely used, tools like `ufw`, `firewalld`, and `nftables` offer more user-friendly or advanced options. Choose the tool that fits your workflow and security needs. 🔐
