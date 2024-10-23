# Basic overview
Central processing unit (CPU)
- Control unit (CU)
	- responsible for directing the flow of instructions and data
- Arithmetic logic unit (ALU)
	- Responsible for performing operations on the data

Main memory

I/O devices

Communications between components through **buses**
- Bundles of tiny wires that carry data between components

# Harvard architecture
Two separate memory spaces for program instructions and data
Two separate buses

# Back to Von Neumann
## Registers
5 registers
1. Accumulator (ACC)
2. Program counter (PC)
3. Instruction register (IR)
4. Memory address register (MAR)
5. Memory data register (MDR)

Registers hold a value temporarily for:
- Storage
- Manipulation
- Calculation

Manipulated directly by the control unit
Their size can vary from $1$ to $128$ bits

### Accumulator
General purpose registers used for:
- Holding data.
- Holding interim and final results of arithmetic operations.
- Holding data waiting to be transferred between different memory locations.
- Holding data waiting to be transferred between I/O and main memory.

### Program counter
Holds the address of the next instruction to be executed

### Instruction register
Holds the actual instruction being executed

### Flags
Flags are 1-bit registers keeping track of special conditions such as:
- Arithmetic carry
- Overflows
- Power failures
- Internal computational errors

Grouped together in one or more status registers (SR)

### Memory address register
Holds the address of a memory location to be accessed
Connects to the memory with a one-way bus

### Memory data register
Holds the value that is being stored to or retrieved from the memory location currently addressed by the MAR
Connects to the memory with a two-way bus. Also known as the memory buffer register (MBR)

## Buses
Physical connection that makes it possible to transfer data from one location in the system to another

A bus is a group of electrical conductors used to carry signals
Four general categories of buses:
1. Data
2. Address
3. Control
4. Power

Buses are used to:
- Transfer data between different points on the CPU.
- Transfer data between the CPU and main memory.
- Transfer data between computer peripherals and the CPU.

### Other buses
Point-to-point buses carries the signal from a specific source to a specific destination.

Broadcast buses carry signals to many different destinations.

Bus Interface Bridges allow communications between the different buses:
- External bus
- PCI: Peripheral Control Interface bus
- USB: Universal Serial Bus