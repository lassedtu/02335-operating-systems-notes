Once a controller's registers are reachable through [[Memory-Mapped IO]], the operating system still has to decide how to actually wait for, and react to, the results of a command it issues to a device. There are three approaches, in increasing order of sophistication.

## How It Works

- **Busy waiting**: send a command, then sit in a loop repeatedly checking whether it is done yet. Simple, but wastes CPU cycles the whole time the device is working.
- **Interrupt-based**: send a command and let the CPU go to sleep (or do other work); the controller itself generates an **[[Interrupt]]** once it is finished, actively signalling completion rather than making the CPU poll for it.
- **Direct Memory Access ([[Direct Memory Access|DMA]])**: a dedicated chip moves data directly between a controller and main memory without the main CPU being involved in the transfer at all, freeing the CPU up completely for the duration of the transfer.

## Related Concepts

Interrupt-based communication is covered step by step in [[Interrupt]]. The most hands-off method, which offloads the data transfer itself rather than just the waiting, is [[Direct Memory Access]].
