## Memory Paging

A page is a fixed size block of data that is comprised of contiguous physical memory addresses

![page](https://dropbox.com/s/janbxcdijndlhc4/page.png?raw=1)

It is efficient to transfer data in pages because of the locality of reference

Data in pages can be addressed by two things:

1. A physical page number `PPN`: Indentifies the page
2. A page offset `PO`: Indentifies the word line in the page itself

## Virtual Memory

Each process in a computer does not know of the existence of other processes. A program doesn't keept track of which memory addresses are free/not free to use - this book keeping is instead done by the OS

The OS hence provides a layer of abstraction where it is the only program that needs to be designed to perform good memory management. The rest of the processes in the computer can proceed as if they are the only process running on the computer, i.e. each process believes that it has its own **virtual memory** space.

## Virtual Address

When we start a program, the OS Kernel allocates a dedicated virtual address space for all the instructions of the program. Two programs can even use the same virtual address because they are mapped to different physical addresses. Thus, the addresses requested by the PC are actually virtual addresses instead of physical addresses

All pointers in a program are virtual addresses - on the software level PAs are never exposed to the developers

A Mememory Management Unit (`MMU`) is a piece of hardware that does this VA -> PA mapping

![VA](https://dropbox.com/s/1h5q5heph7vp3yy/detailVM.png?raw=1)

The contents of the virtual memory can either be in the RAM or the Disk swap space or both.

A process itself is unaware of where its data is stored and if it is contiguous or even on the same hardware or not!

Note: anything that is on the disk does not have a PA. To access something from the disk, it is first loaded into the RAM so it can have a VA->PA mapping

The region of the disk space that is used as an extension of the RAM is called the **disk swap space**

## Pagetable

The OS maintains a pagemap that keeps track of all the VA->PA mappings for each program

A pagemap contains all possible VAs for a program but not all VAs have a corresponding PA (if its in the swap space)

![PT](https://dropbox.com/s/rek05rsjagk2m43/mmuusage.png?raw=1)

The pagetable stores a mapping of the higher $v$ bits of the VAs (the VPN) to corresponding PPN

The lower bits of the VA and the PA are the PO and they are the same.

`D` - Dirty

`R` - Resident data associated with VA is contained in the RAM or not. If not, a page fault exception is thrown and needs to be handled before the program can resume normal execution

`LRU` - $v$ bits - indicates the LRU ordering of the pages resident in the RAM

### Arithmetic

Assuming Byte Addressing, given a VA of $v+p$ bits, and a PA of $m+p$ bits, we know that:

1. The VM is of size $2^{v+p}$ bits
2. The RAM is of size $2^{m+p}$ bits
3. The pagetable stores $(2+m+v)2^v$ bits because there are $2^v$ rows with $m$ bits of PPN, 2 bits for `D` and `R` and $v$ bits for LRU

The pagetable is stored in the physical memory because of its large size. A pagetable pointer is used by the OS to deremine the starting point of the page table,

The disadvantage of storing the pagetable in the RAM is that each memory access is now actually two memory accesses because one is to get back the PA from the VA and the second one to get the actual content needed from the PA.

### TLB: Translation Lookaside Buffer

A small FA cache to store the most recently used page table entries. cache on top of cache. AMAZING!

#### Super Locality of Reference

We know that there is locality of reference in memory address reference patterns. Therefore there is super locality of page number reference patterns (hit-rate of the TLB 99\%99% in practice).

### Demand Paging

basically lazy loading from swap space

All data associated with a program is first placed onto the swap spaced. Only the data that is requested by the program's instructions is placed in the RAM as an when it is requested

The OS Kernel is (one of the) first programs that is loaded onto the physical memory when our computer is started up. It maintains an organised array of pages on disk.

When a request is made to open a program through the OS, it Allocates and prepares almost the entire virtual memory space for this program on the disk’s swap space. Only the program's main function and inital stack is put into the RAM to begin with

When a program starts executing a lot of page faults occur until most of its working memory makes it into the RAM. The kernel updates the corresponding entries of the Pagetable and the TLB when stuff is put into the RAM.

Replacing resident pages works the same way as it does in the cache using a write-back approach


## Context Switching
A single core CPU is capable of running many programs – seemingly at the same time.

Actually, the CPU switches the execution of each programs from time to time, so rapidly that it seems like all programs are all running at once as if we have more than one CPU. This technique is called rapid context switching.

Context switch refers to the procedure that a CPU must follow when changing the execution of one process with another. This is done to ensure that the process can be restored and its execution can be resumed again at a later point.

Proper hardware support that enables rapid context switching is crucial as it enables users to multitask when using the machine.

To distinguish one program's VA from anothers, a set of VA are assigned a context number (PID). A *context* is a set of mappings from VA to PA associated with one process

This PID can be appended to the VPN to find its correct PPN

An additional register is used in the MMU to store the PID. The TLB tag field contains both the VPN and the PID. In case of a miss, the Pagetable Pointer is updated to point to the beginning of the pagetable section for the required PID

## Using a Cache with VMem

1. Before MMU (using VA)
   1. No MMU access on hit
   2. Need to flush cache on context switch

2. After MMU (using PA)
   1. MMU access every time
   2. No flushing when changing contexts

Since the PO is the same in the VA and the PA, then two computations can happen in parallel:

1. VPN to PPN mapping
2. finding the correct cache line in the cache

![something](https://dropbox.com/s/mdgucv6qubun01l/cachemmu2.png?raw=1)

What happens if the page is Resident but there’s a cache MISS? Cache must be updated by fetching the data from the Physical Memory.

What happens if the page is Not Resident? Page must be fetched from the swap space and copied over to the Physical Memory. Then, we update the cache.

