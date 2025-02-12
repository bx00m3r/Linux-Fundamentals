# Getting Help

After building a solid understanding of Linux's structure, its distributions, and the shell's purpose, it's time to apply that knowledge. This section will guide you on how to use commands in the terminal and seek help when you encounter unfamiliar commands.

At some point, you’ll encounter commands with optional parameters that you might not remember, or tools you’ve never seen before. It's important to know how to seek help to familiarize yourself with those tools. The primary ways to seek help in Linux are through the `man` pages and the `--help` function. It's always a good practice to review the tool's help or documentation before using it. We'll also learn some tricks with tools that you might not have thought possible.

### Getting Help with `man`

The `man` command displays the manual pages for a given tool, providing detailed explanations on its usage, syntax, and available options. Here's an example of how to use `man` to get help for the `ls` command:

#### Syntax:
```bash
man <tool>
```

#### Example:
```bash
bx00m3r@htb[/htb]$ man ls
```

#### Output:
```
LS(1)                            User Commands                           LS(1)

NAME
       ls - list directory contents

SYNOPSIS
       ls [OPTION]... [FILE]...

DESCRIPTION
       List  information  about  the FILEs (the current directory by default).
       Sort entries alphabetically if none of -cftuvSUX nor --sort  is  speci‐
       fied.

       Mandatory  arguments  to  long  options are mandatory for short options
       too.

       -a, --all
              do not ignore entries starting with .

       -A, --almost-all
              do not list implied . and ..

       --author
```

To quickly see available options without reading the full documentation, you can use the `--help` flag:

#### Syntax:
```bash
<tool> --help
```

#### Example:
```bash
bx00m3r@htb[/htb]$ ls --help
```

#### Output:
```
Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

Mandatory arguments to long options are mandatory for short options too.
  -a, --all                  do not ignore entries starting with .
  -A, --almost-all           do not list implied . and ..
  --author                   with -l, print the author of each file
  -b, --escape               print C-style escapes for nongraphic characters
      --block-size=SIZE      with -l, scale sizes by SIZE when printing them;
                             e.g., '--block-size=M'; see SIZE format below
```

### Getting Help with `-h`

Some tools, like `curl`, offer a shorter version of help with the `-h` flag:

#### Syntax:
```bash
<tool> -h
```

#### Example:
```bash
bx00m3r@htb[/htb]$ curl -h
```

#### Output:
```
Usage: curl [options...] <url>
     --abstract-unix-socket <path> Connect via abstract Unix domain socket
     --anyauth       Pick any authentication method
 -a, --append        Append to target file when uploading
     --basic         Use HTTP Basic Authentication
     --cacert <file> CA certificate to verify peer against
     --capath <dir>  CA directory to verify peer against
 -E, --cert <certificate[:password]> Client certificate file and password
```

### Using `apropos` to Search for Commands

If you're unsure about a command but know a relevant keyword, you can use `apropos` to search for descriptions in the manual pages. It will return a list of commands related to your keyword.

#### Syntax:
```bash
apropos <keyword>
```

#### Example:
```bash
bx00m3r@htb[/htb]$ apropos sudo
```

#### Output:
```
sudo (8)             - execute a command as another user
sudo.conf (5)        - configuration for sudo front end
sudo_plugin (8)      - Sudo Plugin API
sudo_root (8)        - How to run administrative commands
sudoedit (8)         - execute a command as another user
sudoers (5)          - default sudo security policy plugin
sudoreplay (8)       - replay sudo session logs
visudo (8)           - edit the sudoers file
```

### Additional Resources

If you still have trouble understanding long commands or syntax, you can use the website [ExplainShell](https://explainshell.com/) to break down commands and explain their components.

### Summary

With these tools, you now have a solid understanding of how to seek help when using commands you're unfamiliar with or need more information about. Feel free to experiment with the tools and explore options at your own pace—it's always valuable to tinker and gain hands-on experience with the Linux command line.
