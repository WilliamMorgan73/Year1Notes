# CISC model
Dozens of formats in the full set of instructions. The size of instructions can vary

![[Pasted image 20240323164230.png]]

## CISC architecture
Complex instruction set computers (CISC)
- A large number of specialised instructions
- A wide variety of addressing modes
- Instruction length varies
- Comparatively few general-purpose registers

# RISC architecture
**Reduced instruction set computers (RISC)**
Limited and simplified instruction set - but instructions are executed more efficiently

Register oriented instructions - limited memory access. Essentially can only load and store to memory, most operations done on registers.

Fixed length and format of instructions - enables independent fetching and decoding of instructions.

Limited addressing modes - direct or register indirect.

A large bank of registers - intermediate results can be stored in registers to avoid load/store operations.

# CISC vs RISC
Idea: simplified instructions can be executed more quickly than complex instructions.

Even the simple instructions in CISCs are slowed down by hardware complexity in the instruction decoder required to decode the complex instruction formats.

![[Pasted image 20240323164535.png]]

# Pipelining
## Fetch-execute cycle
**Fetch**
Find and decode instruction, load from memory into register and signal ALU.
**Execute**
Performs the operation that the instruction prescribes.
Move / process data.

## Separate fetch/execute units
One instruction processed at a time
The next (few) can be fetched

The decode unit identifies the opcode and instruction format and hence the addresses of the operands

This info is passed to the Execution unit which reads/writes the operands and liaises with the ALU

## Pipelining
![[Pasted image 20240323164928.png]]

Notice that here Instruction 3 is delayed by waiting for the result of step 3 in Instruction 2

Assembly-line technique to allow overlapping between fetch-execute cycles of sequences of instructions.

### Scalar processing
An individual instruction takes the same amount of time as before.
Average instruction throughput is approximately equal to the clock speed of the CPU

### Problems from stalling and branching
Waiting for prior results to become available.
At a branch, we don’t know what the next instruction is.

#### Branch problems solutions
**Separate pipelines for both possibilities:**
Work on both outcomes until the branch is resolved.

**Probabilistic approach:**
Predict the branch outcome based on previous visits or programmer hint.

**Requiring the following instruction to not be dependent on the branch:**
Can also be used to avoid stalling: following a write to memory do not allow read from that location for a few steps.

**Instruction Reordering:**
Analyse instructions coming up and do the ones that do not depend on the current pipeline first.

### Multiple execution units
Include specialist units for different types of instruction execution, e.g. Load/Store unit

Have several units for the most common instructions.

Each unit can have a pipeline, and if they are all filled, the overall processor can execute more than one instruction per clock cycle. This is called superscalar processing.

## Superscalar processing
![[Pasted image 20240323165325.png]]

### Complications
- Instructions may complete in the wrong order.
- Dependencies on prior results may be lost.
- Branch instructions must be resolved correctly.
- Conflicts for CPU resources, e.g. registers, arise

