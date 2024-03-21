# Timing
In any physical gate or circuit there is a delay between the input changing and the output adjusting appropriately

![[Pasted image 20240309122338.png]]

We can break this delay down to a lower bound and an upper bound
## Contamination delay $t_{cd}$
The min delay before the output changes

## Propagation delay: $t_{pd}$
The max delay before the output is stable

## Causes of delay
- Capacitance and resistance in a circuit
- The speed of light limitation

## Reasons why $t_{pd}$ and $t_{cd}$ may be different
- Different rising and falling delays
- A circuit may have multiple inputs and outputs, some of which are faster than others
- Circuits slow down when hot and speed up when cold

# Critical paths

![[Pasted image 20240309122801.png]]

The **critical path** is the path determining the propagation delay of the circuit
- The **longest path** in the circuit
- For the circuit above this is
$$t_{cd}=2t_{pd \; AND} + t_{pd \; OR}$$

The **short path** is the path determining the contamination delay of the circuit
- The **shortest path** in the circuit
- In the circuit above this is
$$t_{cd}=t_{cd \; AND}$$

## Gate delay
Gate delay can also give rise to so called **Hazards** or **Glitches** at the output
These manifest themselves as unwanted brief logic level **changes at the output in response to changing inputs**
Hazards are classified into **static** and **dynamic**
- Static
	- Output undergoes a **momentary transition** when one input changes when it is supposed to remain unchanged
- Dynamic
	- Output **changes more than once** when it is supposed to change just once

# Timing diagrams
Used to visually represent Hazards
This shows the logical **value of a signal as a function of time**, for example the following timing diagram shows a transition from $0$ to $1$ and then back again

![[Pasted image 20240309132708.png]]

## Static and dynamic hazards

![[Pasted image 20240309132725.png]]

# Hazard removal
The presence of a static hazard is apparent in the Karnaugh map of the output
A static hazard can be removed by covering the adjacent prime implicants by a redundant circle to **eliminate the dependency on the variable causing the hazard**
- To remove a $1$ hazard
	- Draw the K-map of the output concerned
	- The $1$ hazard will occur when two adjacent $1s$ are not covered by the same circle
	- Add another term (circle) which overlaps the essential terms
- To remove a $0$ hazard
	- Draw the K-map of the complement of the output concerned
	- Add another term (circle) which overlaps the essential terms
	- Consider the compliment of that term and add the original circuit

Removing dynamic hazards is not covered in this module

## Example
$$Y=(\overline{A}\wedge \overline{B}) \vee (B \wedge C)$$

![[Pasted image 20240309133342.png]]

# Adder
The full adder circuit we looked at takes **$3$ gate delays** for the carry out to be computed

![[Pasted image 20240309133522.png]]

If we can **pre-compute the first level** there are only 2 gate delays once the carry in arrives

# Ripple adder
The computation of the carry bit **ripples** through the chained adders

![[Pasted image 20240309133612.png]]

A k-bit ripple adder will take $3+2(k-1)=2k+1$ gate delays to compute $c_{out}$
So a $32-bit$ adder takes $65$ gate delays

# Carry-Lookahead adder
From the basic rules of binary addition we can define two functions

**Generate**
$G(A,B)=1$ if $A$ and $B$ would cause $c_{out}$ even if $c_{in}=0$

**Propagate**
$G(A,B)=1$ if $A$ and $B$ would cause $c_{out}$ even if $c_{in}=1$


$$G(A,B)=A \; AND \; B$$
$$P(A,B)=A \; OR \; B$$

Carry occurs if it is **generated** or if there is carry in and it is **propagated**
$$C_{out}=G(A,B) \vee P(A,B) \wedge C_{in}$$

![[Pasted image 20240309134039.png]]

$$C_{out}=G_4 +P_4\times C_3$$
$$=G_4+P_4 \times (G_3 + P_3 \times C_2)$$
$$=G_4+P_4 \times (G_3 + P_3 \times (G_2 + P_2 \times c_1))$$
$$=G_4+P_4 \times (G_3 + P_3 \times (G_2 + P_2 \times (G_1 + P_1 \times C_{in})))$$
$$=G_4+P_4G_3+ P_4P_3G_2 +P_4P_3P_2G_1+P_4P_3P_2P_1 \times C_{in}$$

We can compute every $P_1$ and $G_1$ in one gate delay
So we can compute $C_{out}$ (and all the intermediate carries) in $3$ gate delays ($1$ for $P_1,G_1$ an AND layer and an OR layer)
We could compute the full sum in $4$ gate delays

![[Pasted image 20240309143206.png]]

We could create a CLA which adds $n-bit$ numbers in constant gate delay
It would require order $n^2$ gates and gates taking order $n$ inputs
This is impractical for large n

## First solution
Chain $4-bit$ CLAs

![[Pasted image 20240309143336.png]]

The carry now ripples along the chain $4-times$ as fast as originally

Rather than letting the carry ripple through the CLAs, we can pre-compute whether it would be generated or propagated by each CLA

![[Pasted image 20240309143459.png]]

We now have $16-bit \; 2-level$ CLA

**Gate delays:**
- $1$ gate delay to compute first (bit) level $Gs, Ps$
- $2$ gate delays to compute second (block)  level $Gs, Ps$
- $2$ gate delays to compute carries across the whole system
- $1$ gate delay to compute sums across the whole system

Total **$6$ gate delays**
A standard $16$-bit ripple carry adder would take $33$ gate delays
These $16$-bit adders could be chained to give an $n$-bit adder with gate delay $2(\frac{n}{16})+4$
