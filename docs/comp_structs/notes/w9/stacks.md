## Named Registers:

R29 - SP, Stack Pointer - address of the top of the stack

R28 - LP, Link Pointer - (return address) address of the instruction just after the function call branch instruction

R27 - BP, Base Pointer - address of the base of the stack frame

The `PUSH(R#)` macro is defined as the two following instructions:
```cpp
ADDC(SP, 4, SP)
ST(R#, -4, SP) // store the contents of R# to Mem[SP-4]
```
In general, the push macro puts the content of `R#` on to the stack and moves SP up


The `POP(R#)` macro is defined as the following instructions:
```cpp
LD(SP, -4, R#) // load the contents of Mem[SP-4] to R#
SUBC(SP, 4, SP)
```
In general, the pop macro puts the thing at the top of the stack into `R#` and moves SP down

```cpp
ALLOCATE(k): ADDC(SP, 4*k, SP)
DEALLOCATE(k): SUBC(SP, 4*k, SP)
```
For allocating memory for locals

This is the standard implementation for procedures:

```CPP
// calling sequence
// push the arguemnts on to the stack in reverse order,
// branch to the start of the function and put the return address in LP
    PUSH(R3)
    PUSH(R2)
    PUSH(R1)
    BR(func, LP)
    INSTRUCTION // this is the address stored in LP

// entry sequence
// push the return address and the old base pointer to the stack
// make the current SP the BP
// this way, the first arguemnt of the function is at BP-12
// and the first local variable of the function is at BP itself, and so on
// Now we finally push the values of all the regs used by the procedure on to the stack for restore later
f:  PUSH(LP)
    PUSH(BP)
    MOVE(SP, BP)
    ALLOCATE(k)
    PUSH(R#)

// return sequence (pop in rev order)
// restore regs, remove locals
// restore the base pointer of the previous stack
// pop and return to the return address in LP
f:  POP(R#)
    DEALLOCATE(k)
    POP(BP)
    POP(LP)
    JMP(LP)
```