Instruction pipelining is a technique that lets a [[CPU]] work on several instructions at once instead of finishing one completely before starting the next.

## How It Works

Pipelining separates instruction processing into distinct fetch, decode, and execute units. While one instruction is being executed, the next is already being decoded, and the one after that is already being fetched. Each stage works on a different instruction simultaneously, so the stages overlap like a factory assembly line rather than running strictly one after another.

This is a form of instruction-level parallelism that does not require extra cores: it comes purely from overlapping the internal stages of instruction processing on a single execution pipeline.

## Related Concepts

A **[[Superscalar Processor]]** takes this idea further by adding specialized execution units, so that genuinely different kinds of work, not just different stages of the same kind of work, can happen in parallel within a single core.
