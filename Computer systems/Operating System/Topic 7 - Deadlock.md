# Deadlock
A set of processes is deadlocked if each process in the set is waiting for an event that only another process in the set can cause

# System model
System consists of resources
Resource types $R_1 , R_2 , ..., R_m$
- CPU cycles, memory space. I/O devices
Each resource type $R_i$ has $W_i$ instances
Each process utilizes a resource as follows
- Request
- Use
- Release
# Deadlock characterisation
## Mutual exclusion
Only one process at a time can use a resource

## Hold and wait
A process holding at least one resource is waiting to acquire additional resources held by other processes 

## No pre-emption
A resource can be released only voluntarily by the process holding it, after that process has complete its task

## Circular wait
There exists a set $\{P_0, P_1, ..., P_n\}$ of waiting processes such that $P_0$ is waiting for a resource that is held by $P_1$
$P_1is$ waiting for a resource that is held by $P_2$, etc
$P_{n-1}$ is waiting for a resource that is held by $P_n$ and $P_n$ is waiting for a resource held by $P_0$

If all four arises simultaneously, a deadlock can occur

# Resource-allocation graph
A set of vertices $V$ and a set of edges $E$

$V$ is partitioned into two types:
1. $P=\{P_1,P_2,...,P_n\}$, the set consisting of all the processes in the system
2. $R+\{R_1,R_2,...,R_n\}$, the set consisting of all resource types in the system

**Request edge** - Directed edge $P_i \rightarrow R_j$
**Assignment edge** - Directed edge $R_j \rightarrow P_i$

## Representation
### Process

![[Pasted image 20240308161618.png]]

### Resource Type with 4 instances

![[Pasted image 20240308161628.png]]

### $p_i$ requests instance of $R_j$

![[Pasted image 20240308161636.png]]

### $P_i$ is holding an instance of $R_j$

![[Pasted image 20240308161648.png]]

#### Example - RAG

![[Pasted image 20240308161938.png]]

#### Example - RAG with deadlock

![[Pasted image 20240308161954.png]]

#### Example - RAG with cycle but no deadlock

![[Pasted image 20240308164332.png]]

#### Basics
If a graph contains no cycles, there is no deadlock
If a graph contains a cycle:
- If only one instance per resource type then deadlock
- If several instances per resource type, possibility of deadlock

## Dealing with deadlocks
1. Ignore the problem altogether
2. Prevention
	- Negating one of the four necessary conditions
3. Avoidance
	- Careful resource allocation
4. (Detection and) Recovery

### Approach 1 - The ostrich algorithm
Pretend there is no problem
Reasonable if:
- Deadlocks occur  very rarely
- Cost of prevention is high

UNIX and Windows take this approach as:
- Resources are plentiful
- Deadlock over such resources rarely occur
- Deadlock typically handled by rebooting

Its a trade off between
- Convenience
- Correctness

### Approach 2 - Deadlock prevention
#### Mutual exclusion
Not required for sharable resources (e.g., read-only files); Must hold for non-sharable resources

#### Hold and wait
To ensure it never occurs, one must guarantee that whenever a process requests a resource, it does not hold any other resources.
- Require process to request and be allocated all its resources before it begins execution.
- Or allow process to request resources only when the process has none allocated to it
	- Low resource utilization; Starvation possible

#### No pre-emption
To ensure it does not hold
- If a process that is holding some resources requests another resource that cannot be immediately allocated to it, then all resources currently being held are released (pre-empted)
- Pre-empted resources are added to the list of resources for which the process is waiting
- Process will be restarted only when it can regain its old resources, as well as the new ones that it is requesting

#### Circular wait

One way to ensure it does not hold is to impose a total ordering of all resource types, and require that each process requests resources in an increasing order of enumeration

### Approach 3 - Deadlock avoidance
Requires that the system has some additional **a priori** information available
- Simplest and most useful mode requires that each process declare the **maximum number** of resources of each type that it may need
- The deadlock-avoidance algorithm dynamically examines the resource-allocation state to ensure that there can never be a circular-wait condition
- Resource-allocation state is defined by the number of available and allocated resources, and the maximum demands of the processes

## Safe state
When a process requests an available resource, system must decide if immediate allocation leaves the system in a safe state

System is in **safe state** if there exists a sequence $<P_1,P_2,...,P_n>$ of ALL the processes in the systems such that:

for each $P_i$, the resources that $P_i$ can still request can be satisfied by currently available resources + resources held by all the $P_j$, with $j < i$

That is:
- If $P_i$ resource needs are not immediately available available, then $P_i$ can wait until all $P_j$ have finished
- When $P_j$ is finished, $P_i$ can obtain needed resources, execute, return allocated resources, and terminate
- When $P_i$ terminates, $P_{i+1}$ can obtain its needed resources, and so on

## Example
Processes: $P_0$, $P_1$, and $P_2$
Resources: $12$

|       | Needs | Current | Requires |
| ----- | ----- | ------- | -------- |
| $P_0$ | $10$  | $5$     | $10-5=5$ |
| $P_1$ | $4$   | $2$     | $4-2=2$  |
| $P_2$ | $9$   | $2$     | $9-2=7$  |

Available start at $12-9=3$, we need to see what we can complete ($Requires \leq Available$), then complete $P_i$ then relinquish the resources used and add to available, then repeat.

At time $t_0$, the system is in a safe state. The sequence $<P_1,P_0,P_2>$ satisfies the safety condition
- A system can go from a safe state to an unsafe state.
	- Suppose that, at time $t_1$, processes $P_2$ requests one resource and is granted


If a system is in safe state
	$\implies$ no deadlocks
If a system is in unsafe state
	$\implies$ possibility of deadlock
Avoidance
	$\implies$ ensure that a system will never enter an unsafe state

![[Pasted image 20240312131920.png]]

# Avoidance algorithms
Single instance of a resource type
- Use a resource-allocation graph

Multiple instances of a resource type
- Use the banker's algorithm

## RAG scheme
- **Claim edge** $P_i \rightarrow R_j$ indicated that process $P_j$ may request resource $R_j$; represented by a dashed line
- Claim edge converts to request edge when a process requests a resource
- Request edge converted to an assignment edge when the resource is allocated to the process
- When a resource is released by a process, assignment edge reconverts to a claim edge

![[Pasted image 20240312132451.png]]

**Left side**

$P_1, P_2$ can request for $R_2$ in the future
$P_2$ requesting $R_1$
$R_1$ allocated to $P_1$

**Right side**

$P_12$ can request for $R_2$ in the future
$P_2$ requesting $R_1$
$R_1$ allocated to $P_1$
$R_2$ allocated to $P_2$

If allowing request would lead to **deadlock**, do not allow

## RAG algorithm
Suppose that the process $P_i$ requests a resource $R_j$
The request can be granted only if converting the request edge to an assignment edge does not result in the formation of a cycle in the resource allocation graph

# Banker's Algorithm
- Multiple instances 
- Each process must be a priori claim maximum use
- When a process requests a resource, it may have to wait
- When a process gets all its resources it must return them in a finite amount of time


$$let \; n= \#processes, \; and \; m=\#resources \; types$$
**Available:** Vector of length $m$. 
	If $available=k$, there are $k$ instances of resource type $R_j$ available
**Max**: $n\times m$ matrix
	If $Max=k$, then process $P_i$ may request at most $k$ instances of resource type $R_j$
**Allocation**: $n\times m$ matrix
	If $Allocation = k$ then $P_i$ is currently allocated $k$ instances of $R_j$
**Need**: $n \times m$
	If $Need=k$, then $P_i$ may need $k$ more instances of $R_j$ to complete its task
$$Need=Max-Allocation$$

## Example
Processes: $P_0, P_1$, and $P_2$
Resources: $A,B,$ and $C$

|       | Allocation    | Max           | Need          | Available     |
| ----- | ------------- | ------------- | ------------- | ------------- |
|       | $A \; B \; C$ | $A \; B \; C$ | $A \; B \; C$ | $A \; B \; C$ |
| $P_0$ | $1 \; 0 \; 2$ | $5 \; 2 \; 3$ | $4 \; 2 \; 1$ | $5 \; 3 \; 2$ |
| $P_1$ | $4 \; 2 \; 1$ | $4 \; 2 \; 0$ | $0 \; 0 \; 1$ |               |
| $P_2$ | $2 \; 3 \; 1$ | $5 \; 3 \; 3$ | $3 \; 0 \; 2$ |               |

Can do $P_0$ first and end up with $5+4 \; 3+2 \; 2+1 = 9 \; 5 \; 3$ available, and we can repeat to complete $P_1,P_2$
$<P_0,P_1,P_2>$

## Banker's safety algorithm
1. Let **work** and **finish** be vectors of length $m$ and $n$ respectively.
		Initialize:
$$Work=Available$$
$$Finish[i]=false \; for \; i=0,1,...,n-1$$
2. Find an $i$ such that both:
	1. $Finish[i]=false$
	2. $Need_i \leq Work$
	If no such $i$ exists, go to step $4$

3. $Work=Work + Allocation_i$
	$Finish[i]-true$
	Go to step $2$

4. If $Finish[i] == true \; \forall \; i$, then the system is in a safe state

## Banker's Resource-Request Algorithm
**Request** = Request vector for process $P_i$. If $Reqest_i[j]=k$ then $P_i$ wants $k$ instances of resource type $R_j$
1. If $Request_i \leq Need_i$ go to step $2$. Otherwise, raise error condition, since process has exceeded its maximum claim
2. If $Request \leq Available$, go to step $3$. Otherwise $P_i$ must wait, since resources are not available
3. Pretend to allocated requested resources to $P_i$ by modifying the state as follows

$$Available = Available-Request_i$$
$$Allocation=Allocation_i+Request_i$$
$$Need_i=Need_i-Request_i$$
	- If safe $\implies$ the resources are allocated to $P_i$
	- If unsafe $\implies P_i$ must wait, and the old resource-allocation sate is restored

# Approach 4 - Recovering from deadlock
## Process termination
Abort all deadlocked processes
Abort one process at a time until the deadlock cycle is eliminated
In which order should we choose to abort?
1. Priority of the process
2. How long process has computed, and how much longer to completion 
3. Resources the process has used
4. Resources process needs to complete
5. How many processes will need to be terminated 
6. Is process interactive or batch?

## Resource pre-emption
**Selecting a victim** - Minimise cost
**Rollback** - Return to some safe state, restart process for that state
**Starvation** - Same process may always be picked as victim, include number of rollbacks in cost factor