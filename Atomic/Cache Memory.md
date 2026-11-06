Cache memory is the small, fast layer of the [[Memory Hierarchy]] sitting closest to the [[CPU]]. It only helps performance if the system's guesses about what to keep there are good, and those guesses rely on the **[[Principle of Locality]]**.

## How It Works

Locality is not just a hardware detail, it directly shapes how fast your own code runs. For temporal locality, make sure any reuse of the same data happens shortly after its prior use. For spatial locality, cluster reused data together, and cluster together data that tends to be accessed shortly after each other.

### Real Hardware: Quad-Core Cache Architectures

Real multicore chips organize their cache hierarchy in different ways. One layout has four cores connected to each other and to a shared cache over a common internal bus. Another gives each core its own private L2 cache, with an L1 cache sitting even closer to each individual core. On Linux, you can inspect your own machine's actual cache structure directly with `lscpu`, or with `getconf -a | grep -i cache`. See [[Multicore Processor]] for more on how cores relate to each other.

## Examples

Consider a simple example: summing every element of a large two-dimensional array.

```c
int a[1000][1000];
int c = 0;

for (i=0; i<1000; i++)
    for (j=0; j<1000; j++)
        c += a[i][j];
```

versus the same loop with the indices swapped:

```c
int a[1000][1000];
int c = 0;

for (i=0; i<1000; i++)
    for (j=0; j<1000; j++)
        c += a[j][i];
```

These two loops touch exactly the same set of memory addresses and compute exactly the same result, but they access memory in a completely different order. A 2D array is laid out in memory row by row, so `a[i][j]` walks through memory sequentially as `j` increases, exhibiting strong spatial locality: each access is right next to the previous one, so it is very likely to already be sitting in cache. The swapped version, `a[j][i]`, jumps a full row's width in memory on every single access, which tends to miss the cache far more often. In practice, this version can run dramatically slower, even though the arithmetic is identical.

The general lesson: caches depend on locality to work, so code has to actually exhibit locality to benefit from them.
