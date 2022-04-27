## SVC

Superviser calls is a 32 bit instruction that triggers the ILLOP exception, hence trapping the processes to the kernel. `000001` op code for SVC in beta.

```cpp
SVC_Handler: 
LD(XP, -4, R0)	| examine the faulting instruction
ANDC(R0, 0xN, R0) | mask out lower N bits
SHLC(R0, 2, R0) | make a word index
LD(R0, SVCtbl, R0) | load service table entry
JMP(R0) | jump to the appropriate handler
```

UUO is a macro that redirects the PC to each subroutine
```cpp
SVCTbl: UUO(HaltH) | SVC(0): User-mode HALT instruction
UUO(WrMsgH) | SVC(1): Write message
UUO(WrChH) | SVC(2): Write Character
UUO(GetKeyH) | SVC(3): Get Key
UUO(HexPrtH) | SVC(4): Hex Print
UUO(WaitH) | SVC(5): Wait(S), S in R3
UUO(SignalH) | SVC(6): Signal(S), S in R3
UUO(YieldH) | SVC(7): Yield()
```

## Async IO Handling

When I/O interrupt requests are made by devices, they may not be immediately serviced by the Kernel.

Each interrupt request usually have a deadline, and the Kernel has to service the request before the said deadline.

For example, the Kernel has to service each keyboard input interrupt request quick enough so as to give the experience of a responsive system.

**Latency** is defined as the amount of elapsed time from interrupt is first requested up until the Kernel **begins** servicing it.

The Kernel scheduler in the kernel has to ensure that the interrupt request is serviced before its deadline.

The amount of latency affects how **real-time** the machine reacts. The shorter the latency, the more responsive it will seem.

## Scheduling Multiple Interrupts

**Weak, non-preemptive measure**: The machine has a fixed ordering of device handling, but it will not pre-empt current service. It will only reorder requests in the interrupt queue based on the types of device.

**Strong, preemptive measure**: Allow interrupt handlers with lower priority to be interrupted only by other handlers with strictly higher priority level. The lower prio interrupted handler can be resumed later on after the higher prio handler has finished execution

We call this type of Kernel **preemptive Kernel** (but not reentrant)

A reentrant kernel is made such that it allows multiple processes (running in different cores) to be executing in the kernel mode at any given point of time without causing any consistency problems among the kernel data structures.

The priority level for each interrupt handler is stored using the higher p bits of PC => the location of the handler in memory changes its prio.

If higher priority interrupts happen at a high rate, requests with lower priorities might be interrupted repeatedly - potentially resulting in *starvation*.

The effective Interrupt Load these devices impose to the CPU is computed by multiplying the maximum frequency of each device interrupt with its own service time.

