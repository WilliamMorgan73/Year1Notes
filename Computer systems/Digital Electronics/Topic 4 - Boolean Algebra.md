# Functionally complete sets
A **functionally complete set of Boolean operators** is one which can be used to *express all possible truth tables* by combining members of set into a Boolean expression.

Any logic circuit can be constructed with just these three operators
- **AND, OR,** and **NOT**
- They form a **functionally complete set**

NOR and NAND gates alone form a functionally complete set

## NOR gates
**AND**
$$A\wedge B = \overline{ \overline{\left(A\vee A\right)} \vee \overline{\left(B \vee B \right)}}$$
**OR**
$$A \vee B = \overline{\overline{\left( A\vee B \right)} \vee \overline{\left( A \vee B \right)}}$$
**NOT**
$$\overline{A}=\overline{A \vee A}$$

## NAND gates
**AND**
$$A\wedge B = \overline{ \overline{\left(A\wedge B\right)} \wedge \overline{\left(A \wedge B \right)}}$$
**OR**
$$A \vee B = \overline{\overline{\left( A\wedge A \right)} \wedge \overline{\left( B \wedge B \right)}}$$
**NOT**
$$\overline{A}=\overline{A \wedge A}$$
### NAND chips
NAND gates are easier to make (use less silicon for same performance) than NOR gates.

# Digital design principles
Digital design is all about **managing the complexity** of huge numbers interacting elements. Some principles help humans do this:
- **Abstraction:** Hiding details when they aren't important
- **Discipline**: Restricting design choices to make things easier to model, design and combine. E.g., the logic families and the digital abstraction

**The three -y's**
1. **Hierarchy:**
	- Dividing a system into modules and submodules
2. **Modularity**
	- Well-defined functions and interfaces for modules
3. **Regularity**
	- Encouraging uniformity so modules can be swapped or reused.

# Circuits
Network that processes discrete-valued variables

A **circuit** has:
- One or more discrete valued input terminals
- One or more discrete valued outputs terminals
- A specification of the relationship between inputs and outputs
- A specification of the delay between inputs changing and outputs responding

![[Pasted image 20240308143046.png]]

The circuit is made up of **elements** and **nodes**:
- An **element** is itself a circuit with inputs, outputs, and specs
- A **node** is a wire joining elements, whose voltage conveys a discrete valued variable

![[Pasted image 20240308143136.png]]

# Combinational logic
Combinational logic rules:
- **Individual gates** are combinational circuits
- Every circuit **element** must be a combinational circuits
- Every node is either an **input** to the circuit or connecting **to exactly one output** of a circuit element
- The circuit has **no cyclic paths** - Every path through the circuit visits any node at most once

## Examples
![[Pasted image 20240308143550.png]]

A is a combinational circuit
B is not a combinational circuit as there is a cyclic path
C is a combination circuit
D is not a combinational circuit as two outputs combine
E is a combinational circuit
F is not a combination circuit as there is a cyclic path

# Truth table to Boolean algebra


| X   | Y   | Z   | F(X,Y,Z) |
| --- | --- | --- | -------- |
| 0   | 0   | 0   | 1        |
| 0   | 0   | 1   | 0        |
| 0   | 1   | 0   | 0        |
| 0   | 1   | 1   | 1        |
| 1   | 0   | 0   | 0        |
| 1   | 0   | 1   | 1        |
| 1   | 1   | 0   | 1        |
| 1   | 1   | 1   | 0        |

## Sum of products
Every Boolean expression can be written as minterms $(1s)$ ORed together
$$(A\wedge B \wedge C) \vee(A\wedge \overline{B} \wedge \overline{C} ) \vee (\overline{A} \vee B \vee C)$$
## Product of sums
Every Boolean expression can be written as maxterms $(0s)$ ANDed together
$$(\overline{A} \vee \overline{B} \vee \overline{C}) \wedge (\overline{A}\vee B \vee C) \wedge(A \vee \overline{B} \vee \overline{C})$$
# Theorems of several variables
## Commutativity

$$B \wedge C = C \wedge B$$
$$B \vee C=C \vee B$$

## Associativity

$$(B \wedge C)\wedge D = B\wedge(C\wedge D)$$
$$(B \vee C)\vee D = B\vee(C\vee D)$$

## Distributivity

$$(B \wedge C)\vee D = (B \wedge C) \vee (B \wedge D)$$
$$(B \vee C)\wedge D = (B \vee C) \wedge (B \vee D)$$

## Covering

$$B \wedge (B \vee C) = B$$
$$B\vee(B\wedge C)=B$$

## Combining

$$B \wedge C \vee B \wedge \overline{C}=B$$
$$(B \vee C) \wedge (B \vee \overline{C})=B$$

## Consensus

$$(B \wedge C) \vee (\overline{B}\wedge D) \vee (C \wedge D)= (B \wedge C)\vee (\overline{B}\wedge D)$$
$$(B \vee C) \wedge (\overline{B}\vee D) \wedge (C \vee D)= (B \vee C)\\wedge (\overline{B}\vee D)$$

## De Morgan's

$$\overline{B_0 \wedge B_1\wedge ...}=\overline{B_0} \vee \overline{B_1}\vee ...$$
$$\overline{B_0 \vee B_1\vee ...}=\overline{B_0} \wedge \overline{B_1}\wedge ...$$

