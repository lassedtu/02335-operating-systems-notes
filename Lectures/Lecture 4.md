# Operating System Execution and Processes

## Execution Modes

### Kernel Mode
Kernel mode is an unrestricted execution state where the processor has complete access to all hardware resources and system instructions.

### User Mode
User mode is a restricted execution environment with limited access to hardware and privileged instructions, designed to protect system stability and security.

## System Calls

To transition safely between user mode and kernel mode, programs utilize system calls to request privileged services or hardware interaction from the operating system kernel.

**Example (reading from a file descriptor):**
```c
read(fd, buffer, nbytes);
```

System calls return specific status codes to indicate execution success or error conditions.

## POSIX Standards

The Portable Operating System Interface (POSIX) is a standardized Application Programming Interface (API) framework designed to maintain source compatibility across distinct operating systems.

- **POSIX-Certified Operating Systems:** macOS, Solaris
- **POSIX-Compliant Operating Systems:** Linux, Android, FreeBSD, Contiki
- **Compatibility Layers:** Cygwin provides a POSIX-compatible emulation environment on Microsoft Windows.

---

# Processes

Operating systems manage active tasks through the concept of a process, which represents a program in execution.

## Process Architecture and Management

Each process maintains its own allocated memory space, CPU registers, open file descriptors, and associated system resources.

Modern operating systems support concurrent execution, allowing multiple processes to run in parallel on multi-core processors or via pseudo-parallelism (rapid context switching) on single-core systems.

The kernel maintains a system-wide data structure known as the process table to track all active, suspended, and terminated (zombie) processes. Every process is assigned a unique Process ID (PID) and an associated user owner for access control and security.

## Process Monitoring

To inspect the currently running processes in a Unix-like operating system, administrators and users query the process table using utilities such as:

```bash
ps -ef
```

This command generates a full-format listing of all active processes currently executing on the system, displaying details such as the UID, PID, parent PID (PPID), start time, terminal, and the command arguments associated with each execution thread.

---

## Process Creation and Forking

### The `fork()` System Call

![[tree.png|350]]

In Unix-like operating systems, a process can clone itself using the `fork()` system call. The process that initiates the clone is designated as the parent process, and the newly created duplicate is the child process.

The child process is allocated a distinct address space containing an exact duplicate of the parent process's memory contents at the time of the call.

`fork()` is the fundamental mechanism for process creation in these systems. Consequently, all active processes originate from a root ancestor (traditionally the `init` process). Process trees can be inspected using:

```bash
pstree
```

### Return Values of `fork()`

Because the child process is an exact copy of the parent, both resume execution at the instruction immediately following the `fork()` call. To allow the program to distinguish between the two execution paths, the system call returns different values:

- **To the parent process:** It returns the Process ID (PID) of the newly created child.
- **To the child process:** It returns `0`.

### Associated Process Management System Calls

#### `pid_t fork(void);`

This syscall clones the calling process, generating a new child process.

#### `pid_t getpid(void);`

This syscall returns the unique Process ID of the calling process.

#### `pid_t getppid(void);`

This syscall returns the Process ID of the parent process.

#### `void exit(int status);`

This syscall terminates the calling process and reports an exit status code to the operating system.

---

## Process Memory and Inter-Process Communication

### Separate Address Spaces

Following a `fork()` operation, the parent and child processes execute in isolated address spaces. Because these memory regions are independent, processes cannot directly exchange data through standard global variables or heap allocations.

### Shared Memory Allocation

To bypass this isolation and enable efficient inter-process communication (IPC), processes can request a designated memory region from the operating system kernel that is mapped concurrently into multiple address spaces.

### System Calls

```c
void *mmap(void *addr, size_t len, int prot, int flags, int fd, off_t offset);
```

Maps files, devices, or anonymous memory regions into a process's virtual address space, enabling shared memory regions across independent processes.

---

## Process Execution and Program Replacement

### The `exec()` System Call

The `exec()` family of system calls replaces the current process image with a new program. This replaces the existing code, data, heap, and stack with those of the new executable while retaining the process identity (PID).

Unlike `fork()`, `exec()` does not create a new process. It transforms the existing one.

New programs can be executed through two steps:

1. The parent process calls `fork()` to create a clone child process.
2. The child process calls `exec()` to replace its current program with another executable.

### System Calls

#### `int execl(const char *path, const char *arg, ...);`

This syscall replaces the current process image with a new executable specified by `path`. Additional arguments are passed to the new program, with the argument list terminated by `NULL`.

A successful `exec()` call does not return, as the original process image has been replaced. If the call fails, it returns `-1`.

### Example: Combining `fork()` and `exec()`

```c
pid_t pid = fork();

if (pid == 0) {
    execl("/bin/ls", "ls", "-l", NULL);
    exit(1);
} else if (pid > 0) {
    waitpid(pid, NULL, 0);
}
```

The parent creates a child process using `fork()`. The child then executes the `ls` program using `execl()`, replacing its original process image. Meanwhile, the parent waits for the child to terminate.

---

# Files and File Systems

## File Fundamentals

A file is a data container in the file system, typically stored on a disk, but files are not limited to physical storage devices.

Directories group files together, providing an organisational structure for the file system.

Files and directories are organised in hierarchical trees, starting from a root directory.

### File Descriptors

Each open file is assigned a unique file descriptor within the process.

A file descriptor is a handle used by a process to access an open file or other I/O resource.

File descriptors are represented as non-negative integers and are used by system calls to identify the resource being accessed.

### Example: Reading from a File

```c
int fd = open("example.txt", O_RDONLY);

char buffer[128];
read(fd, buffer, sizeof(buffer));

close(fd);
```

The `open()` system call opens the file and returns a file descriptor. The `read()` system call uses this descriptor to retrieve data, while `close()` releases the resource when it is no longer needed.

---

## File Permissions

Access to files is restricted through file permissions, which determine which users can read, write, or execute a file.

### Permission Structure

File permissions are represented as a bitmap consisting of nine permission bits, divided into three groups:

- **Owner:** Permissions assigned to the file's owner.
- **Group:** Permissions assigned to users belonging to the file's group.
- **Others:** Permissions assigned to all remaining users.

Each group contains three permission bits:

| Permission | Symbol | Octal Value |
|---|---|---|
| Read | `r` | 4 |
| Write | `w` | 2 |
| Execute | `x` | 1 |

The permissions can be inspected using:

```bash
ls -al
```

Example output:

```text
-rwxr-xr-- 1 lasse users 1024 Nov 6 example
```

The permission string `-rwxr-xr--` indicates that the owner has read, write, and execute permissions, the group has read and execute permissions, and others have read permissions.

### System Calls

#### `int chmod(const char *path, mode_t mode);`

This syscall changes the permissions of a file specified by its path.

### Example: Changing File Permissions

```bash
chmod 754 example
```

The octal value `754` represents the following permissions:

- Owner: `7` = read, write, execute.
- Group: `5` = read, execute.
- Others: `4` = read.

---

## Unix File Abstraction

### Everything in UNIX is a File

UNIX-like operating systems expose many different types of resources through a common file interface.

Examples of resources exposed through the file system include:

- **Input and Output:** Keyboard and screen.
- **Storage Devices:** Hard drives and CD-ROMs.
- **Peripherals:** Serial ports and printers.
- **System and Hardware Properties:** Various system and hardware properties, such as CPU temperature.
- **Networking:** Modems and networking interfaces.

These resources are not necessarily regular files. However, they are exposed through the file system and can be accessed using file descriptors.

This leads to the expression:

**"Everything in UNIX is a file descriptor."**

### Unified I/O Interface

Because different resources can be accessed through file descriptors, the same system calls and tools can operate on different types of resources.

For example, the same `read()` system call can retrieve data from an actual file, a serial port, or the keyboard.

### Standard File Descriptors

Every process typically starts with three predefined file descriptors:

| File Descriptor | Name | Purpose |
|---|---|---|
| `0` | STDIN | Standard input |
| `1` | STDOUT | Standard output |
| `2` | STDERR | Standard error |

These descriptors can be redirected to different files or I/O resources.

### Terminal Redirection

Unix shells provide operators for redirecting input and output:

| Operator | Purpose | Example |
|---|---|---|
| `>` | Redirects standard output to a file | `ls > output.txt` |
| `<` | Redirects standard input from a file | `sort < input.txt` |
| `|` | Connects the output of one command to another | `ls \| wc -l` |

Redirection allows programs to exchange data without requiring them to implement their own file handling mechanisms.

---

## Inter-Process Communication (IPC)

### Pipes

A pipe is a unidirectional data channel exposed through two file descriptors. It is used for inter-process communication (IPC), allowing processes to exchange data.

A pipe connects the output of one process to the input of another.

Each pipe consists of two file descriptors:

- **Read end (`pipefd[0]`):** Used to receive data from the pipe.
- **Write end (`pipefd[1]`):** Used to send data into the pipe.

### System Calls

#### `int pipe(int pipefd[2]);`

This syscall creates a pipe and stores its two file descriptors in the provided array.

#### `int dup2(int oldfd, int newfd);`

This syscall duplicates an existing file descriptor, assigning the new descriptor number to `newfd`. If `newfd` is already open, it is closed before the duplication.

### Example: Creating a Pipe

```c
int pipefd[2];

pipe(pipefd);
```

The `pipe()` syscall creates a communication channel between processes. The resulting file descriptors can be used to send and receive data.

### Example: Redirecting Output Through a Pipe

```c
int pipefd[2];
pipe(pipefd);

pid_t pid = fork();

if (pid == 0) {
    close(pipefd[0]);

    dup2(pipefd[1], STDOUT_FILENO);
    close(pipefd[1]);

    execl("/bin/ls", "ls", NULL);
    exit(1);
} else if (pid > 0) {
    close(pipefd[1]);

    char buffer[128];
    int n;

    while ((n = read(pipefd[0], buffer, sizeof(buffer))) > 0) {
        write(STDOUT_FILENO, buffer, n);
    }

    close(pipefd[0]);
    waitpid(pid, NULL, 0);
}
```

The parent creates a pipe before calling `fork()`, allowing both processes to inherit its file descriptors.

The child redirects its standard output to the pipe's write end using `dup2()`. When `exec()` replaces the child process with `ls`, its output is consequently written into the pipe.

The parent reads the resulting data from the pipe's read end and forwards it to its own standard output.

This demonstrates how `fork()`, `exec()`, file descriptors, and pipes work together to enable inter-process communication.