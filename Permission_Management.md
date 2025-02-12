# Linux File Permissions 🔑

In Linux, permissions are like access keys 🗝️ that control who can do what with files and directories. Every file and folder has an **owner** (a user) and is also associated with a **group**. This setup ensures security and proper access control across the system.

## Understanding Permissions
Each file or directory has three permission sets:
- **Owner (User - u)** 👤
- **Group (g)** 👥
- **Others (o)** 🌍

Each of these has three types of access rights:
- **r (Read)** 📖 - View the file's contents.
- **w (Write)** ✏️ - Modify or delete the file.
- **x (Execute)** 🚀 - Run the file if it's a script or program.

### Example:
```bash
~$ ls -l
```
Output:
```
-rwxr-xr--  1 cry0l1t3 htbteam 0 May  4 22:12 shell
```
Breaking it down:
- **rwx** → Owner can read, write, and execute.
- **r-x** → Group can read and execute.
- **r--** → Others can only read.

## Traversing Directories 📂
Want to enter a directory? You need **execute (x) permission** on it. Without it, you’ll get a "Permission Denied" error—even if you can see its contents.

Example:
```bash
~$ ls -al mydirectory/
```
Output:
```
ls: cannot access 'mydirectory/script.sh': Permission denied
```
If you **don't** have `x` on a directory, you can't access its files.

## Changing Permissions 🔄
You can modify permissions using `chmod`.

### Symbolic Method:
```bash
~$ chmod a+r shell
```
This grants **read access to all users**.

### Octal Method:
Each permission type has a numeric value:
- Read (r) = `4`
- Write (w) = `2`
- Execute (x) = `1`

So, to set `rwxr-xr--` (754 in octal):
```bash
~$ chmod 754 shell
```

## Changing Owner & Group 🏷️
Use `chown` to change a file’s owner and group:
```bash
~$ chown root:root shell
```
Now, `shell` belongs to **root**.

## Special Permissions 🚨
### SUID (Set User ID) & SGID (Set Group ID) 🔼
These allow a program to **run as the owner or group**, regardless of who executes it. This is useful for admin tools but can be risky if misused.
- **SUID** (`s` instead of `x` in owner permissions)
- **SGID** (`s` instead of `x` in group permissions)

Example:
```bash
-rwsr-xr-x 1 root root 12345 Jan 1 00:00 somefile
```
Here, `somefile` runs **as root**, no matter who launches it.

⚠️ **Be careful** with SUID/SGID—it can be a security risk!

### Sticky Bit 📌
Used for shared directories—prevents users from **deleting or renaming files they don’t own**, even if they have write access.

Example:
```bash
~$ ls -ld /tmp
```
```
drwxrwxrwt 10 root root 4096 Jan 1 00:00 /tmp
```
- The **`t`** at the end means the sticky bit is set.
- Only the **owner** (or root) can delete files inside.

To set it manually:
```bash
~$ chmod +t mydir
```

---

Linux permissions may seem tricky at first, but once you get the hang of them, they’re super powerful. Play around with `chmod`, `chown`, and `ls -l` to get a feel for how they work! 🚀

