## Fetch Phase

The CPU incrermemnts the address in the PC, and then fetches the instruction at that address to execute.

## Decode Phase

A RoM that hard codes the output for each input is used to decode the instruction in beta CPU.

There are mainly 3 types of instructions:

1. Memory Access: Read/Write b/n the REGFILE and the MU
2. Arithmentic: Involving the ALU
3. Branch Instructions: Anything that changes the value of the PC

## PC

1. The output of the PC is connected to the input address of the MU. The MU produces the operation stored at that address
2. In each cycle, the PC's address is incremented by 4 (unless otherwise determined by the PCSEL signal)

If `Reset = 1`, `PC = 0x80000000`. Why is the MSB `1`?

# Register Files

32 Registers, each 32 bit wide. Each register is addressable in `5` bits.