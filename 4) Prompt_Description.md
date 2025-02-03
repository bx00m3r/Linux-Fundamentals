# Bash Prompt Customization

The bash prompt is an essential part of the command-line interface (CLI) in Linux. By default, it provides basic information such as your username, the system's hostname, and the directory you're currently in. It serves as a ready prompt for you to type commands.

### Default Prompt Format

The default bash prompt format looks something like this:

```bash
<username>@<hostname><current working directory>$
```

If you're in the home directory, it's represented by a tilde `<~>`. Here's what the prompt looks like when you are in your home directory:

```bash
<username>@<hostname>[~]$
```

When you switch to the root user, the prompt symbol changes from `$` to `#`:

```bash
root@htb[/htb]#
```

### Prompt During Shell Uploads

If you upload and run a shell on a target system, you might not see the username, hostname, and current working directory due to the PS1 variable not being set correctly. In this case, you might only see:

- **Unprivileged - User Shell Prompt:**

  ```bash
  $
  ```

- **Privileged - Root Shell Prompt:**

  ```bash
  #
  ```

### Customizing the Prompt with PS1

The PS1 variable controls the appearance of the bash prompt. It's a template that defines what information is displayed when the system is ready for you to enter a command. By modifying the PS1 variable, you can show details like your username, hostname, current directory, and even time or colors to personalize your terminal.

This customization is helpful, especially during penetration testing, as it allows you to track your actions and set up informative, visually appealing prompts. For example, you can set the prompt to display the full path of the current directory instead of just its name or include the target's IP address.

Additionally, tools like `script` or the `.bash_history` file can be used to document and track all the commands you've run.

### Special Characters for Customization

Here are some special characters you can use in your `.bashrc` file to customize the bash prompt:

| **Character**   | **Description**                               |
|-----------------|-----------------------------------------------|
| `\d`            | Date (Mon Feb 6)                              |
| `\D{%Y-%m-%d}`  | Date (YYYY-MM-DD)                            |
| `\H`            | Full hostname                                 |
| `\j`            | Number of jobs managed by the shell          |
| `\n`            | Newline                                       |
| `\r`            | Carriage return                               |
| `\s`            | Name of the shell                            |
| `\t`            | Current time (24-hour format HH:MM:SS)        |
| `\T`            | Current time (12-hour format HH:MM:SS)        |
| `\@`            | Current time (AM/PM format)                  |
| `\u`            | Current username                             |
| `\w`            | Full path of the current working directory   |

### How to Customize the Prompt

To customize your prompt, you'll need to edit your `.bashrc` file, located in your home directory. You can use the following variables to modify your prompt:

- `\u` — represents the current username
- `\h` — represents the hostname
- `\w` — represents the current working directory

For example, you can use the following to create a prompt that displays the username, hostname, and the full path of the current directory:

```bash
PS1="\u@\h:\w$ "
```

### Additional Customizations

Beyond modifying the appearance of the prompt, you can also customize the terminal environment with color schemes, fonts, and other settings to make your workspace visually appealing and user-friendly. Customizing your bash prompt allows for a more efficient and personalized terminal experience.

Although adjusting the bash prompt is outside the scope of this guide, tools like `bash-prompt-generator` and `powerline` can help you easily create and adapt prompts according to your needs.
