Output depends on **history** as well as current input
I.e., the circuit implicitly contains **memory** elements
Fundamental components:
- **Latches**
- **Flip-flops**

# SR-Latch
## NOR latch

![[Pasted image 20240310101249.png]]

Both inputs usually set to $0$
If input $S$ (set) has a pulse of $1$, the output becomes $1$
The output remains $1$ even when the pulse is over
If input $R$ (reset) has a pulse of $1$, the output becomes $0$
The output remains $0$ even when the pulse is over

If output is already $1$, a pulse of $S$ wont change it
If output is already $0$, a pulse of $R$ wont change it

Latches can be used to store a single bit in memory
This sequential circuit has two stable states for a given input (**bistable**)

![[Pasted image 20240310101513.png]]

## NAND Latch

![[Pasted image 20240310102231.png]]

Latches can also be built from NAND gates
In this case the usual state for the inputs is $1$, so the inputs are denoted with bars

# D-Latch
In a latch a pulse on set or reset indicates **what** the new state should be, and **when** it should change
Designing circuits becomes easier if we can separate **what** and **when**

![[Pasted image 20240310102501.png]]

D - **data** input. Defines **what** the new value should be
CLK - **clock** input. Define **when** the new variable should arise

# D Flip-flop
In the D-latch the output can change **whenever** the clock is high
Even better is if we  can make it change **only at the moment the clock goes high**

![[Pasted image 20240310103041.png]]

D flip-flop copies $D$ to $Q$ on the rising edge of the clock and remembers its state at all other times

![[Pasted image 20240310103052.png]]

# Enabled flip-flop
Incorporates an additional input (**enable**) to control whether the data is loaded into the register or not

![[Pasted image 20240310111715.png]]

EN can control the input with a multiplexor, or can control the clock. This is called a **gated clock**
Gated clocks can cause **timing errors and glitches** on the clock

# Problem circuits
The problems are caused by outputs being fed back into inputs: The circuits contains **loops** or **cyclic paths**
To avoid this, we insert **registers** into cyclic paths:
- The registers contain the 'state' of the circuit
- They break the paths
- They only update on a clock edge
- Say they are **synchronised** to the clock

If the clock is **sufficiently slow**, so that all inputs to all the registers have settled before the next clock edge, then race conditions cannot arise
## Example
![[Pasted image 20240310111825.png]]

The gates have a delay of $1ns$

![[Pasted image 20240310111855.png]]

# Synchronous circuits
A **synchronous sequential circuit** consists of interconnected elements such that:
- Every circuit element is either a **combinational circuit** or a **register**
- At least one circuit element is a register
- All registers receive the same **clock signal**
- Every **cyclic path** contains **at least one register**

A **synchronous sequential circuit** has:
- A discrete set of states $\{S_0,...,S_{k-1}\}$
- A clock input, whose rising edge indicates when a state change occurs
- A functional specification which details the next state and all outputs for each possible current state and set of inputs

# Timing
The **dynamic discipline** restricts us to using circuits satisfying timing constraints that allow us to combine components

![[Pasted image 20240310112954.png]]

$t_{setup}:$ time before rising edge during which inputs must be stable
$t_{hold}:$ time after rising edge during which inputs must be stable
$t_{ccq}:$ time until output starts to change
$t_{pcg}:$ time by which output has stabilized

## Setting time
The **clock frequency** determines how fast the computer operates
- It is bound by timing constraints of registers and any CL block in between

Register $2$ will not get an answer until the clock ticks a second time

![[Pasted image 20240310113211.png]]

Time between ticks $(T_c)$ must be at least $t_{pcq}+t_{pd}+t_{setup}$

Rearranging we see that $t_{pd} < T_c-(t_{pcg}+t_{setup})$
$(t_{pcq}+t_{setup})$ is called the **sequencing overhead**

The clock speed and sequencing overhead and normal fixed
Designers must get all elements of combinational logic to work within the bound on $t_{pd}$ in order for the circuit to be reliable

There is also a minimum delay requirement

![[Pasted image 20240310121733.png]]

- $D2$ Must hold its value for at least $t_{hold}$ time after the rising edge
- It could change as soon as $t_{ccq}+c_{cd}$
- Designers have a **min-delay constraint:**
$$t_{ccq}+t_{cd}>t_{hold} \implies t_{cd} > t_{hold}-t_{ccq}$$
- Often in order to allow direct connection of flip-flops, $t_{hold}<t_{ccq}$, so the min-delay constraint isn't technically an issue

## Example
![[Pasted image 20240310122052.png]]

Flip flops:
$t_{ccq}=30ps$
$t_{pcq}=80ps$
$t_{setup}=50ps$
$t_{hold}=60ps$

Gates:
$t_{cd}=25ps$
$t_{pd}=40ps$

Critical path: going through all three gates
Min cycle time is therefore: $t_{pcq}+3t_{pd}+t_{setup}=250ps$
Max frequency is therefore $\frac{1}{250\times 10^{-12}}=4GHz$

Short path: $C \; to \; X'$ and $D \; to \; Y'$. $X' \; or \; Y'$ could change after $c_{ccq}+t_{cd}=55ps$
However, $t_{hold}=60ps$, so $X' \; or \; Y'$ may change before $X$ has reliably set its value to the correct previous value!

### Fixing the hold time violation

![[Pasted image 20240310122550.png]]

Critical path is unaffected so max frequency is still $4GHz$
Short paths now: $T_{ccq}+2t_{cd}=80ps > t_{hold}$, so no hold time violations

# Pipelining
How can we increase the clock frequency

$$T_{pcq}=0.3ns \; \; \; \; \; \; \; \; \; \; T_{setup}=0.2ns$$

![[Pasted image 20240310123129.png]]

Latency: $9.5ns$
Throughput: $\frac{1}{9.5ns}=105MHz$

Insert an additional register in the circuit. $(T_{pcq}=0.3ns \; \; \; T_{setup}=0.2ns)$

![[Pasted image 20240310123228.png]]

Insert another register in the circuit $(T_{pcq}=0.3ns \; \; \; T_{setup}=0.2ns)$

![[Pasted image 20240310123301.png]]