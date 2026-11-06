A pipe is a unidirectional data channel exposed through two [[File Descriptor|file descriptors]]. It is used for inter-process communication (IPC), allowing [[Process|processes]] to exchange data, and is the underlying mechanism behind the shell's `|` operator, see [[Shell Redirection]].

## How It Works

A pipe connects the output of one process to the input of another. Each pipe consists of two file descriptors:

- **Read end** (`pipefd[0]`): used to receive data from the pipe.
- **Write end** (`pipefd[1]`): used to send data into the pipe.

```c
int pipe(int pipefd[2]);
```

This syscall creates a pipe and stores its two file descriptors in the provided array.

```c
int dup2(int oldfd, int newfd);
```

This syscall duplicates an existing file descriptor, assigning the new descriptor number to `newfd`. If `newfd` is already open, it is closed before the duplication. This is how a process redirects one of its [[Standard File Descriptors]], for example its STDOUT, into the write end of a pipe.

## Examples

```c
int pipefd[2];

pipe(pipefd);
```

The `pipe()` syscall creates a communication channel between processes. The resulting file descriptors can be used to send and receive data.

### Redirecting Output Through a Pipe

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

The parent creates a pipe before calling [[Fork System Call|fork()]], allowing both processes to inherit its file descriptors.

The child redirects its standard output to the pipe's write end using `dup2()`. When [[Exec System Call|exec()]] replaces the child process with `ls`, its output is consequently written into the pipe.

The parent reads the resulting data from the pipe's read end and forwards it to its own standard output. This demonstrates how `fork()`, `exec()`, file descriptors, and pipes work together to enable inter-process communication.
