## Contexts and Processes

A more complete list of components that make up a process context are:

1. Values of R0, R1, ... R30
2. VA to PA mapping
3. PC value
4. Stack state
5. Program (and shared code)
6. Virtual I/O devices (console, etc)

![OS](https://dropbox.com/s/fvo6fllqrwwg2qr/context.png?raw=1)

## Kernel Mode and User Mode

Kernel Mode and User Mode

To support a safe virtual machine for each process, we need to establish the notion of dual mode system, that is a system that has a Kernel Mode (privileged mode) and a User Mode (non-privileged mode):

1. The OS Kernel runs in full privilege mode called the Kernel Mode, and it oversees the execution of all processes in the computer system, handles real I/O devices, and emulate virtual I/O device for each process.
2. All other programs do not have such privileged features like the kernel. We call these programs as running in non-privileged mode called the User Mode with limited access to any hardware resources:
   1. No direct access to actual hardware
   2. No direct access other process’ address space
   3. No knowledge about other processes’ context and processor state
3. The Kernel will handle the need of these programs running in user mode for access to various hardware resources: access to I/O devices, interprocess communication, allocation/deallocation of shared memory space, etc.

This is a major benefit: programs can be easily written as if they have absolute access to all hardware resources (not just the physical memory), without having to worry about sharing them with other running processes.

## OS Multiplexing - Context Switching

![OS](https://dropbox.com/s/p5r7q2uit6vbdkz/process.png?raw=1)

1. At first, the CPU runs some task from P1.
2. After some time `t`, imagine that a timed interrupt (caused by other asynchronous hardware, e.g: a timer) occurs. This causes the CPU to execute part of the kernel program that handles such asynchronous interrupt, hence pausing the execution of P1.
3. This interrupt handler takes control of the CPU when hardware interrupt occurs, and saves the current states (PC, Registers, etc) of P1 to a dedicated space (Kernel Stack) in the Memory Unit (so that P1’s progress is not lost and can be resumed later on) before performing a *context switch*:
4. Load the states of P2 to the CPU (and also the required resources, mapping, etc), and
5. Resume the execution of P2
6. P2 runs and progresses for some time t before another hardware interrupt occurs. The entire context switch process is repeated to pause P2, resume P1, and so forth.
7. The key technology that allows for OS Multiplexing is the asynchronous hardware interrupt.

In practice, the interrupt handler will examine the cause of the asynchronous interrupt. In the event of periodic interrupt caused by a timer, the handler will delegate the task to the kernel scheduler whose job is to decide which process to run next, and prepare the necessary information / context to load this process back into the CPU so that the selected process may resume smoothly. When the scheduler returns to the handler, the handler resumes execution of the CPU by simply setting $PC \leftarrow Reg[XP] - 4$

We will simply call asynchronous interrupt as just “interrupt” for simplicity. A synchronous interrupt is called as “trap” instead (see the later chapters).

There must be some piece of hardware that triggers these interrupts periodically. The hardware is responsible for directing the `PC` to the correct address where the interrupt is handled. During this handling (KM) other interrupts must be disabled so that the CPU can safely save data for one process and restore another's

## Beta specific

A kernel scheduler will typically configure some system timer to fire at some interval. This timer runs asynchronously with the CPU, and sets the `IRQ` signal to `1` each time it fires.

The interrupt hardware configuration forces the CPU to execute the interrupt handler at `XAddr` in the next cycle each time the timer fires.

The first few instructions of the interrupt handler saves current process states (R0 to R30 contents, PC state, stack, and others) in process table.

**Process table**: a Kernel data structure that stores all the states of running processes in the machine. It lives in the Kernel memory space. The kernel keeps track on which process is currently scheduled to run in the CPU.

Then, the handler will figure out which specific **service routine** needs to be called to *service* the interrupt, e.g: scheduler, or I/O routines.

Afterwards, the service routine returns back to this interrupt handler. The handler finally sets $PC \leftarrow Reg[XP]-4$

## Restricting access to Kernel Mode

This restriction is implemented via hardware:

1. Programs running in user mode (PC31 == 0) can never branch or jump to instructions in the kernel space.
2. Computations of next instruction address in `BEQ`, `BNE`, and `JMP` cannot change PC31 value from `0` to `1`.
3. Programs runing in user mode (PC31 == 0) can never load/store to data from/to the kernel space.
4. Computations of addresses in `LD`, `LDR` and `ST` ignores the MSB.
5. Entry to the kernel mode can only be done via restricted entry points. In $\beta$, there are only three entry points:
   1. Interrupts (setting PC to Xaddr: 0x8000 0008),
   2. Illegal operations (setting PC to ILLOP: 0x8000 0004), or
   3. Reset (setting PC to RESET: 0x8000 0000)

### Re-entrancy

When the CPU is in kernel mode, it may or may not allow other interrupts to occur (if it does - re-entrant)

Beta kernel mode is not re-entrant, interrupts are disabled when it is in Kernel mode via hardware.

Uninterruptable kernel is scary - kernel code must be very carefully written so that it is not buggy (stuck in inf loops) because it will just result in system crashes

## Traps

A synchronus interrupt that is caused by a user process itself is called a trap. A trap can be caused by illop, exceptions (result in process termination) or they can be caused by intended interrupts i.e. a sys call (aka svc, superviser call) to use a particular hardware resource. This is done by leaving the index of the desired hardware resource needed in `R0` and executing a special ILLOP code.

1. Control unit sets PCSEL = 011, and saves PC+4 into Reg[XP]
2. The PC will execute the instruction at location ILLOP in the next cycle where the illegal operation handler resides.
3. The illop handler will look at Reg[R0] and invoke the right service routine to provide the requested service.
4. Upon returning, the service routine will put its return the result in Reg[R0].
5. The illop handler resumes the execution of the originating process by jumping back to the `XP`
