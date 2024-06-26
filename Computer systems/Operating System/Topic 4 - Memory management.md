# OS Memory Management
- Keeps track of what memory is in use and what memory is free
- Allocates(and deallocates) free memory to processes when needed
- Deciding which processes (or part of processes) and data to move in and out of memory
	- Transfer between RAM and disk
# Memory sharing
As a result of CPU scheduling, we can improve:
- The utilisation of the CPU
- The speed of the computer's response to its users

To realise this increase in performance, however we must be able to keep several processes in memory at once

# Types of memory
- Cache memory/ CPU cache (L1,L2, etc)
- Main memory (volatile e.g., RAM)
- Storage memory (non-volatile SSD, HDD)
- Virtual memory

The cache and main memory are referred to as **primary storage**
The cache primarily supports, and is managed by the CPU
It is invisible to the OS
It uses the same memory management approaches as main memory

# Basic hardware
Each process has a separate memory space
A pair of **base** and **limit registers** define the local address space
CPU must check every memory access generated in user mode to be sure it is between base and limit for that user

![[Pasted image 20240301162422.png]]

## Hardware address protection
Protection of memory required to ensure correct operation
Separate per-process, memory space protects the processes from each other

![[Pasted image 20240301162427.png]]

## Logical/Physical addressing
Memory is made up of many memory cells.

A memory cell is an electronic circuit that stores one bit $(0, 1)$ of information.
The electro-mechanics is purely whether the circuit has a voltage higher than a pre-determined arbitrary threshold $(1)$, or not $(0)$.

The concept of a logical address space that is bound to a separate **physical address space** is central to proper memory management
- **Logical address** – generated by the CPU
	- also referred to as virtual address
- **Physical address** – address seen by the memory unit 
 
A user (application) program deals with logical addresses; it never knows the real physical addresses

# Memory Management Unit (MMU)
Hardware device that at run time maps virtual to physical address

Consider a simple scheme where the value in the relocation register is added to every address generated by a user process at the time it is sent to memory

Base register now called relocation register
![[Pasted image 20240227142321.png]]

## Memory partitioning
The main memory is usually split into two partitions:
1. Kernel processes
2. User processes

Each partition is contained in a single contiguous section of memory

## Memory protection
Reallocation registers used to protect user processes from each other, and form changing OS code and data

- Reallocation register contains value of smallest physical address
- Limit register contains range of logical addresses
	- Each logical address must be less than the limit register
- MMU maps logical address *dynamically*

![[Pasted image 20240301162446.png]]

### Contiguous allocation
If reading memory, contiguous memory can be read in sequence and is read faster

To achieve this an effective memory allocation strategy is required based on:
- **Hole**
	- Block of available memory
- Holes of various sizes are scattered throughout memory
- When a process arrives, it is allocated memory from a hole large enough to accommodate it

The OS also needs to maintain information about each partition and:
1. Its allocated holes
2. Its free holes

![[Pasted image 20240227142836.png]]

#### Memory hole allocation
Some strategies involve:
1. First-fit
	- Allocates the first hole that is big enough
1. Best-fit
	- Allocate the smallest hole that is big enough
		- Must traverse entire list, unless ordered by size
		- Produces the smallest leftover hole
1. Worst-fit
	- Allocate the largest hole
		- Must search entire list
		- Produces the largest leftover hole

First-fit and best-fit are usually better than worst-fit in terms of speed (first-fit) and storage (best-fit) utilization


# Fragmentation
**External fragmentation** is memory space that is able to satisfy a request but it is not contiguous

First fit analysis reveals that given $N$ blocks allocated, $0.5N$ blocks lost to fragmentation
$\frac{1}{3}$ may be unusable $\rightarrow$ 50-percent rule

Reduce external fragmentation by **compaction**
 - Shuffle memory contents to place all free memory together in one large block

# Paging
Physical address space of a process can be non-contiguous; process is allocated physical memory whenever the latter is available
- Avoids external fragmentation
- Avoids problem of varying sized memory chunks

Physical memory is divided into fixed-sized blocks called **frames**
Typically the size is a power of $2$ between $512$ and $8192$ bytes

Logical memory is divided into blocks of the same size called **pages**

To run a program of size $n$ pages, we need to find $n$ free frames and load the program. This is **paging**

A **page table** is set up to help manage the mapping of logical to physical addresses, using an address translation
- Still have internal fragmentation

## Address translation scheme
The logical memory address generated by the CPU is divided into:
1. **Page number $(p)$:**  
	- Index into a page table which contains base address of each page in physical memory.
2. **Page offset $(d)$:**
	- combined with base address to define the physical memory address that is sent to the memory unit.

![[Pasted image 20240227144911.png]]

## Paging hardware
1. Extract the page number $p$ and use it as an index into the page table
2. Extract the corresponding frame number $f$ from the page table
3. Replace the page number $p$ in the logical address with the frame number $f$

![[Pasted image 20240227145030.png]]

## Paging model

![[Pasted image 20240227145048.png]]

## Free frames

![[Pasted image 20240227145341.png]]

## Implementation of page table
The hardware implementation of the page table can be done in several ways
The page table is kept in main memory, and a page-table base register (PTBR) points to the page table
In this schema every data/instruction access requires two memory accesses: One for the page table and one for the data/instruction

The two memory access problem can be solved by the use of special fast-lookup hardware cache called associative memory or translation look-aside buffers (TLBs)

### Translation look-aside buffer (TLB)
![[TLB.png]]

When a logical address is generated by the CPU, the MMU first checks if its page number is present in the TLB
- If the page number is found, its frame number is immediately available and is used to access memory
- If the page number is not in the TLB (TLB miss), memory reference to the page table must be made
	- Frame number is obtained, we can use it to access memory
	- Add the page number and frame number to the TLB, so that they will be found quickly on the next reference
- If the TLB is already full of entries, existing entry must be selected for replacement

### Effective Access Time (EAT)
$Hit \; ratio = \alpha$
- Hit ratio - Percentage of times that a page number is found in the associate registers
- Ratio related to number of associate registers

$$ EAT = (TLB \; hit-ratio \; \times \; Memory \; access \; time ) + ((1-TLB \; hit-ratio) \times (2\times memory \; access \; time) $$

It is $2\times memory \; access \; time$ for a TLB miss as it two memory accesses are involved in a TLB miss (TLB access, page table access)
#### Example
Consider $\alpha = 80 \%, \; 10ns$ for memory access, $10ns$ for page table search
$$EAT = 0.8 \times 10 + 0.2 \times 20 =12ns$$

## Protection
Memory protection implemented by associating protection bit with each frame

A **valid-invalid bit** is attached to each entry in the page table
- **Valid** indicates that the associated page is in the process's logical address space. and thus a legal page
- **invalid** indicates that the page is not in the process' logical address space

### Valid (v) or invalid (i) Bit in a page table
![[V or i Bit.png]]

## Types of page table
1. Hierarchical paging

![[Pasted image 20240301162244.png]]

2. Hashed page table

![[Pasted image 20240301162309.png]]

3. Inverted page table

![[Pasted image 20240301162322.png]]

# Virtual memory
Virtual memory is the capability of the OS that enables programs to address more memory locations than are actually provided in main memory

Helps remove much of the burden of memory management from the programmers

- The **logical** address space is much larger than the **physical** address space
- Pages are swapped (paged) in and out of memory
- The physical address space is shared by several processes
- Only part of the process needs to be in the physical address space for execution
- A free frame list of the physical address space is maintained by the OS

## Virtual address space
Logical view of how process is stored in memory
Each process views the address space as a contiguous block of memory holding the objects it needs to execute
- Code (read-only)
- Data (read and write)
- Heap
	- The address space in memory that is used to hold data produced during execution of a process. This space will expand and contract during execution
- Stack
	- The address space that is used to hold instructions and data known at the time of the procedure call. The contents of the stack grow as the process issues nested procedure calls and shrinks as the called procedures return

![[Pasted image 20240301162732.png]]

## Demand paging
Bring a page into memory only when it is required by the process during its execution
- Reduces
	- Number of pages to be transferred
	- Number of frames allocated to a process
- Increases
	- Overall response time for a collection of processes
	- Number of processes executing

### A process' page table
When reference is made to a page's address
- Invalid reference $\rightarrow$ abort
- Not-in-memory $\rightarrow$ bring to memory

A valid/invalid bit is associated with each process' page table entry to indicate if the page is already in memory
- $1 \rightarrow$ in-memory
- $0 \rightarrow$ not-in-memory

Address translation
- When valid/invalid bit in page table entry $0 \rightarrow$ page fault trap

Initially the valid/invalid bit is set to $0$ on all entries

![[PageTableWhenSomePagesAreNotInMainMemory.png]]

#### Handling page fault traps
A process requests access to an address within a page:

Check the validity of the process’s access to that address
If an invalid request
- terminate process
- clear all previously allocated main memory
- throw error message “invalid memory access”

Else if a valid request
- If page allocated a frame in main memory; break
- Else if page fault trap
	- identify a free frame from the free frame list
	- read the page into the identified frame
	- update the process’s page table
	- restart the instruction interrupted by the page fault trap (break)

![[StepsInHandlingaPageFault.png]]

### Performance of Demand paging
Page fault Rate $0 \leq p \leq 1$
- If $p=0$ no page fault
- If $p=1$ every reference is a fault

$$EAT=(1-p)\times memory \; access + p \; \times \; (page \; fault \; overhead \; + \; swap \; page \; out \; + \; swap \; page \; in$$

Page fault overhead includes
- Context switching when relinquishing the CPU
- Time waiting in the paging device queue
- Time waiting back in the ready queue
- Context switching when regaining the ready queue

#### No free frame?
This occurs when all main memory frames available to a process are currently allocated

##### Page replacement
Find some page in memory, but not really in use, and swap it out
- Page replacement algorithms to decide the page
- We want to minimise number of page faults

###### Basic page replacement
1. Find the location of the desired page on the disk, either in swap space or in the file system.
2. Find a free frame:
    1. If there is a free frame, use it.
    2. If there is no free frame, use a page-replacement algorithm to select an existing frame to be replaced, known as the _**victim frame**_.
    3. Write the victim frame to disk. Change all related page tables to indicate that this page is no longer in memory.
3. Read in the desired page and store it in the frame. Adjust all related page and frame tables to indicate the change.
4. Restart the process that was waiting for this page.

![[BasicPageReplacement.png]]

##### Evaluating Replacement algorithms
Run each algorithm on a particular string of memory references (reference string).

- Compute the number of page faults per algorithm on that string.
- Compare the number of page faults: We are aiming for the lowest possible number of page faults given the reference string.

## First in First out (FIFO) algorithm
Associated with each page the time it was brought into memory

The victim page is the oldest page

### Example
Reference string: 7,0,1,2,0,3,0,4,2,3,0,3,0,3,2,1,2,0,1,7,0,1
3 frames (3 pages can be in memory at a time per process)

![[FIFO example.png]]

## Belady's Anomaly
For some page fault algorithms, the page fault rate may increase as the number of allocated frames increases

FIFO suffers from Belady's anomaly.

## Optimal Algorithm
Replace the page that will not be needed for longest period of time

This algorithm will always have the fewest page faults when compared with any other algorithm

Used to demonstrate how close to the ideal any other algorithm has progressed

Is impossible to implement as don't know what is going to come

### Example
Reference string: 7,0,1,2,0,3,0,4,2,3,0,3,0,3,2,1,2,0,1,7,0,1
3 frames (3 pages can be in memory at a time per process)
![[Optimal Page Replacement Algorithm.png]]

## Least recently used (LRU)
Associate with each page the time of its last use

Victim page is the page that has not been used for the longest time

LRU belongs to a class of page replacement algorithms known as **stack algorithms.**

Stack or counter algorithms can never exhibit **Belady's anomaly**
- A set of pages in memory of $n$ frames is always a subset of the set of pages that would be in memory with $n+1$ frames

### Example
Reference string: 7,0,1,2,0,3,0,4,2,3,0,3,0,3,2,1,2,0,1,7,0,1
3 frames (3 pages can be in memory at a time per process)
![[LRU page-replacement algorithm.png]]
### Implementations
#### Counter implementation
- Every page entry has a counter
- Every time a page is referenced, record the time
- When a page needs to be changed, look at the counters to determine which are to change

**Stack implementation:** Keep a stack of page numbers in a double ink form:
- Page referenced
	- Move it to the top (requires pointers to be altered)
- No search for the replacement: the tail pointer points to the bottom of the stack, which is the LRU page

## Counting-based algorithms
Keep a counter of the number of references that have been made to each page
- Not common
Lease frequently used (LFU) Algorithm: based on the argument that the page with the smallest count was probably just brought in and has yet to be used

## Allocation of frames
- Global replacement
	- Select a replacement frame from the set of all frames; one process can take a frame from another
- Local replacement
	- Select from only the process' own set of allocated frames
- Fixed allocation
	- Equal allocation
	- Proportional allocation: Allocate according to size of process
- Priority allocation
	- If process $pi$ generates a page fault, select for replacement a frame from a process with lower priority number

## Thrashing
**Thrashing** occurs when a process is spending more time paging then doing actual work
If a process does not have enough pages, the page-fault rate is very high
- Page fault to get page
- Replace existing frame
- But quickly needs replaced frame back
- This leads to:
	- Low CPU utilization
	- Operating system thinking that it needs to increase the degree of multiprogramming
	- Another process added to the system

## Prepaging
**Prepaging:** Page into memory at one time all the pages that will be needed
In a system using the working set model,
- We keep with each process a list of pages within its working set model
- If a process is suspended we remember working set for that process
- When the process resumes we automatically bring back into memory its entire working set before restarting the process

Prepaging is a means to prevent thrashing. However, we must ensure that the cost of prepaging is less than the cost of servicing the page faults.

## Page-fault Frequency Scheme
A **page-fault frequency scheme** is an alternative approach to prevent thrashing
Scheme: Firstly establish an "acceptable" page-fault rate. Then:
- If the actual rate is too low, i.e., the process has got too many frames
	- The process loses frames
- If the actual rate too high, i.e., the process has not got enough frames
	- The process gains frames



