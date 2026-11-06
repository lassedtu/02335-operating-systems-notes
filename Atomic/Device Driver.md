A device driver is a piece of operating system software written specifically to talk to one particular kind of device controller, part of the [[Input and Output Devices]] subsystem.

## How It Works

The operating system never drives hardware blindly, it goes through the driver written for that specific controller. How a driver actually gets into the running kernel has evolved over time:

- In the old days, adding a driver meant **relinking the entire kernel** from source.
- Later, the OS gained the ability to **load drivers automatically at boot time**.
- More recently, drivers are **loaded on the fly as devices are plugged in**, commonly called **plug and play**.

## Related Concepts

Where a driver actually runs, inside the kernel or as a user-mode service, is one of the central design questions behind [[Operating System Structure]]: a buggy driver inside a [[Monolithic Kernel]] can crash the whole system, while a buggy driver running as a [[Microkernel]] service cannot.
