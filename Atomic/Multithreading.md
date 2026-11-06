Multithreading gives a single [[CPU]] core the ability to hold the state of two (or more) execution threads at once and switch between them extremely fast, in a kind of pseudo-parallel execution.

## How It Works

Because the core keeps the full state of each thread ready, it can switch from one thread to another without the heavier cost of a full context switch between unrelated processes. This is especially useful when one thread stalls waiting on something slow, like fetching data from memory, since the CPU can switch to the other thread rather than sitting idle during the wait.

Multithreading is pseudo-parallel: at the hardware level, a single core is still only genuinely doing one thing at a time, it is just very good at hiding the stalls of one thread by filling them with work from another. This is distinct from a [[Multicore Processor]], where separate cores really are doing separate work at the same instant.

## Related Concepts

At the [[Process]] level, an operating system achieves a similar pseudo-parallel effect through rapid context switching between processes on a single core.
