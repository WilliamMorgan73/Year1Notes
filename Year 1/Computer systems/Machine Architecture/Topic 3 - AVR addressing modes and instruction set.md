# Registers only addressing modes
## Direct register addressing - Single register
The operand is container in register $d \; (Rd)$
![[Pasted image 20240323122513.png]]

### Example NEG
Replaces the contents of register $Rd$ with its two's complement

$$NEG \; Rd$$

## Direct register addressing - Two registers
Operands are contained in registers $r \; (Rr)$ and $d \; (Rd)$
![[Pasted image 20240323122549.png]]

### Example ADD
Adds two registers $Rd$ and $Rr$ and places the result in $Rd$

$$add \; r1,r2$$
Adds $r2$ to $r1$
$$add \; r28,r28$$
Adds $r28$ to itself

# Data addressing modes
## Direct data addressing
![[Pasted image 20240323123925.png]]
A 16-bit data address is contained in the 16 Least Significant Bits (LSBs) of a two word instruction. (the program counter will be incremented by two: PC ← PC + 2)

Rd/Rr specifies a destination or source register

### Example LDS
Loads one byte from the data space to a register

$$lds \; r2, \; \$FF00$$
Load $r2$ with the contents of the data space location $\$FF00$

## Indirect data addressing
![[Pasted image 20240323124457.png]]
Operand address is the contents of the X, Y, or the Z register.
The schematic figure does not show opcodes.

### With pre-decrement
![[Pasted image 20240323124658.png]]
As indirect, but the X, Y, or the Z register is decremented before the operation.
The schematic figure does not show opcodes.

### With post-increment
![[Pasted image 20240323124725.png]]
As indirect, but the X, Y, or the Z register is incremented after the operation.
The schematic figure does not show opcodes.

### With displacement
![[Pasted image 20240323124745.png]]
Operand address is the contents of the Y or Z register, added to the six-bit immediate (denoted in the schematic figure by q).
Rd/Rr specifies the destination or source register

# Program memory (update the PC)
## Direct program memory addressing
![[Pasted image 20240323124836.png]]
Program execution continues at the address immediate in the instruction words

### Example JMP
Jump to an address
$$jmp \; marker$$

## Relative program memory addressing
![[Pasted image 20240323125129.png]]

Program execution continues at address $PC + k + 1$
The relative address k is from $-2048$ to $2047$.

### Example RJMP
Jump to an address within $PC-2K+1$ and $PC+2K$