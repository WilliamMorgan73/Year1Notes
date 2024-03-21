# Multiprogramming
Aim is to maximize CPU utilization
Several processes kept in memory concurrently

When one process is **waiting**, the OS executes (to **running**) one of the processes sitting in the **ready** queue

## CPU scheduling
Provides a fair and efficient sharing of system, in this case, CPU resources

### Schedulers
An OS operates three types of scheduler:
1. Long-term (Job scheduler)
	- Selects which processes should be brought into the ready queue
2. Medium-term
	- Part of swapping and in-charge of handling the swapped out-processes
3. Short-term (CPU scheduler)
	- Selects the process to be executed next and allocated to the CPU
		- E.g., switch from ready to running state, or from running to ready state, or from waiting to ready

### Dispatcher
Module that gives control of the CPU to the process selected by the CPU scheduler
Functions involved are:
- **Switching context**
	- Context-switch time is an overhead;: the system undertakes no user processing while switching
- Switching to user mode
- Jumping to proper location in the user program to restart that program


Dispatch latency - Time it takes for the dispatch to stop one process and start another running



![[Pasted image 20240220141423.png]]

MAKE AS GRAPH

### Scheduling criteria
- **CPU utilization:**
	- Keep the CPU busy
- **Throughput:**
	- Number of processes that complete their execution per unit of time
- **Turnaround time:**
	- Amount of time to execute a particular process (waiting + execute + I/O)
- **Waiting time:**
	- Total amount of time a process has been waiting in the ready queue
- **Response time:**
	- Amount of time it takes from when a request was submitted until the first response (access to the CPU)
	- Not the time taken to complete the process

### Optimization criteria
- Max CPU utilization
- Max Throughput
- Min Turnaround time
- Min Waiting time
- Min Response time

# Scheduling algorithms
There are a number of different algorithms including:
- First Come, First Served (FCFS)
- Shortest Job First (SJF)
- Shortest Remaining Time First (SRTF)
- Priority (with or without pre-empting)
- Priority (with or without ageing)
- Round-Robin (RR)
- Multilevel queue / feedback queue

## First Come, First Served (FCFS)
The first process to request the CPU is allocated the CPU until it is completed
### Example 1
Suppose that the process arrive in the order: $P_1,P_2,P_3$ (all at time $0$)

Burst time
$$P_1 = 24$$
$$P_2 = 3$$
$$P_3 = 3$$
The Gantt Chart for the schedule is:
![[Pasted image 20240220142144.png]]
$$Waiting \; time \; for \; P_1 =0; P_2 =24; P_3=27$$
$$Average \; waiting \; time = \frac{0+24+27}{3}=17$$

### Example 2
Suppose that the process arrive in the order: $P_2,P_3,P_1$ (all at time $0$)

Burst time
$$P_1 = 24$$
$$P_2 = 3$$
$$P_3 = 3$$
The Gantt Chart for the schedule is:
![[Pasted image 20240220142409.png]]
$$Waiting \; time \; for \; P_1 =6; P_2 =0; P_3=3$$
$$Average \; waiting \; time = \frac{0+6+3}{3}=3$$
Much better than the previous case
Convoy Effect short process behind long process

### Overview
- The average waiting time may or may not be lengthy!
- A simple algorithm to implement.
- May result in a ‘convoy’ effect, for example short processes waiting on a long process to finish

## Shortest-Job-First (SJF)
Associate with each process, the length of its next CPU burst

Use these lengths to schedule the process with the shortest time
- If two processes have the same length then FCFS

Non pre-emptive
- Once the CPU is given to the process it cannot be pre-empted until the process has completed its CPU burst
### Example

Burst time
$$P_1 = 7$$
$$P_2 = 4$$
$$P_3 = 1$$
$$P_4 = 4$$

Arrival time
$$P_1 = 0.0$$
$$P_2 = 2.0$$
$$P_3 = 4.0$$
$$P_4 = 5.0$$
The Gantt Chart for the schedule is:
![[Pasted image 20240220142956.png]]

$$Average \; waiting \; time = \frac{0+6+3+7}{4}=4$$
$$Average \; turnaround \; time = \frac{7+10+4+11}{4}=8$$

### Overview
SJF is optimal - gives minimum average waiting time for a given set of processes
- The difficulty is knowing the length of the next CPU request
- Could ask the user

Jobs may arrive which are shorter than the longer ones, and therefore the longer ones will never be executed (Starved)

## Shortest Remaining Time First (SRTF)
If a new process arrives in the ready queue with a CPU burst length less than the remaining time of executing process
- Then pre-empt the running process and run the process with the shorter CPU burst length

It can be viewed as a pre-emptive version of SJF

### Example
Burst time
$$P_1 = 7$$
$$P_2 = 4$$
$$P_3 = 1$$
$$P_4 = 4$$

Arrival time
$$P_1 = 0.0$$
$$P_2 = 2.0$$
$$P_3 = 4.0$$
$$P_4 = 5.0$$

The Gantt Chart for the schedule is:
![[Pasted image 20240220143521.png]]

$$Average \; waiting \; time = \frac{9+1+0+2}{4}=3$$

$$Average \; turnaround \; time = \frac{16+5+1+6}{4}=7$$

### Overview

Simple algorithm to create
Gives priority the short processes

## Round Robin (RR)
Each process gets a small unit of CPU time:
- a time quantum or time slice usually $q = 10 \; to \; 100$ milliseconds.

After this time has elapsed, the process is pre-empted and added to the end of the ready queue. 

If there are $n$ processes in the ready queue and the time quantum is $q$, then each process gets $\frac{1}{n}$ of the CPU time in chunks of at most $q$ time units at once

### Example

$Time \; quantum = 4$
$Arrival \; time = 0$

Burst time
$$P_1 = 24$$
$$P_2 = 3$$
$$P_3 = 3$$

The Gantt Chart for the schedule is:
![[Pasted image 20240220144152.png]]

$$Average \; waiting \; time = \frac{6+4+7}{3}=5.66$$

$$Average \; turnaround \; time = \frac{30+7+10}{3}=15.66$$

### Time quantum vs context switching
Performance of the RR algorithm depends heavily on the size of the time quantum
- If the time quantum is extremely large, the RR policy is the same as the FCFS policy
- If the time quantum is extremely small, the RR approach can result in large number of context switches

Turnaround time also depends on the size of the time quantum

Time quantum should be large compared with the context-switch time, it should not be too large

Rule of thumb - $80\%$ of the CPU bursts should be $<$ the time quantum

## Priority Scheduling
The algorithm associates a priority number (integer) for each process

The CPU is allocated by the dispatcher to the process with the highest priority (smallest integer = highest priority or otherwise)

Priority based CPU scheduling can be either:
- Pre-emptive
- Non pre-emptive

### Example
Arrival time of all process $=0$

Priority
$$P_1 = 3$$
$$P_2 = 1$$
$$P_3 = 4$$
$$P_4 = 5$$
$$P_5 = 2$$

Burst time
$$P_1 = 10$$
$$P_2 = 1$$
$$P_3 = 2$$
$$P_4 = 1$$
$$P_5 = 5$$

The Gantt Chart for the schedule is:
![[Pasted image 20240220145003.png]]
$$Average \; waiting \; time = \frac{6+0+16+18+1}{5}=8.2$$

### Starvation (indefinite blocking)
The low priority process may never execute as more processes may arrive with a higher priority

**Solution**
1. Ageing
	- As time progresses, increase priority of the process
2. Combine RR with priority
	- Executes the highest priority process and runs processes with same priority using round robin

