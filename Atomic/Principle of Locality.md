The principle of locality is the observation that a program accesses a relatively small portion of its address space at any given instant. It is the reason a [[Memory Hierarchy]] works at all: it lets a system make a good guess about which data to keep in fast [[Cache Memory]] without having to know the future.

## How It Works

The principle splits into two distinct types:

- **Temporal locality** (locality in time): if an item is referenced once, it will tend to be referenced again soon.
- **Spatial locality** (locality in space): if an item is referenced, items whose addresses are close to it tend to be referenced soon as well.

## Related Concepts

[[Cache Memory]] shows how violating or respecting these two principles in your own code can make a dramatic, measurable difference in performance.
