Microprocessor without Interlocked Pipeline Stages:

# Registers

| Name      | Number | Use                     |
| --------- | ------ | ----------------------- |
| $0        | 0      | The constant value 0    |
| $at       | 1      | Assembler temporary     |
| $v0 - $v1 | 2-3    | Function return values  |
| $a0 - $a3 | 4-7    | function arguments      |
| $t0 - $t7 | 8-15   | temporary variables     |
| $s0 - $s7 | 16-23  | saved variables         |
| $t8 - $t9 | 24-25  | temporary variables     |
| $k0 - $k1 | 26-27  | OS temporaries          |
| $gp       | 28     | global pointer          |
| $sp       | 29     | stack pointer           |
| $fp       | 30     | frame pointer           |
| $ra       | 31     | function return address |

# MIPS assembly
## Example 1
$a=b+c$

$$
add \; $s0, \; $s1, \; $s2 
$$
$\$s0=a$
$\$s1=b$
$\$s2=c$

## Example 2
$a=b+c-d$

$$
sub \; $t0, \; $s2, \; $s3
$$
$$
add \; $s0, \; $s1, \; $t0 
$$
$\$s0=a$
$\$s1=b$
$\$s2=c$
$\$s3=d$

# Instruction types
Three types of instructions
1. R-type
	- Register operands
2. I-type
	- Immediate operand
3. J-type
	- For jumping

## R-type instruction format

![[Pasted image 20240321154700.png]]

Three registers
- $rs,rt$ source registers
- $rd$ destination register

The other fields
- Op - Opcode
	- Always $0$ for R-type
- Funct - The function
	- Essentially the second part of the operand
	- Tells the computer what R-type instruction it is
- Shamt - Shift amount
	- Shift amount for shift instructions
	- Otherwise it is $0$

### Example 1
The assembly code for adding the values in registers $17$ and $18$ and putting the answer in register $16$
$$
add \; $s0, \; $s1, \; $s2 
$$

![[Pasted image 20240321154926.png]]

### Example 2
The assembly code for subtracting the value in register $13$ from the value in register $11$ and putting the answer in register $8$
$$
sub \; $t0, \; $t3, \; $t5
$$

![[Pasted image 20240321155845.png]]

## I-type instruction format

![[Pasted image 20240321160107.png]]

Three operands:
- $rs,rt$ - Register operands
- $imm$ - 16-bit immediate written in two's complement
- $rs$ and $imm$ are used as source operands. $rt$ is used as source in some instructions and as destination in some other

The other filed
- $op$ - opcode
	- The instruction is completely determined by the opcode
### Example 1
The assembly code for adding the number $5$ to the value of register $17$ and putting the answer in register $16$
$$addi \; $s0, \; $s1, \; 5$$

![[Pasted image 20240321184953.png]]

### Example 2
The assembly code for loading the number $5$ to the register $16$
$$li \; $s0, \; 5$$

![[Pasted image 20240321185058.png]]

## J-type instruction format

![[Pasted image 20240321185208.png]]

- $addr$
	- 26-bit address operand
- $op$
	- The opcode

# MIPS memory map
Word: $32$-bits
Byte: $8$-bits

MIPS uses $32$-bit memory addresses and memory is **byte addressable**

![[Pasted image 20240321185413.png]]

![[Pasted image 20240321185607.png]]

With $32$-bit addresses, the MIPS address space spans
$$2^{32} \; bytes =4GB$$
Word addresses are divisible by $4$ and range from $0$ to $0\times FFFFFFFC$
$0\times$ means hex

Divides into four parts:
1. Text segment
2. Global data segment
3. Dynamic data segment
4. Reserved segments

## The text segment
Stores the machine language program
It can store almost $256MB$ of code

The four most significant bits of any word address in text segment are all $0$
Thus the $26$ bits of the $addr$ field of the $j$ instruction suffice to specify the address of any instruction stored in the text segment

## The global data segment
Stores global variable, which can be seen by all functions in a program
It can store $64KB$ of data

Global variables are accessed using the pointer $\$gp$

By convention, we initialise $\$gp$ at the middle of the global data segment at value $0\times 10008000.$ The value of $\$gp$ stays constant throughout execution, and global variables are addressed as offsets from $0\times 10008000$

## The dynamic data segment 
Stores data that is dynamically allocated and deallocated throughout the execution of the program
Spans almost $2GB$ of the address space

Data in this segment are stored in a stack and a heap

## The reserved segments
Used by the OS and cannot directly be used by the program

# MIPS addressing modes
## Reading and writing operands
### Register Only
Uses registers for all source and destination operands.
R-type instructions use Register Only addressing

### Immediate
Uses registers and a 16-bit immediate as operands. Some of the I-type instructions use Immediate addressing (depending on how the 16-bit immediate is used).

### Base Addressing
Used in **memory access** instructions
Implemented by $I-type$ instructions
The address of the memory operand is computed by adding the base address in register $rs$ to a $16-bit$ offset stored in $imm$

The instructions:
- $lw$
	- Load word
- $lb$
	- Load byte
- $sw$
	- Store word
- $sb$
	- Store byte

#### Example 1

![[Pasted image 20240321191945.png]]
$lw \;  \$s0, \; 0\left( \$0 \right)$
Read data word $0 \; \left( 0\times ABCDEF78 \right)$ and load it into $\$s0$

$lw \;  \$s0, \; 8\left( \$0 \right)$
Read data word $2 \; \left( 0\times 01EE2842 \right)$ and load it into $\$s1$

#### Example 2
Assume that the register $\$t1$ stores the word $0\times 004000000$
How would you describe the content of register $\$t0$ after the instruction $lw \; \$t0, \; 8\left(\$t1\right)$?

**Answer**
The word stored in $0\times 004000008$
## Writing the Program Counter
### PC-Relative addressing
Branching instructions can use PC-relative addressing to specify the new value of the PC (Program Counter) if the branch is taken.

To calculate the imm, we take the PC value immediately after the branching instruction,  we subtract it from the Branch Target Address (BTA), and divide by 4.

$$bne \; \$1, \; \$t0, \; loop$$

![[Pasted image 20240323114644.png]]
CCURRENTLY HERE
### Pseudo-direct addressing
MIPS does not support direct addressing, which would need 32-bit for the address and 6-bits for the opcode, while the instruction has 32 bits only

MIPS uses pseudo-direct addressing in J-Type instructions,
calculating the new value of the PC, called Jump Target Address (JTA), as follows: 

The two least significant bits are left to 0 
The next 26 bits are taken from the addr field of the J-Type instruction.
The four most significant bits are again left to 0 

![[Pasted image 20240323114804.png]]

$$j \; sum$$
![[Pasted image 20240323114846.png]]

# Functions
## Call and return
![[Pasted image 20240323120457.png]]

The function main calls the function simple using the jal instruction.

jal simple (jump and link) jumps to the address $0\times 00401020$ (as j would do) but also stores in register $ra the address where the program should return after simple has been executed (here $0\times 00400204$). jr $\$ra$ (jump register) jumps to the address stored in a register (here $\$ra$). Notice, that jr is an R-type not a J-type instruction.

## Arguments and return value

$move \; \$s0,\; \$v0$ is another pseudo-instruction like li. It copies the value of a register into another register.

## Loops
![[Pasted image 20240323120849.png]]
We use beq to break from the loop

## Input/Output
![[Pasted image 20240323121353.png]]

The type of syscall service is specified by what is stored in $\$v0$
Code $5$ corresponds to integer from keyboard

### Examples of syscall services

| Service       | Syscall code | Arguments      | Result                 |
| ------------- | ------------ | -------------- | ---------------------- |
| print integer | $1$          | $\$a0=integer$ | -                      |
| print string  | $4$          | $\$a0=string$  | -                      |
| read integer  | $5$          | -              | Integer $(in \; \$v0)$ |
| exit          | $10$         | -              | -                      |

# Compiling, assembling, and loading
![[Pasted image 20240323121717.png]]


The compiler translates the high-level code into assembly language.

The assembler turns the assembly code into machine language code (object file).

The linker combines the object file with other machine language code (e.g. from already compiled and assembled libraries).

The loader puts the executable into the memory.