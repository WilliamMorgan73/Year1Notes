# Binary addition
$$1+0 = 1$$
$$1+1=10$$
$$1+1+1=11$$
$$1+1+1+1=100$$
# Binary Multiplication
Same as decimal long multiplication, but easier
![[Pasted image 20240305162915.png]]

# Overflow
When the number is too large for the registers
Let the register be an $8-bit$ register, if the binary number becomes $9 \; bits$, overflow would occur.
This should trigger a flag in the **status register**, but can cause errors

# Negative numbers
## Signed magnitude
Add a single-bit flag
- $0$ for positive numbers
- $1$ for negative numbers

$$0000 \; 0110=6$$
$$1000 \; 0110=-6$$
The first bit dictates the sign
However, it makes binary arithmetic messy

## Ones complement
The negative of a number is represented by flipping each bit
### Example
$$0100 \; 1001_2=73_{10}$$
$$1011 \; 0110_2=-73_{10}$$
Has two representations for 0
$$1111 \; 1111 \; or \; 0000 \; 0000$$

## Twos-complement
Perform ones complement and add one
Or
Starting from right to left, keep the bits the same until you reach the first $1$, then inverse them after it.

### Example
$$73=0100 \; 1001$$
$$-73=1011 \; 0111$$

## Add a bias:
Used in storing floating point numbers
Stores a number $N$ as an unsigned value $N+B$, where $B$ is the bias (typically half the unsigned range)
For $k-bit$ numbers add a bias of $2^{k-1}-1$, then store in normal binary
E.g., For an $8-bit$ number: $2^7 -1=127$
Can store numbers between $-(2^{k-1}-1)$ and $2^{k-1}$
### For example
$-65_{10}$ stored as $-65+127=62$ becomes $0011 \; 1110$
The higher order bit **does not indicate** the sign of the number in the normal way


# Floating point representation
Contains $3$ parts:
1. The sign bit $S$
2. The exponent $e$
3. The mantissa $M$

Representing the number $(+ \; or \; -) \; M\times 2^e$

Single precision $(32-bit)$ floating point numbers have:
- $1-bit$ sign
- $8-bit$ exponent
- $23-bit$ mantissa

![[Pasted image 20240306112608.png]]

## The sign bit $S$
- $0$ indicates a positive number
- $1$ indicates a negative number

## The exponent $e$
Value in the range $-126$ to $127$
Stored with **a bias 127** is added giving a number between $1$ and $254$

The $8-bit$ exponent field can store values in the range $0$ to $255$, but $0$ and $255$ have **special meanings:**

- Exponent field $0$ with mantissa $0$ gives the number zero
- Exponent field $0$ with non-zero mantissa gives "Subnormal numbers"
- Exponent field $255$ with mantissa $0$ gives $\pm \infty$
- Exponent field $255$ with non-zero mantissa gives not a number

## The mantissa $M$
Some binary number like $1.\fbox{10101010110}$
Always scaled so that the radix point is after the leading $1$

Hence, we need **not store** the leading $1$, we can assume it is there
We only store **23 binary digits** of the fractional part: $10101010110$

## Example

$$\fbox{0}\fbox{01111100}\fbox{01000000000000000000000}$$
- Sign $0$ - Positive number
- Exponent field is $124$, so $e=124-127=-3$
- Mantissa field is $010$, so the actual mantissa is $1.01000...=1.25$

$$1.25\times2^{-3}=\frac{1.25}{8}=0.15625$$
## Example
$$-12.375_{10}=1100.011_2$$
$$1100.011=1.100011\times2^3$$
Sign 1 is to represent a **negative**
Mantissa is $1.100011$, we will store $100011000...$
Exponent is $3$, we will store $130_{10} = 1000 \; 0010_2$ after adding the bias
$$110000010\fbox{100011}\fbox{000000000000000}$$
