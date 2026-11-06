Direct Memory Access (DMA) is a dedicated chip that can move data directly between a device controller and main memory without the main CPU being involved in the transfer at all, freeing the CPU up completely for the duration of the transfer. It is the most sophisticated of the three [[Device Communication Methods]].

## How It Works

Where busy waiting wastes CPU cycles polling, and an **[[Interrupt]]** at least lets the CPU do other work while waiting, both still require the CPU itself to move the actual data once it is ready. DMA removes even that step: the DMA chip handles the transfer end to end, and typically raises an interrupt only once the entire transfer is complete, rather than for every individual unit of data.

## Related Concepts

DMA is especially valuable for high-throughput devices like disks and network interfaces, where having the CPU copy every byte itself would waste a large fraction of its time that could otherwise go to running other processes, see [[Process]].
