An [[Operating System]] manages and abstracts resources, and understanding what it is actually managing means first understanding what the hardware itself looks like.

## How It Works

A modern computer system is built from a recognizable set of parts: one or more processors, main memory, disks, CD/DVD drives, printers, a keyboard, a mouse, a display, network interfaces, and a whole category of other I/O devices.

- The **[[CPU]]** fetches and executes instructions, using on-chip [[CPU|registers]] for fast temporary storage.
- **[[Memory Hierarchy|Memory]]** stores the data and instructions a running program needs, organized in fast-to-slow layers because no single technology is simultaneously fast, large, and cheap.
- **[[Input and Output Devices]]** let the computer interact with disks, networks, displays, and peripherals, each managed through a **[[Device Driver]]**.
- A **[[Bus]]** is the communication line that physically connects all of these parts together.

## Examples

### A Real x86 System

A real x86 system's block diagram shows how these pieces actually connect: two CPU cores, each with their own cache, sit behind a shared cache and connect (via PCIe) to a graphics chip and (via memory controllers) to DDR3 main memory. Below that, a DMI link connects to a Platform Controller Hub, which fans out to PCI slots, SATA (for disks), USB 2.0 and 3.0 ports, Gigabit Ethernet, and further PCIe devices. See [[Bus]] for how this hierarchy of buses ties the pieces together.

### A Real Embedded Sensor System

The same underlying structure, processor, memory, and I/O, shows up at a radically smaller scale in an embedded sensor. The SPHERE wearable sensor, built around a CC2650 System-on-Chip and an ADXL362 accelerometer, packs an ARM Cortex-M3 main CPU, flash, SRAM, and ROM alongside a dedicated ARM Cortex-M0 sensor controller and a full RF core for wireless communication, all fitting on a board small enough to sit inside a wristband. It applies the same computer organization principles as a desktop PC, just compressed dramatically. Some devices at this scale skip the operating system entirely and run [[Bare Metal]].
