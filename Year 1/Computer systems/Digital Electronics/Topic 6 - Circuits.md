# Key circuits
## Combinatorial/Combinational circuits
- **Adders**
	- Add the contents of $2$ registers
- **Decoders**
	- Decodes an n-digit binary number into $2^n$ data lines
- **Multiplexors**
	- Use a binary number to select an input

## Sequential circuits
Output depends on state and input i.e., history of input
- **Latches/flip-flops**
	- Basic memory element

# Half-adder
Based on simple addition rules

![[Pasted image 20240308203719.png]]

# Adder
An adder is just the combination of $2$ half adders
![[Pasted image 20240308203748.png]]

## Chaining adders - ripple carry adder
How would you add $2$ $4$ bit registers

![[Pasted image 20240308203839.png]]

# Subtractor
Create a **twos-complement negative** by inverting each bit and adding 1
We subtract $b$ from $a$ by adding $-b$

![[Pasted image 20240308204849.png]]

The NOT gates and setting $c_{in}=1$ give the effect of converting $b$ to $-b$

# Decoder
Translates coded information from one format into another:
- Transforms a set of digital input signals into an equivalent decimal mode at its output

$N$ inputs. $2^N$ outputs
**Only one** output is high at a time

## 1-bit decoder

![[Pasted image 20240308205041.png]]

## 2-bit decoder

![[Pasted image 20240308205108.png]]


Larger decoders require multi-input AND gates to be constructed, requiring a lot of circuitry

Can create deeper circuits with fewer transistors at the cost of slower response

# Multiplexor (MUX)
Chooses $1$ of many inputs to steer to its single output under the direction of control inputs (selector)
- E.g., if the input to a circuit can come from several places a Mux is one way to funnel multiple sources selectively to the single input

![[Pasted image 20240308205936.png]]

A multiplexor has $k+2^k$ **inputs** and $1$ **output**
The first $k$ inputs (selector) represent a binary number
The output takes the value of the remaining input indexed by this binary number

# Tristate
In contrast to a normal buffer which is either $1$ or $0$ at its output, a tristate buffer can be electrically disconnected from the bus wire, i.e., it will have no effect on any other data currently on the bus

![[Pasted image 20240308210111.png]]

## Inverting Tristate 

![[Pasted image 20240308210139.png]]

## Tristate
Therefore a tristate's output can be strengthened by inverting the inverted tristate.

![[Pasted image 20240308210240.png]]

## Using a tristate to create a MUX

![[Pasted image 20240308210309.png]]

# MUX again
A Mux can also be used to implement combinational logic functions
For example, an $8-bit$ Mux can be used to implement functions expressed as a sum of minterms $(SoP)$
$$f=(\overline{x}\wedge \overline{y} \wedge \overline{z}) \vee (y \wedge \overline{z} )\vee (x \wedge y \wedge \overline{z}) \vee (x \wedge y \wedge z)$$
The control inputs are used to select the minterms required at the output

![[Pasted image 20240308210619.png]]

## Example
In this example if we use one of the inputs as a variable, then we can get away with a $4-to-1$ Mux

$$f=(\overline{x}\wedge \overline{y} \wedge \overline{z}) \vee (y \wedge \overline{z} )\vee (x \wedge y \wedge \overline{z}) \vee (x \wedge y \wedge z)$$
$$=(\overline{x}\wedge \overline{y} \vee \overline{x} \wedge y)\wedge \overline{z} \vee (x \wedge y \wedge (z \vee \overline{z}))$$
$$=(\overline{x} \wedge \overline{y} \vee \overline{x} \wedge y) \wedge \overline{z}\vee (x \wedge y)$$

![[Pasted image 20240308210905.png]]

# Building a simple ALU

![[Pasted image 20240308210351.png]]

