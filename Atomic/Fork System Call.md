In Unix-like operating systems, a [[Process]] can clone itself using the `fork()` system call. The process that initiates the clone is designated as the **parent process**, and the newly created duplicate is the **child process**.

## How It Works

The child process is allocated a distinct address space containing an exact duplicate of the parent process's memory contents at the time of the call. Because these address spaces are separate from the moment of creation, the parent and child cannot exchange data through ordinary variables, see [[Shared Memory]] for how processes get around this.

`fork()` is the fundamental mechanism for process creation in Unix-like systems. Consequently, all active processes originate from a root ancestor (traditionally the `init` process). Process trees can be inspected using:

```bash
pstree
```

### Return Values

Because the child process is an exact copy of the parent, both resume execution at the instruction immediately following the `fork()` call. To allow the program to distinguish between the two execution paths, the system call returns different values:

- **To the parent process**: it returns the [[Process Identifiers|Process ID (PID)]] of the newly created child.
- **To the child process**: it returns `0`.

## Examples

```c
pid_t fork(void);
```

This syscall clones the calling process, generating a new child process.

Combined with [[Exec System Call|exec()]], `fork()` is the standard two-step way to launch a brand new program:

```c
pid_t pid = fork();

if (pid == 0) {
    execl("/bin/ls", "ls", "-l", NULL);
    exit(1);
} else if (pid > 0) {
    waitpid(pid, NULL, 0);
}
```

The parent creates a child process using `fork()`. The child then executes the `ls` program using `execl()`, replacing its original process image. Meanwhile, the parent waits for the child to terminate, see [[Process Termination]].
