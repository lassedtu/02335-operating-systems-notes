Following a [[Fork System Call|fork()]] operation, the parent and child [[Process|processes]] execute in isolated address spaces. Because these memory regions are independent, processes cannot directly exchange data through standard global variables or heap allocations.

## How It Works

To bypass this isolation and enable efficient inter-process communication (IPC), processes can request a designated memory region from the operating system kernel that is mapped concurrently into multiple address spaces.

```c
void *mmap(void *addr, size_t len, int prot, int flags, int fd, off_t offset);
```

`mmap()` maps files, devices, or anonymous memory regions into a process's virtual address space, enabling shared memory regions across independent processes.

## Related Concepts

Shared memory is one way for related processes to communicate; **[[Pipe|pipes]]** are another, better suited to streaming a sequence of bytes from one process to another rather than sharing an entire region of memory.
