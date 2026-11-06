Multiple processors (commonly 4, 8, 16, or more cores) on a single chip provide genuinely true parallelism, rather than the pseudo-parallelism of [[Multithreading]], since separate cores really are doing separate work at the same instant.

## How It Works

Each core is a largely independent execution unit, capable of its own [[Instruction Pipelining]] and potentially its own [[Superscalar Processor|superscalar]] execution units, fetching and executing its own stream of instructions. Real multicore chips organize their cache hierarchy in different ways: one layout has all cores connected to each other and to a shared cache over a common internal bus; another gives each core its own private L2 cache, with an L1 cache sitting even closer to each individual core. See [[Cache Memory]] for more on how these hierarchies behave.

### GPUs

A Graphics Processing Unit (GPU) pushes the multicore idea to an extreme, offering a very large number of simpler cores optimized for the kind of massively parallel work graphics (and, increasingly, machine learning) require.

## Examples

On Linux, you can inspect your own machine's actual cache and core structure directly with:

```bash
lscpu
```

or:

```bash
getconf -a | grep -i cache
```
