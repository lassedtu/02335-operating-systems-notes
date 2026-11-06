The CPU (processor) is, informally, the brain of the computer, one of the core components of [[Computer Hardware]]. Concretely, what it does is fetch instructions from memory and execute them.

## How It Works

CPU instructions fall into three broad categories:

- **Data handling instructions**: read, write.
- **Arithmetic and logic instructions**: add, divide, compare.
- **Control flow instructions**: jump, call.

To do this, the CPU relies on **registers**, small pieces of extremely fast on-chip storage.

- **General purpose registers** hold things like key variables and temporary results.
- **Special registers** serve dedicated roles: the **program counter** tracks which instruction comes next, and the **stack pointer** tracks the top of the current call stack.

### Parallelism Inside the CPU

Modern CPUs do not simply execute one instruction fully before starting the next, nor do they rely on a single core. Three distinct techniques give a CPU parallelism at different levels:

- **[[Instruction Pipelining]]** overlaps the fetch, decode, and execute stages of consecutive instructions on a single execution unit.
- A **[[Superscalar Processor]]** adds multiple specialized execution units so genuinely different kinds of work can happen at the same time within a single core.
- **[[Multithreading]]** lets a single core hold the state of several threads and switch between them rapidly.
- A **[[Multicore Processor]]** provides several complete cores, giving true simultaneous execution rather than the pseudo-parallelism of multithreading.

## Related Concepts

The CPU's behavior is split into two privilege levels, [[Kernel Mode]] and [[User Mode]], which determine which instructions and hardware resources a running program is allowed to use directly.
