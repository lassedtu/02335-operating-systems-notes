Memory-mapped I/O is the mechanism by which device controllers expose their memory and registers to the rest of the system: their memory-mapped registers get mapped directly into the system's address space, so the CPU can read or write them exactly like any other memory address, with no special instructions required.

## How It Works

Instead of needing dedicated instructions just to talk to hardware, the operating system (or a [[Device Driver]]) can read and write a device's control registers using the same load and store instructions it would use for ordinary memory. This is the foundation that makes the communication methods in [[Device Communication Methods]] possible: busy waiting, interrupts, and DMA all ultimately rely on being able to address a controller's registers as if they were memory.

## Related Concepts

This abstraction is part of how the [[Operating System]] turns the genuinely messy hardware interface, countless different controllers with different register layouts, into something uniform that software can reason about.
