# Positional number system
The **base** (or **radix**) of the number system is the number of symbols (including $0$)
We use **positional number systems** to represent values
E.g.,
$$cab.bc_3=201.12_3$$

## Conversions
Converting to base 10 can be done with this table

| Position          | 2     | 1     | 0     | .   | -1       | -2       |
| ----------------- | ----- | ----- | ----- | --- | -------- | -------- |
| $Base^{Position}$ | $2^2$ | $2^1$ | $2^0$ | .   | $2^{-1}$ | $2^{-2}$ |
| Decimal value     | $4$   | $2$   | $1$   | .   | $.5$     | $.25$    |
| Example           | $1$   | $1$   | $0$   | .   | $1$      | $1$      |
$110.11=$
$$1 \times 2^2=4$$
$$1 \times 2^1=2$$
$$1 \times 2^{-1}=.5$$
$$1 \times 2^{-2}=.25$$
$$=6.75_{10}$$

# Binary
Each digit in a binary number system is known as a bit

A bit can have only one of two possible values
- $0$
- $1$

Groups are bits are known as:
- Nibble
	- $4 \; bits$
- Bytes
	- $8 \; bits$
- Half word
	- $16 \; bits$
- Word
	- $32 \; bits$
- Double word
	- $64 \; bits$

Word is CPU dependent - Sometimes refers to $64 \; bits$

# Hexadecimal
$16$ distinct symbols
$$0,1,2,3,4,5,6,7,8,9,A,B,C,D,E,F$$
## Advantages
- More compact than other number systems
- Easy to convert between binary and hexadecimal

## Example

| Position          | 2      | 1      | 0      | .   | -1        | -2          |
| ----------------- | ------ | ------ | ------ | --- | --------- | ----------- |
| $Base^{Position}$ | $16^2$ | $16^1$ | $16^0$ | .   | $16^{-1}$ | $16^{-2}$   |
| Decimal value     | $256$  | $16$   | $1$    | .   | $.0625$   | $.00390625$ |
| Example           | $C$    | $2$    | $D$    | .   | $1$       | $0$         |
$C2D.10=$
$$C \times 16^2=3072$$
$$2 \times 16^1=32$$
$$D \times 16^{0}=13$$
$$1 \times 16^{-1}=.0625$$
$$=3117.0625_{10}$$
# Translation from Binary to Hex
Starting from the **radix point**, separate the binary number into groups of **four** binary digits (nibbles)
Then translate each group to Hex

## Example
$$11 \; 0101 \;1101 \; 1000.001=35D8.2_{16}$$
$$0011=3$$
$$0101=5$$
$$1101=D$$
$$1000=8$$
$$.0010=2$$

# Translation from Hex to Binary
Translate each character individually into binary, then combine

# Converting Decimal to Binary
Repeatedly divide the number by $2$, until you reach $\frac{0}{2}$
Put the remainders down **right to left** from radix point
Convert $13_{10}$ to Binary

$$\frac{13}{2}=6 \; Remainder =1$$ 
$$\frac{6}{2}=3 \; Remainder=0$$
$$\frac{3}{2}=1 \; Remainder =1$$
$$\frac{1}{2}=0 \; Remainder =1$$
Result is $1101_2$

## Decimal fractions to binary
Repeatedly multiply the number by $2$, until fractional part is $0$
If the $i^{th}$ result  $\geq$ $1$, place $1$ in the $i^{th}$ position. to the right of the radix, retain only fractional part
Else, place $0$ in the $i^{th}$ position to the right of the radix

## Example
$$0.40625_{10}$$
$$0.40625\times 2=0.8125 \; Place \; 0$$
$$0.8125\times 2=1.625 \; Place \; 1$$
$$0.625\times 2=1.25 \; Place \; 1$$
$$0.25\times 2=0.5 \; Place \; 0$$
$$0.5\times 2=1 \; Place \; 1$$

Answer $0.01101_2$

