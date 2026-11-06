A system call is the mechanism a program uses to transition safely from [[User Mode]] into [[Kernel Mode]], requesting privileged services or hardware interaction from the operating system kernel. Normal execution is suspended and the operating system takes control through what is called a **trap**.

## How It Works

Because applications in user mode cannot directly execute privileged instructions or touch arbitrary hardware, any time a program needs something only the kernel can provide, reading a file, creating a [[Process]], allocating memory, it has to go through a system call rather than doing it directly. System calls return specific status codes to indicate execution success or error conditions.

## Examples

Reading from a file descriptor:

```c
read(fd, buffer, nbytes);
```

Other examples covered elsewhere in this knowledge base include [[Fork System Call|fork()]], [[Exec System Call|exec()]], and the file-related calls in [[File Descriptor]].

## Related Concepts

**[[POSIX]]** standardizes many system calls so that source code using them stays portable across different Unix-like operating systems.
