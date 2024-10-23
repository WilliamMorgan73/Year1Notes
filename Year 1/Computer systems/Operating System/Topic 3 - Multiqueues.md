# Multilevel Queue
The **ready** queue is partitioned into separate queues:
- e.g., foreground (interactive) and background (batch)

Each queue has its own scheduling algorithm
- e.g., foreground in Round robin and background in First come first serve

Scheduling must be undertaken between the queues
- Fixed priority scheduling
	- e.g., Serve all from foreground then form background
- Time slice
	- Each queue gets a certain amount of CPU time which it can schedule amongst its processes
	- e.g., $80\%$ foreground in Round robin, $20\%$ to background in First come first serve

## Multilevel queue scheduling
![[Pasted image 20240228111541.png]]
Separate queue for each priority

**Problem:** provides differentiation but not flexible, since a process remains in the same queue regardless of adapting requirements

## Multilevel Feedback queue
**Feedback queues** are an adaption of multilevel queue scheduling.
A process can move between the various queues; aging can be implemented this way

Multilevel-feedback-queue scheduler defined by the following parameters:
- number of queues
- scheduling algorithms for each queue
- method used to determine when to upgrade/demote a process
- method used to determine which queue a process will enter when that process needs service 
### Example
The scheduler first executes all processes in $Q_0$
- $Q_0$ - RR with time quantum $8$ milliseconds
- $Q_1$ - RR time quantum $16$ milliseconds
- $Q_2$ - FCFS

Scheduling
- When a new process enters queue $Q_0$
	- If it gains CPU job, job receives $8$ milliseconds
	- If it does not finish in $8$ milliseconds, job is moved to tail of queue $Q_1$
- At $Q_1$ process receives $16$ additional milliseconds
	- If it still does not complete, it is pre-empted and move to queue $Q_2$
- To prevent starvation, a process that waits too long in a lower-priority queue may gradually be moved to a higher-priority queue

# Algorithm evaluation
## Deterministic modelling:
Take a predetermined workload (case) and analyse the performance of each algorithm

## Queuing Models:
Queuing networks analysis

$$Little's \; formula, \; n=\lambda \times W$$
$n=Average \; long-term \; queue \; length$
$W = Average \; waiting \; time \; in \; queue$
$\lambda = Average \; rate \; of \; new \; processes \; in \; the \; queue$

E.g., if $7$ processes arrive every seconds (on average) and normally $14$ processes in the queue, then the average waiting time per process is $2$ seconds

