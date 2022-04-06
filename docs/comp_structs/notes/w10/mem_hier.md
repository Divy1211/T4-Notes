## S-RAM Cell

6T-SRAM Cell (6 transistor)

SRAM is volatile because the NOT gates need powering to maintain their state (remember the CMOS tech, VDD is needed to make these gates work)

![SRAM](https://dropbox.com/s/u1acx3abx3102pn/read_sram.png?raw=1)

The word line is the read/write enable.

The complementary bit lines are connected to a single sense amplifier. The job of this sense amp is to calc the difference of the voltages on the two lines. If it is positive, then the sense amp outputs a valid logic `1` else a valid logic `0`.

This is what happens when the data needs to be read, word line is set high, the sense amps detect and output accordingly.

When writing, the word line is set high and a strong voltage needs to be supplied through the bit line and its complement (to get the loop to flip states if necessary)

## DRAM

2 compoenents

DRAM is volatile because it needs powering/refreshing to maintain its state

![DRAM](https://dropbox.com/s/4wovmxsgb7896vd/dram.png?raw=1)

To read, we set the word line high and read the voltge of the capacitor on the bit line

To write, we set the word line high and supply a strong `1` or `0` to charge or discharge the capacitor.

DRAM looses charge  (data) overtime.

DRAM cells need to be refreshed (refresh rate!) to keep the data intact

significantly slower than SRAM but cheaper

A D-Latch uses a mux - 4 nand gates - 16T.

A DFF uses 2 muxes - 32T + 2T for inverter

## Hard Disk

![HDD](https://dropbox.com/s/x32k130rfu8h7fm/disk.png?raw=1)

## Memory Addressing

![mad](https://dropbox.com/s/kc5atqtnyuo5dg7/decoding.png?raw=1)

## Memory Hierarchy

![mh](https://dropbox.com/s/9v2wj0zf64zbclo/memhierarchy.png?raw=1)

## Locality of Reference

It is possible to give the user an illusion that they’re running at SRAM speed at all times due to the locality of reference.

The locality of reference states that reference to memory location $X$ at time $t$ implies that reference to $X+\Delta X$ $t + \Delta t$ becomes more probable as $\Delta X$, $\Delta t$ approach zero

In laymen terms: there exists the tendency of a CPU to access the same set of memory locations repetitively over a short period of time.

Evidence that memory reference patterns exhibit locality of reference:

Local stack frame grows nearby to one another
Related program instructions are near one another
Data (e.g: arrays) are also nearby one another (why python lists are slow)

## Average LD/ST Times

$t_ave = \alpha t_c + (1-\alpha)(t_c + t_m) = t_c + (1-\alpha)t_m$. t_c is always there, but $1-\alpha$ times we also have $t_m$

$\alpha$ - cache hit ratio

Most modern CPUs have at least three independent caches: an instruction cache to speed up executable instruction fetch, a data cache to speed up data fetch and store, and a Translation Lookaside Buffer (TLB) used to speed up virtual-to-physical address translation for both (executable) instructions and data. Data cache is usually organized as a hierarchy of more cache levels (L1, L2, L3, L4, etc.).

## FA Cache

![FA](https://dropbox.com/s/yoj1kl3kg3do86c/facache.png?raw=1)

1. Expensive
   1. Needs 64 bis (32 bits address, 32 bits data) to store each memory address
   2. Bitwise compare at each cache line
   3. Tri state buffer at each row
   4. Large `OR` gate to compute `HIT`
2. Very Fast because of parallel lookup when given an address
3. Flexible because any mem can go to any cache line

## DM Cache

![DM](https://dropbox.com/s/eu74l2gi23380mp/dmcache.png?raw=1)

1. Cheaper:
   1. Less SRAM is used as the `TAG` only contains the `T` upper bits of the address A
   2. Only one bitwise compare needed for `2^(32-T)` addresses
   3. A demux and `32-T` selector bits are needed
2. Not as flexible as FA Cache because `2^(32-T)` addresses are stored consecutively
3. Contention Problem (2 different addresses with same lower `32-T` bits map to same cache line)
4. Slower since no parallel searching