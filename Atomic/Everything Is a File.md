UNIX-like operating systems expose many different types of resources through a common file interface, not just data stored on disk.

## How It Works

Examples of resources exposed through the file system include:

- **Input and output**: keyboard and screen.
- **Storage devices**: hard drives and CD-ROMs.
- **Peripherals**: serial ports and printers.
- **System and hardware properties**: various system and hardware properties, such as CPU temperature.
- **Networking**: modems and networking interfaces.

These resources are not necessarily regular files, see [[File]]. However, they are exposed through the file system and can be accessed using [[File Descriptor|file descriptors]]. This leads to the expression: **"Everything in UNIX is a file descriptor."**

### Unified I/O Interface

Because different resources can be accessed through file descriptors, the same system calls and tools can operate on different types of resources. For example, the same `read()` system call can retrieve data from an actual file, a serial port, or the keyboard, the same underlying controllers discussed in [[Input and Output Devices]].
