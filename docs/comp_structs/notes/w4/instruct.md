We can create a machine that is simply programmable, but it also has to support the following features for it to resemble the Universal Turing Machine:

1. An expandable memory unit (to represent that infinite tape)
2. A rich repertoire of operations
3. Ability to generate a new program and then execute it

## Example of a Programmable Control System

Suppose we have a simple sequential logic circuit called Machine $M$ as shown below. It receives one $N$ bit input, and produces two outputs: an $N$ bit `output1` and a $1$ bit `output2`.

This cicuit is termed as a datapath.

A datapath is a collection of functional units made up of combinational devices, registers, and buses.

![img](https://dropbox.com/s/k9m89zfzb7aqopj/B.png?raw=1 "img")

`R1` and `R2` units are not a regular DFF. They accept an additional control signal, denoted as $LE$. These control signals $A_{LE}, B_{LE}$ are fed to R1 and R2 unit works as follows:

If $A_{LE}$ is $1$, then the current input to R1 will be reflected as R1’s output in the next clock cycle. It’s like “enabling” the R1, allowing it to "remember" new value

If $A_{LE}$ is $0$, then R1 will continue to produce it’s old value as an output, whatever last value it was remembered

Different specifications for this control FSM can allow for us to do different things.

However machine $M$ is not a general purpose computer:

1. Limited storage
2. Lmited operations: only `factorial` and `input*(input-1)`.
3. Unable to generate a new program. Entire Control FSM must be replaced for "reprogramming"

A general purpose comp must have:

1. A general purpose data path, which can be used to efficiently solve most problems, and
2. A proper instruction set to allow for easier ways to control it.

## JVN Model

![jvn](https://dropbox.com/s/rjotczxs894klvg/vnm.png?raw=1 "jvn")

The CPU is a part of the computer that executes instructions. A series of these executable instructions is called a computer program.

Instruction Set Architecture (ISA): Figurative Blueprint for CPU.

Ex: x86 (found in desktops and laptops) and ARM (found in embedded and mobile devices)

## Structure of a CPU

![CPU](https://dropbox.com/s/w5dt2ixcx1p6g7q/cpu.png?raw=1 "CPU")

1. It should be able to read/write to the memory unit.
2. Execute the instruction loaded from the MU
3. Read/Write to REGFILE

**The datapath** is an overarching infrastructure that controls what inputs/outputs go to/from each component

**The Control Unit** is made of a program counter (PC) and a control unit (CU).

PC: which instruction to read from the MU.
CU: Gives the appropriate control signals based on the instruction loaded.

**The ALU** is what does the actual computation

## The Memory Unit

Takes in an address, input, output, read, write signals. The smallest unit of addressable memory is of size 1 byte.

Typically reads/writes 32 consecutive bits at once (x86 architecture). This size is called a word. (64 bit for x64 bit arch)

The smallest address of the bytes in the word is used as the address of the entire word.

## Beta ISA

For a machine to be programmable, it must have a set of well defined operations. A combination of these operations can then be used to make larger, programs.

Along with the instruction set, the ISA also defines the supported data types, the # of internal registers, how to address them, and other fundamental features such as addressing mode (read/write), input, output, etc.

[Full Beta Doc](https://dropbox.com/s/2hzbawz9v51g6fu/beta_documentation.pdf?dl=0)

32 Operations supported.

Each instruction is atomic and completed in one clock cycle

All registers are 32 bit wide. There are 33 registers in the CPU:

1 PC register, 32 REGFILE registers. R31 in the REGFILE is ROM set at 0. Reg[Rx] refers to the contents of the register

There are 2 types of instructions in the beta CPU:

![TI](https://dropbox.com/s/6sij3diwmtxs7q3/S4.png?raw=1)

`I[31:0]` are segmented into various sections:

1. OPCODE: `I[31:26]` 6 bits.
2. Rc = `I[25:21]` 5 bits
3. Ra = `I[20:16]` 5 bits

4.1. Type 1:

1. Rb = `I[15:11]` 5 bits

2. Unused = `I[10:0]` 11 bits

4.2. Type 2:

1. c = `I[15:0]` 

