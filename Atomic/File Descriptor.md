A file descriptor is a handle used by a [[Process]] to access an open [[File]] or other I/O resource. Each open file is assigned a unique file descriptor within the process.

## How It Works

File descriptors are represented as non-negative integers and are used by [[System Call]]s to identify the resource being accessed. Every process typically starts with three predefined file descriptors, see [[Standard File Descriptors]].

Because many different kinds of resources, not just regular files, are represented this way, the same system calls can operate on very different underlying resources, see [[Everything Is a File]].

## Examples

```c
int fd = open("example.txt", O_RDONLY);

char buffer[128];
read(fd, buffer, sizeof(buffer));

close(fd);
```

The `open()` system call opens the file and returns a file descriptor. The `read()` system call uses this descriptor to retrieve data, while `close()` releases the resource when it is no longer needed.
