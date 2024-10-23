Karnaugh maps allow us to simplify Boolean expressions in an easier way than truth tables

# Example
Say we have the truth table

| A   | B   | C   | Y   |
| --- | --- | --- | --- |
| $0$ | $0$ | $0$ | $1$ |
| $0$ | $0$ | $1$ | $1$ |
| $0$ | $1$ | $0$ | $0$ |
| $0$ | $1$ | $1$ | $0$ |
| $1$ | $0$ | $0$ | $0$ |
| $1$ | $0$ | $1$ | $0$ |
| $1$ | $1$ | $0$ | $0$ |
| $1$ | $1$ | $1$ | $0$ |
Create a Karnaugh table, which is structured like:

![[Pasted image 20240308175750.png]]

To get algebraic expression from this, create the biggest rectangles you can make.
![[Pasted image 20240308175826.png]]
$$Y=AP$$

## Rules
To make the biggest box we can, we can:
- Use corners
- Use any size of $2^x$ e.g., $2x2$, $4x2$, $4x4$, etc

# 7-segment display driver
4 inputs $D_3, D_2, D_1, D_0$ written $D_{3:0}$
7 outputs

Input represents $4-bit$ binary number
Output should show the corresponding decimal

![[Pasted image 20240308202925.png]]

![[Pasted image 20240308202938.png]]

## Unspecified inputs
So far we have assumed unspecified inputs are $0s$
We could equally output $1s$ if it helps reduce redundancy, as we can make bigger terms.
![[Pasted image 20240308203030.png]]

