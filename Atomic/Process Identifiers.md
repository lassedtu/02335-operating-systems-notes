Every [[Process]] is assigned a unique Process ID (PID) by the kernel, used for access control, security, and bookkeeping in the system-wide process table.

## How It Works

A process can also look up its own PID, and the PID of its parent (PPID), through dedicated system calls:

```c
pid_t getpid(void);
```

Returns the unique Process ID of the calling process.

```c
pid_t getppid(void);
```

Returns the Process ID of the parent process.

Parent/child relationships created through the **[[Fork System Call]]** are what give every process a PPID in the first place: when a process calls `fork()`, the new child's PPID is the PID of the process that called `fork()`.

## Examples

The relationship between PID and PPID is visible directly in the output of:

```bash
ps -ef
```

which lists the UID, PID, parent PID (PPID), start time, terminal, and command for every process, and in:

```bash
pstree
```

which renders the parent/child relationships as an actual tree, rooted at the `init` process.
