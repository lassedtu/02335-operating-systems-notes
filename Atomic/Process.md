Operating systems manage active tasks through the concept of a process, which represents a program in execution.

## How It Works

Each process maintains its own allocated memory space, [[CPU|CPU registers]], open file descriptors (see [[File Descriptor]]), and associated system resources. Because these memory regions are independent, processes cannot directly exchange data through standard global variables or heap allocations, though they can get around this with [[Shared Memory]].

Modern operating systems support concurrent execution, allowing multiple processes to run in parallel on a [[Multicore Processor]] or via pseudo-parallelism (rapid context switching) on single-core systems, conceptually similar to how [[Multithreading]] lets a single core juggle multiple threads.

The kernel maintains a system-wide data structure known as the **process table** to track all active, suspended, and terminated (zombie) processes. See [[Process Termination]] for what happens to a process's entry when it exits. Every process is assigned a unique **[[Process Identifiers|Process ID (PID)]]** and an associated user owner for access control and security.

New processes are created with the **[[Fork System Call]]**, and can replace their own program image using the **[[Exec System Call]]**.

## Examples

To inspect the currently running processes on a Unix-like operating system, administrators and users query the process table using utilities such as:

```bash
ps -ef
```

This command generates a full-format listing of all active processes currently executing on the system, displaying details such as the UID, PID, parent PID (PPID), start time, terminal, and the command arguments associated with each execution thread.
