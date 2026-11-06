A bus is simply a communication line connecting parts of the computer together, the physical infrastructure underneath every interaction described in [[Computer Hardware]].

## How It Works

Buses vary along two independent dimensions:

- **By width of transfer**: **serial** buses move one bit at a time, while **parallel** buses move a whole word (for example, 32 bits) at once.
- **By sharing**: a **dedicated** bus is allocated exclusively to two specific components, while a **shared** bus is used by multiple devices in turn.

## Examples

### A Real x86 System

A real x86 system's block diagram shows how these pieces actually connect: two [[CPU]] cores, each with their own cache, sit behind a shared cache and connect (via PCIe) to a graphics chip and (via memory controllers) to DDR3 main memory. Below that, a DMI link connects to a Platform Controller Hub, which fans out to PCI slots, SATA (for disks), USB 2.0 and 3.0 ports, Gigabit Ethernet, and further PCIe devices. Every box in this diagram maps directly onto a concept already introduced elsewhere: cores, [[Cache Memory|caches]], memory controllers, and I/O controllers (SATA, USB, Ethernet) all connecting through a hierarchy of buses.

### A Real Sensor System

The same underlying structure, processor, memory, and I/O, shows up at a radically smaller scale in an embedded sensor. The SPHERE wearable sensor, built around a CC2650 System-on-Chip and an ADXL362 accelerometer, packs an ARM Cortex-M3 main CPU, flash, SRAM, and ROM alongside a dedicated ARM Cortex-M0 sensor controller and a full RF core for wireless communication, all fitting on a board small enough to sit inside a wristband. It is the same computer organization principles, just compressed dramatically.
