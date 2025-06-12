## User Management

User management is a core skill in Linux system administration. Whether you're setting up a new workstation, securing resources, or performing system audits — understanding how to manage users and groups is essential.

---

### 🔍 Concept Explanation

In Linux:

- A **user** is an individual account that interacts with the system.
- A **group** is a collection of users with shared permissions.

Admins frequently:

- Create user accounts.
- Assign users to groups to control access.
- Allow users to execute commands as other users (e.g., root) using tools like `sudo`.

---

### 🧪 Real-World Example

Imagine a new employee named **Alex** joins your company. You, as the system administrator, need to:

- Create a user account for `alex`.
- Add Alex to relevant groups (like developers or testers).
- Ensure Alex can perform certain tasks with elevated privileges using `sudo`.

---

### 🔐 Viewing Protected Files (Permissions in Action)

Let's try viewing a protected file:

```bash
cat /etc/shadow
```

**Output:**

```bash
cat: /etc/shadow: Permission denied
```

> 🔒 `/etc/shadow` contains encrypted password data. Only **root** has permission to read it.

To access it with elevated privileges:

```bash
sudo cat /etc/shadow
```

**Example output (snipped for security):**

```bash
root:<SNIP>:18395:0:99999:7:::
daemon:*:17737:0:99999:7:::
bin:*:17737:0:99999:7:::
```

---

### ⚙️ Common User Management Commands

| Command       | Description                                                                          |
|---------------|--------------------------------------------------------------------------------------|
| `sudo`        | Execute a command as another user (default is root).                                |
| `su`          | Switch user. Requests credentials and opens a new shell as that user.               |
| `useradd`     | Create a new user.                                                                  |
| `userdel`     | Delete a user and optionally remove their files.                                    |
| `usermod`     | Modify an existing user account.                                                    |
| `addgroup`    | Create a new group.                                                                 |
| `delgroup`    | Delete an existing group.                                                           |
| `passwd`      | Change user password.                                                               |

---

### 📌 Practical Syntax & Examples

#### ➕ Create a User and Home Directory

```bash
sudo useradd -m alex
```

- `-m` ensures a home directory is created at `/home/alex`.

#### 🔒 Lock a User Account

```bash
sudo usermod --lock alex
```

- `--lock` disables a user without deleting them.

#### 👤 Run a Command as Another User

```bash
su --command "ls /root" root
```

- `--command` executes a specific command as another user (here, `root`).

---

### 🧪 Try It Yourself (HTB Academy-Style Tasks)

#### ✅ Task 1: Create a user with a home directory

```bash
sudo useradd -m sam
```

#### ✅ Task 2: Lock a user account

```bash
sudo usermod --lock sam
```

#### ✅ Task 3: Run a command as a different user

```bash
su --command "whoami" root
```

> Expected Output:  
> `root`

---

### 🧠 Quiz Answers

- **Which option creates a home directory with `useradd`?**  
  ✅ `-m`

- **Which option locks a user with `usermod` (long version)?**  
  ✅ `--lock`

- **Which option allows executing a command with `su` (long version)?**  
  ✅ `--command`

---

### ✅ Quick Recap

- Use `useradd -m` to create a user **with** a home directory.
- Use `usermod --lock` to temporarily disable an account.
- Use `sudo` or `su --command` to execute commands as other users (usually root).
- Critical files like `/etc/shadow` are protected — only root can access them.

---

### 💡 Final Tip

Don't be afraid to explore. Mistakes in a controlled environment are the best way to learn. If something breaks — just reset the machine and try again!

