The Internet of Things (IoT) refers to the broad category of small, often battery-powered, networked embedded devices, sensors, wearables, and similar hardware, that extend computing and connectivity down to a scale far smaller than a desktop or server.

## How It Works

IoT devices still need software to manage their hardware, but the constraints are extreme compared to a desktop: limited power, limited memory, and limited processing capability. Some run specialized, lightweight **[[Operating System|operating systems]]** built for exactly this environment, such as Contiki OS, RIOT, OpenWSN, and TinyOS. Others skip an operating system entirely and run **[[Bare Metal]]**, where the overhead of a full OS is not justified given how constrained the device is.

## Examples

The SPHERE wearable sensor, described in [[Computer Hardware]] and [[Bus]], is a concrete example: it packs an ARM Cortex-M3 main CPU, flash, SRAM, ROM, a dedicated ARM Cortex-M0 sensor controller, and a full RF core for wireless communication onto a board small enough to sit inside a wristband, the same computer organization principles as a desktop PC, just compressed dramatically.
