## Ideal Chars of Comb Circuits

1. High gain = more noise margin
2. Cheap and small
3. zero power dissipation - no power dissipated when the circuit isn't changing states
4. Non linear gain - voltage changes quickly when the input changes: minimises power loss.
5. functional accuracy

## MOSFET

*M*etal *O*xide *S*emiconductor *F*ield *E*ffect *T*ransitors. Four terminal controlled voltage switches

A MOSFET has two "diffusion terminals" (source & drain). If the voltage at the gate terminal is large enough, it creates a conducting channel and the MOSFET turns on. Otherwise, this conducting channel does not form and the MOSFET remains off.

1. MOSFET turns `1`s to `0`s or vice versa.
2. It has 4 terminals, Input is supplied at the gate, and the output is obtained at the drain
3. The current flow between the source and the drain ($I_{DL}$) is proportional to the $\cfrac{W}{L}$ (the width and the length) of the MOSFET
4. The source and the drain are physically symmetrical. We name them depending on the type of MOSFET

1. Reverse-biased: a state whereby D is insulated from S, where current cannot flow from D to S in the presence of applied voltage.
2. A FET that is “ON” refers to a state whereby there exists a connection between D and S, so that current can flow through them.
3. A FET that is “OFF” referes to a state whereby there is no connection between D and S. Current cannot flow through them.

There are two types of MOSFETS:

### NFET

1. In the NFET, the source and the drain are n-doped and the bulk is p-doped

2. The majority charge carrier for the bulk are $e^o$. The majority charge carrior for the source and drain are $e^-$. Typically, the bulk is connected to GND to keep the PN junction rev biased.

3. The bulk and the S is connected to $GND$ to keep the PN junctions rev biased. This ensures that no current leaks between the source and the bulk and the drain and the bulk. When the NFET is on, electrons flow from the S to the D (current flows from D to S).

4. The NFET is on when the $V_{gs}$ = $V_g - V_s > V_{th}$. Since $V_s = 0$ we have that the NFET is off when $V_g < V_{th}$ and on when the $V_g > V_{th}$. An n-channel is formed between the S and the D.

5. $V_{th}$ for NFET is positive.

6. The output of the NFET is at the D terminal. The output of an ON NFET is `0`

### PFET

1. In the PFET, the source and the drain are p-doped and the bulk is n-doped

2. The majority charge carrier for the bulk are $e^-$. The majority charge carrior for the source and drain are $e^o$. Typically, the bulk is connected to VDD to keep the PN junction rev biased

3. The bulk and the S is connected to $V_{DD}$ to keep the PN junctions rev biased. This ensures that no current leaks between the source and the bulk and the drain and the bulk. When the PFET is on, holes flow from the S to the D (current flows from S to D).

4. The PFET is on when the $V_{gs}$ = $V_g - V_s < V_{th}$. Since $V_s = V_{DD}$ we have that the NFET is off when $V_g > V_{th} + V_{DD}$ and on when the $V_g < V_{th} + V_{DD}$. A p-channel is formed between the S and the D.

5. $V_{th}$ for PFET is negative

6. The output of an ON PFET is `1`

![mosfets_internal](https://dropbox.com/s/px5ev6j9ae22ceg/pnfet.png?raw=1 "mosfets_internal")

![mosfets_circuitdia](https://dropbox.com/s/qd1zhsulqjmknv2/pfetnfet.png?raw=1 "mosfets_circuitdia")


### Naming

Naming of S and D. The majority charge carrier is always meant to be **drained** at D and **sourced** at S, meaning that it flows from S to D.

## Complementary MOS circuitry

There are two parts of a CMOS circuit: the pull-up circuit and the pull-down circuit

![cmos_schem](https://dropbox.com/s/ywble3yr4bxj99z/cmos.png?raw=1 "cmos_schem")

The job of these circuits is to ensure that $V_{DD}$ never connects to $GND$ directly, as that would result in a short circut.

To make a combinational circuit, the PU and PD circuits are made such that:

1. The PU circuits connect the output to $V_{DD}$ and the PD circuits disconnect the output from $GND$ when the output needs to be high `1`
2. The PD circuits connect the output to $GND$ and the PU circuits disconnect the output from $V_{DD}$ when the output needs to be low `0`

Contents of the pull-up circuit:

1. All FETs in the pull-up circuit are PFETs.
2. All of their bulks and sources are connected to the $V_{DD}$


Contents of the pull-down circuit:

1. All FETs in the pull-up circuit are PFETs.
2. All of their bulks and sources are connected to the $GND$

Here is the complements recipe for cmos circuits:

![complements](https://dropbox.com/s/y9o0f8qba2ura21/cmoscomp.png?raw=1 "complements")


### Propagation Delay $t_{pd}$

Assume the output of a device is initially invalid. The propagation delay is the time taken for the device to produce a valid output, measured the moment it was given a valid input.

This is the maximum of the propagation delays of all paths to the output from the inputs.

### Contamination Delay $t_{cd}$

Assume the output of a device is initially valid. The contamination delay is the time taken for the device to produce an invalid output, measured from the moment it was given an invalid input.

This is the minimum of the contamination delays of all paths to the output from the inputs.