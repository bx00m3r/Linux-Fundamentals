# File Descriptors and Redirections

A file descriptor (FD) in Unix/Linux operating systems is a reference, maintained by the kernel, that allows the system to manage Input/Output (I/O) operations. It acts as a unique identifier for an open file, socket, or any other I/O resource. In Windows-based operating systems, this is known as a file handle. Essentially, the file descriptor is the system's way of keeping track of active I/O connections, such as reading from or writing to a file.

Think of it as a ticket number you get when checking in your coat at a coatroom. The ticket (file descriptor) represents your connection to your coat (file or resource), and whenever you need to retrieve your coat (perform I/O), you present the ticket to the attendant (operating system) who knows exactly where your coat is stored (which resource the file descriptor refers to). Without the ticket, you'd have no way of efficiently accessing your coat among the many others stored, just as without a file descriptor, the operating system wouldn't know which resource to interact with. You will soon see why file descriptors are so important and why understanding them is crucial as we dive into the upcoming examples.

By default, the first three file descriptors in Linux are:

- **STDIN (Standard Input)** – FD 0
- **STDOUT (Standard Output)** – FD 1
- **STDERR (Standard Error Output)** – FD 2

## STDIN and STDOUT
Let us see an example with `cat`. When running `cat`, we give the running program our standard input (STDIN - FD 0), marked green, wherein this case "SOME INPUT" is. As soon as we have confirmed our input with [ENTER], it is returned to the terminal as standard output (STDOUT - FD 1), marked red.

```bash
~$ cat
```
![Image](https://academy.hackthebox.com/storage/modules/18/find0.png)

## STDOUT and STDERR
In the next example, by using the `find` command, we will see the standard output (STDOUT - FD 1) marked in green and standard error (STDERR - FD 2) marked in red.

```bash
~$ find /etc/ -name shadow
```
![Image](https://academy.hackthebox.com/storage/modules/18/find1.png)

In this case, the error is marked and displayed with "Permission denied." We can check this by redirecting the file descriptor for the errors (FD 2 - STDERR) to `/dev/null`. This way, we redirect the resulting errors to the "null device," which discards all data.

```bash
~$ find /etc/ -name shadow 2>/dev/null
```
![Image](https://academy.hackthebox.com/storage/modules/18/find2.png)

### Redirect STDOUT to a File
Now we can see that all errors (STDERR) previously presented with "Permission denied" are no longer displayed. The only result we see now is the standard output (STDOUT), which we can also redirect to a file with the name `results.txt` that will only contain standard output without the standard errors.

```bash
~$ find /etc/ -name shadow 2>/dev/null > results.txt
```
![Image](https://academy.hackthebox.com/storage/modules/18/find3.png)

### Redirect STDOUT and STDERR to Separate Files
We can also redirect standard error (FD 2 - STDERR) and standard output (FD 1 - STDOUT) to different files.

```bash
~$ find /etc/ -name shadow 2> stderr.txt 1> stdout.txt
```
![Image](https://academy.hackthebox.com/storage/modules/18/find4.png)

### Redirect STDIN
We use `cat` to use the contents of the file `stdout.txt` as STDIN.

```bash
~$ cat < stdout.txt
```
![Image](https://academy.hackthebox.com/storage/modules/18/find5.png)

### Redirect STDOUT and Append to a File
When using `>`, a new file is created if it does not already exist, or it overwrites an existing file. To append STDOUT to an existing file, use `>>`.

```bash
~$ find /etc/ -name passwd >> stdout.txt 2>/dev/null
```
![Image](https://academy.hackthebox.com/storage/modules/18/find9.png)

### Redirect STDIN Stream to a File
We can use the double less-than (`<<`) to add our standard input through a stream.

```bash
~$ cat << EOF > stream.txt
```
![Image](https://academy.hackthebox.com/storage/modules/18/find6.png)

## Pipes
Another way to redirect STDOUT is to use pipes (`|`). These allow us to process the output of one program with another. The `grep` command filters results based on a pattern.

```bash
~$ find /etc/ -name *.conf 2>/dev/null | grep systemd
```
![Image](https://academy.hackthebox.com/storage/modules/18/find7.png)

We can further process the filtered results using another tool, such as `wc`, which counts the total number of results.

```bash
~$ find /etc/ -name *.conf 2>/dev/null | grep systemd | wc -l
```
![Image](https://academy.hackthebox.com/storage/modules/18/find8.png)

By mastering file descriptors, redirections, and pipes, we can structure our commands efficiently, extract relevant information, and manipulate data flows effectively. This knowledge enhances productivity and precision when handling system resources and files.

