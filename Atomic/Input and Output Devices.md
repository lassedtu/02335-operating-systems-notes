I/O devices are the category of [[Computer Hardware]] through which a computer interacts with the world: disks, CD/DVD drives, printers, keyboards, mice, displays, and network interfaces.

## How It Works

I/O devices generally come with a **controller**: a small computer chip that physically operates the device on the computer's behalf. Controllers typically have their own processor (often not programmable by the end user), their own registers, and sometimes their own memory, and they accept commands issued by the operating system rather than being driven directly by the main CPU.

The operating system talks to a controller through a **[[Device Driver]]**, a piece of OS software written specifically for that controller. Controllers expose their memory and registers to the rest of the system through **[[Memory-Mapped IO]]**.

### Communicating With a Device

Beyond mapping a controller's registers into the address space, actual communication with a device can happen in one of several ways, described in [[Device Communication Methods]]: busy waiting, interrupt-based notification, or Direct Memory Access.

## Related Concepts

On Unix-like systems, I/O devices are themselves exposed through the file system, following the philosophy that [[Everything Is a File]].
