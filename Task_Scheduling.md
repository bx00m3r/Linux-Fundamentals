## Task Scheduling ⏰🗓️

Task scheduling is a critical feature in Linux that allows users and administrators to **automate tasks** at specific times or intervals — no manual intervention needed 🙌. Distributions like Ubuntu, Red Hat, and Solaris use it to handle:

* 🔄 Software updates
* 📜 Script execution
* 🛠️ Maintenance
* 💾 Backups
* 📢 Alerts & Notifications

Think of it like setting a coffee maker to brew automatically every morning ☕ — reliable, repeatable, and no human required.

As **cybersecurity specialists or penetration testers**, knowing how task scheduling works is essential. Why?

* 🕵️‍♂️ Catch malicious cron jobs
* 🔒 Detect persistence mechanisms
* 🧪 Simulate attacks with scheduled scripts

---

### Systemd Timers 🔧🕒

Modern Linux distros use **Systemd** to manage services, including timed tasks.
To create a task with Systemd:

1. Create a **timer** file ⏱️
2. Create a **service** file 📄
3. Reload & enable them ✅

#### 🛠️ Step-by-Step

```bash
# Create a timer directory (optional)
sudo mkdir /etc/systemd/system/mytimer.timer.d

# Create the timer file
sudo vim /etc/systemd/system/mytimer.timer
```

**mytimer.timer**

```ini
[Unit]
Description=My Timer

[Timer]
OnBootSec=3min
OnUnitActiveSec=1hour

[Install]
WantedBy=timers.target
```

* `OnBootSec`: Run 3 minutes after boot
* `OnUnitActiveSec`: Run every hour

```bash
# Create the service file
sudo vim /etc/systemd/system/mytimer.service
```

**mytimer.service**

```ini
[Unit]
Description=My Service

[Service]
ExecStart=/full/path/to/my/script.sh

[Install]
WantedBy=multi-user.target
```

Reload and activate everything:

```bash
sudo systemctl daemon-reload
sudo systemctl start mytimer.timer
sudo systemctl enable mytimer.timer
```

---

### Cron 🕓📋

**Cron** is another tool for scheduling. It uses a **crontab** file to define time-based jobs.

#### ⌚ Time Fields in Crontab:

| Field        | Range | Meaning          |
| ------------ | ----- | ---------------- |
| Minute       | 0-59  | At which minute  |
| Hour         | 0-23  | At which hour    |
| Day of Month | 1-31  | Which day        |
| Month        | 1-12  | Which month      |
| Day of Week  | 0-7   | 0 and 7 = Sunday |

#### ✍️ Example Crontab Entries:

```cron
# Every 6 hours
0 */6 * * * /path/to/update_software.sh

# First day of month at midnight
0 0 1 * * /path/to/scripts/run_scripts.sh

# Every Sunday (0 or 7)
0 0 * * 0 /path/to/scripts/clean_database.sh
0 0 * * 7 /path/to/scripts/backup.sh
```

🔔 You can configure notifications and logging for task success or failure.

---

### Systemd vs Cron ⚖️

| Feature       | Systemd ⛓️               | Cron ⏱️         |
| ------------- | ------------------------ | --------------- |
| Config Type   | Timer + Service files 📁 | Crontab file 📄 |
| Trigger Types | Time + Events 🧲         | Time only ⏳     |
| Logging       | Built-in 📘              | Manual setup 📂 |
| Flexibility   | High 🔀                  | Simpler 🧰      |

---

### Practice Task 🧪

📌 **Question**: What is the type of the service for `dconf.service`?

▶️ **Run this command in the HTB Academy lab:**

```bash
systemctl show dconf.service | grep Type
```

✅ **Answer**: `dbus` 🚍
