Kernel mode is an unrestricted execution state where the processor has complete access to all hardware resources and system instructions. The [[Operating System]] itself typically runs here.

## How It Works

CPUs support (at least) two operating modes, and the difference between them is central to how an operating system protects itself and its users. In kernel mode, the CPU can execute every instruction and use every piece of hardware. This is the opposite of **[[User Mode]]**, where the set of allowed instructions and accessible hardware resources is deliberately limited.

A program running in user mode cannot simply jump into kernel mode on its own. It has to make a **[[System Call]]**: normal execution is suspended, and the operating system takes control through what is called a **trap**.

```mermaid
flowchart LR
    UM["User mode\n(limited instructions\nand resources)"] -->|"System call (trap)"| KM["Kernel mode\n(all instructions\nand resources)"]
    KM -->|Return| UM
```

## Related Concepts

Whether a given OS service, like a [[Device Driver]] or a file system, runs in kernel mode or user mode is exactly the question that distinguishes the different approaches to [[Operating System Structure]]: a [[Monolithic Kernel]] runs almost everything in kernel mode, while a [[Microkernel]] pushes nearly everything else out into user mode.
