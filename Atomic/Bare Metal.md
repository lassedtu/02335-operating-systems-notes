Bare metal (or "bare machine") programming means software talks directly to the computer hardware with no [[Operating System]] layer in between at all.

## How It Works

There is no [[Kernel Mode]] or [[User Mode]] split, no process abstraction, and no services like a file system or device drivers provided by an underlying OS. The program itself is responsible for everything a kernel would normally handle: initializing hardware, talking to device registers directly, and managing its own control flow.

This is unusual for general-purpose computing, where an operating system's abstractions are worth their overhead. It shows up mainly in some of the smallest embedded devices, where the overhead of a full OS isn't justified, for example extremely constrained [[Internet of Things]] sensors running no software stack beyond the application itself.

## Examples

A battery-powered sensor the size of a coin may run its firmware directly against the hardware rather than loading an OS like Contiki OS or RIOT, trading away OS conveniences (scheduling, memory protection, file systems) in exchange for minimal code size and power draw.
