# Regular Expressions (RegEx) 🚀

Regular Expressions (RegEx) are like magic for text searching and manipulation! 🪄 They help you find, replace, and filter through text with pinpoint accuracy. Think of RegEx as a **super-smart text scanner** that can quickly find patterns in words, numbers, or special characters.

At its core, RegEx is just a **pattern of characters** that tells the computer what to look for. It’s widely used in programming languages, text editors, and Linux tools like `grep` and `sed` to analyze and process data efficiently.

---

## 📌 Grouping in RegEx

Grouping in RegEx lets you organize search patterns in different ways. Here’s how:

| Operator | Description |
|----------|-------------|
| `(a)` | Groups parts of a regex. Everything inside `()` is treated as a single unit. |
| `[a-z]` | Defines a **character class**, allowing you to match any character inside the brackets. |
| `{1,10}` | Defines **quantifiers**, meaning how many times a pattern should repeat. |
| `\|` | **OR operator** – matches either one pattern or another. |
| `.*` | Works like an **AND operator**, ensuring both patterns exist in order. |

---

## 🔍 Using OR (`|`) Operator

The `|` symbol allows you to search for one **or** the other. Example:

```bash
~$ grep -E "(my|false)" /etc/passwd
```

💡 This searches for lines containing **either** `my` or `false`.

**Example Output:**
```bash
lxd:x:105:65534::/var/lib/lxd/:/bin/false
pollinate:x:109:1::/var/cache/pollinate:/bin/false
mysql:x:116:120:MySQL Server,,:/nonexistent:/bin/false
```

---

## 🔍 Using AND (`.*`) Operator

If you need to find **both words together** in a specific order, use `.*` between them:

```bash
~$ grep -E "(my.*false)" /etc/passwd
```

💡 This will only show lines that contain **both** `my` and `false`, in the same order.

Another way to do this is by chaining `grep` commands:

```bash
~$ grep -E "my" /etc/passwd | grep -E "false"
```

💡 This first filters for `my`, then further filters for `false`.

---

## 🏆 **Optional Exercises** – Try These! 🔥

💪 Time to get hands-on! Open your **/etc/ssh/sshd_config** file and try these challenges using `grep`:

1️⃣ Show all lines **that do NOT contain** `#` (hint: use `-v`).  
2️⃣ Find all lines **starting with** the word `Permit`.  
3️⃣ Find all lines **ending with** the word `Authentication`.  
4️⃣ Search for all lines containing **the word** `Key`.  
5️⃣ Find lines **beginning with** `Password` and containing `yes`.  
6️⃣ Find all lines that **end with** `yes`.  

👉 Try these out and see how RegEx helps in real-world scenarios! 🚀

---

🎯 **RegEx is a powerful tool**—master it, and you’ll level up your text-searching and scripting skills! Keep practicing and experimenting. 💡
