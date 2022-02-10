An FSM is a machine which implements a sequential logic function, which is one whoes output depends not only on its current input but its previous inputs (its state) as well

## Moore Machine
A moore machine is a type of FSM where the output of the machine depends only on the current state of the machine. Usually, the output is drawn INSIDE the circle for the state to indicate this

## Mealy Machine
A mealy machine is a type of FSM where the output of the machine depends on both the current state and the input to the machine. Usually, the output is drawn ON TOP OF the arrow for the particular input that it is for.

an FSM has:

1. A set of $k$ states $S_1, S_2, ... S_k$ (where one should be initial)
2. A set of $m$ inputs $I_1, I_2, ... I_m$
3. A set of $n$ outputs $O_1, O_2, ... O_n$
4. Transition rules, $s(S, I)$ for each of the $k$ states and $m$ inputs
4. Output rules, $f(S, I)$ for each of the $k$ states and $m$ inputs (in case of mealy machine) 

![FSM](https://dropbox.com/s/y157lzv1g0lmwpl/Q2.png?raw=1 "FSM")

## Differences Between A Moore And Mealy Machine

### Moore Machine
1. The output obtained is depends only on the current state (regardless of the input).
2. Sometimes, a Moore machine may require more states than a Mealy machine to implement the same thing.
3. The output of a Moore machine is synchronized with the state change, i.e. the output for moore machine is obtained at the next clock cycle.

### Mealy Machine

1. The output of a Mealy machine is affected by both the current state and the current input.
2. Mealy machines react immediately with the presence of an input (instead of having to obtain the output in the next cycle).
3. Typically we can have less states and less transitions. This means that we can potentially use less registers and logic gates (for the CL) in a Mealy machine, potentially reducing its cost (and size).

A Mealy machine is faster and more responsive than the Moore machine since the output can be produced approximately $t_{pd}$ (or almost immediately if $t_{pd}$ of the last CL unit is small) after input arrives.

One clock period typically takes much longer than the $t_{pd}$ of that smaller CL (at the output of the Flip-Flop) because:

- Dynamic discipline has to be obeyed, thus $t_{pd}$ of the bigger combinational circuit should be smaller than the clock period
- Logically, $t_{pd}$ of the smaller combinational circuit should be smaller than the $t_{pd}$ of a bigger combinational circuit, supporting the statement above.

## Enumerating SM

If we have $s$ state bits, $i$ input bits & $o$ output bits, then there are a total of $2^{(o+s)2^{i+o}}$ FSMs possible.

## FSM equivalence & Reduction

![fsm_eq](https://dropbox.com/s/4frikzlus8gcmeo/Q4.png?raw=1 "fsm_eq")

Two states $S_i$ and $S_j$ are equivalent iff for an arbitrary input sequence applied at both states, the same output sequence results

In FSM A, $S_3$ and $S_2$ are identical. This is because both states:

1. Output `1`
2. Transition to $S_0$ on receiving `0`
3. Transition to $S_3$ on receiving `1`
4. No other input that can be fed to the machine

Therefore, we can safely merge $S_2$ and $S_3$ into $S_4$. Then, we can note the same thing for $S_1$ and $S_4$, and merge them together as well.