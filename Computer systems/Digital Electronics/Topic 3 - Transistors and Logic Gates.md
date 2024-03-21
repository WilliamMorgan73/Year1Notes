# Transistors
2 ports $d$ and $s$ are connected depending on voltage of $3^{rd} \; (g)$

![[Transistors image.png]]

$nMOS$ transistors are off a $g$ low, on at $g$ high
$pMOS$ transistors are on at $g$ low, off at $g$ high

# From transistors to gates
## Not gate
- If $A$ is **high** then the $p-MOS \; P1$ is off and the $n-MOS \; N1$ is on, so $Y$ is connected to $GND$, i.e., **low**
- If $A$ is **low** then the $p-MOS \; P1$ is on and the $n-MOS \; N1$ is off, so $Y$ is connected to $V_{DD}$, i.e., **high**

![[Pasted image 20240308134702.png]]


| A   | $P1$ | $N1$ | $Y$ |
| --- | ---- | ---- | --- |
| $0$ | on   | off  | $1$ |
| $1$ | off  | on   | $0$ |

## NAND gate

![[Pasted image 20240308134810.png]]

| $A$ | $B$ | $P1$ | $P2$ | $N1$ | $N2$ | $Y$ |
| --- | --- | ---- | ---- | ---- | ---- | --- |
| $0$ | $0$ | on   | on   | off  | off  | $1$ |
| $0$ | $1$ | on   | off  | off  | on   | $1$ |
| $1$ | $0$ | off  | on   | on   | off  | $1$ |
| $1$ | $1$ | off  | off  | on   | on   | $0$ |

## AND gate
Made from combining a **NAND** gate and a **NOT** gate

![[Pasted image 20240308135153.png]]

# Beneath the digital abstraction
A chip does not really deal in $0s$ and $1s$
The **voltages** are real numbers between $0V$ and $5V$ (typically)

We can take $0V$ to indicate output $0$ and $5V$ to indicate output $1$, but need to tolerate **noise**

## Supply voltage
The **low** voltage in the system (Connected to **ground (GND)**) is $0V$
The **high** voltage is called $V_{DD}$, typically $5V$

The mapping of continuous voltage measured at any point in the circuit to discrete $0$ and $1$ of the digital abstraction is governed by defining **logic levels**

## Logic levels

![[Pasted image 20240308135551.png]]

Permitted range for high output: $V_{OH}$ to $V_{DD}$
Permitted range for low output: $GND$ to $V_{DL}$
Acceptable range for high input: $V_{IH}$ to $V_{DD}$
Acceptable range for low input: $GND$ to $V_{IL}$

Noise margins:
$$NM_H=V_{OH}-V_{IH}$$
$$NM_L=V_{IL}-V_{OL}$$

## The static discipline
A guarantee that "if inputs meet **valid input thresholds**, then the system guarantees outputs will meet **valid output thresholds**" and will not fall into the forbidden zone

Gates are grouped into **logic families**: the gates of the same family obey the static discipline when used with other gates in the family

This means that (given noise limits) you can successfully apply the **digital abstraction** and **combine elements** without further concern about logic levels or analogue values


| Logic Family | $V_{DD}$       | $V_{IL}$ | $V_{IH}$ | $V_{OL}$ | $V_{OH}$ |
| ------------ | -------------- | -------- | -------- | -------- | -------- |
| TTL          | $5(4.75-5.25)$ | $0.8$    | $2.0$    | $0.4$    | $2.4$    |
| CMOS         | $5(4.5-6)$     | $1.35$   | $3.15$   | $0.33$   | $3.84$   |
| LVTTL        | $3.3(3-3.6)$   | $0.8$    | $2.0$    | $0.4$    | $2.4$    |
| LVCMOS       | $3.3(3-3.6)$   | $0.9$    | $1.8$    | $0.36$   | $2.7$    |
# Moore's law
Transistor density doubles in $2$ years or computer processing power doubles every $18$ months

