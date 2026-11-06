A [[Process]] ends its execution by calling the `exit()` system call, which terminates the calling process and reports an exit status code to the operating system.

## How It Works

```c
void exit(int status);
```

The parent process can retrieve this status by waiting on the child, for example through `waitpid()`, as seen in the combined [[Fork System Call]] and [[Exec System Call]] examples elsewhere in this knowledge base.

A process that has exited but whose exit status has not yet been collected by its parent remains in the kernel's process table as a **zombie process**: its entry is kept around specifically so the parent can retrieve the exit status later. This is why the process table is described as tracking active, suspended, *and* terminated (zombie) processes, not just running ones.
