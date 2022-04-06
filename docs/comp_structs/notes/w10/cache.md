## Design Issues

The cache design issues are categorised as follows:

1. Associativity : we need to determine how many different cache lines can one address be stored to. It implies choice . Of course note that there can only be one copy of that address (tag) in the entire cache.
   1. For DM cache, there is no choice on which cache line is used or looked up. A 1-to-1 mapping between each combination of the last kk bit of the query address A to the cache line (entry) is required. Hence, the DM cache has no associativity.
   2. An FA cache, as the name suggests: has complete associativity. We have N choices of cache lines in an FA cache of size N: any Tag-Content can reside on any cache line in FA cache.
2. Replacement policy : refers to the decision on which entry of the cache should we replace in the event of cache MISS.
3. Block size : refers to the problem on deciding how many sets of 32-bits data do we want to write to the cache at a time.
4. Write policy : refers to the decision on when do we write (updated entries) from cache to the main memory.

## N-Way Set Associative Cache

![NWSAC](https://dropbox.com/s/jbg0b7ajjcn79mg/nway.png?raw=1)

1. An NWSA cache is made up of N DM caches, connected in a parallel fashion.
2. The cells in the same row marked in red is called as belonging in the same **set**.
3. The cells in the same column of DM caches is said to belong in the same **way**. Each way is basically a DM cache that has $2^k$ cache lines.
4. Given a combination of K-bit lower address, the higher T-bit TAG and its Content can be stored in any of the N cache lines in the same set.
5. Given a query address `A`:
   1. we will need to wait for the device to decode its last K bits and find the right set.
   2. Then, the device will perform a parallel lookup operation for all N cache lines.

## Replacement Policies

### Least Recently Used (LRU)

1. An ordered list of $N \log N$ bits needs to be maintained for N cache lines
2. LRU Hardware implementation

### Least Recently Replaced (LRR)

1. One pointer of $\log N$ bits to maintain which cache line was replaced the oldest and should hence be replaced. +1 after replace
2. Not as complex LRR algo

### Random

1. PRNG

## Cache Block Size

We can increase capacity if we cache multiple words instead of just one.

![CBS](https://dropbox.com/s/ceamhyfon0dsofw/blocksize.png?raw=1)

Tag is 28 bits, word offset is 2 bits and byte offset is 2 bits (`00` for beta always)

If high locality of ref, there is a good chance that words from the same block will be required, and when we access them later on, it will be fast.

Risk of fetching unused words. Bad with low locality of ref

## Write Policies

Decide when to write modified cache stuff back to MEM

### Write Through

Always immediately write to the MEM after writing to cache

### Write Back

Use dirty bit and only write to MEM when terminates or a dirty line is replaced

### Write Behind

Write immediately but buffered/pipelined

## Helper Bits

### Valid

Indicates if cache line has a valid entry

### Dirty

Indicates when a cache line is more recent than MEM and needs to be written back

### LRU bits

not in DM cache

## Word Addressing Convention For Beta & PSETs

