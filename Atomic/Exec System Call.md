The `exec()` family of system calls replaces the current [[Process]] image with a new program. This replaces the existing code, data, heap, and stack with those of the new executable while retaining the process identity ([[Process Identifiers|PID]]).

## How It Works

Unlike **[[Fork System Call|fork()]]**, `exec()` does not create a new process. It transforms the existing one. A successful `exec()` call does not return, as the original process image has been replaced. If the call fails, it returns `-1`.

New programs are typically launched through two steps:

1. The parent process calls `fork()` to create a clone child process.
2. The child process calls `exec()` to replace its current program with another executable.

## Examples

```c
int execl(const char *path, const char *arg, ...);
```

This syscall replaces the current process image with a new executable specified by `path`. Additional arguments are passed to the new program, with the argument list terminated by `NULL`.

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
