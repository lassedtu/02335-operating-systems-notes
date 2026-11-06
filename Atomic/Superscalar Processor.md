A superscalar CPU extends [[Instruction Pipelining]] by adding specialized execution units, for example a dedicated floating-point unit, so that genuinely different kinds of work can happen in parallel within a single core.

## How It Works

Where a pipelined CPU overlaps the fetch, decode, and execute stages of a single stream of instructions, a superscalar CPU can dispatch multiple instructions to different specialized units at the same time, as long as those instructions do not depend on each other's results. An integer addition and a floating-point division, for instance, can genuinely execute simultaneously on their own dedicated units rather than waiting in a single shared pipeline.

## Related Concepts

Superscalar execution is still happening within one core. For true parallel execution across separate cores, see [[Multicore Processor]]. For a single core switching rapidly between multiple threads rather than executing them with dedicated hardware units, see [[Multithreading]].
