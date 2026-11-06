An operating system provides a large number of services, and a fundamental design question follows directly from the [[User Mode]]/[[Kernel Mode]] split: which of those services should actually run in kernel mode, and which in user mode?

## How It Works

This is fundamentally a **stability versus efficiency trade-off**: kernel mode is fast but dangerous (a bug there can take the whole system down), user mode is safer but slower (every reach into a kernel-mode resource costs an expensive mode transition, via a [[System Call]]). Different operating system architectures answer this question differently:

- A **[[Monolithic Kernel]]** runs the entire OS as a single program in kernel mode.
- A **[[Layered Operating System]]** organizes the OS as a hierarchy of layers of increasing privilege.
- A **[[Microkernel]]** keeps the kernel itself tiny and pushes almost everything else into user mode.
- A **[[Hybrid Kernel]]** blends ideas from the monolithic and microkernel approaches.

## Related Concepts

Real-world kernel designs rarely sit at a pure extreme, and the trade-offs here echo a famous public disagreement between Andrew Tanenbaum and Linus Torvalds about exactly this question, covered in [[Monolithic Kernel]].
