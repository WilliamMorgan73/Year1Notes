Lower bounds for sorting - Decision tree argument
Lower bounds for selection - Adversary argument

# Lower bounds for sorting
A decision tree is a **full binary tree** (every node either has zero or two children)
It represents comparisons between elements performed by particular algorithm run on particular (size of) input
Only **comparisons** are relevant, everything else is ignored

## Decision trees
**Internal nodes** are labelled $i : j$ for $1 \leq i , j \leq n$ meaning elements $i$ and $j$ are compared

**Downward-edges** are labelled $\leq$ or $>$, depending on the outcome of the comparisons

**Leaves** are labelled with some permutation of $\{1, ..., n\}$

A **branch** from root to leaf describes sequence of comparisons (nodes and edges) and ends in some resulting sequence (leaf)

We have at least $n!$ leaves - at least one for each outcome

### Example: SelectionSort
$3-element$ input
![[Decision tree selection sort.png]]

![[Decision tree selection sort 2.png]]

#### Lower bound for worst case
Length of longest path from root of decision tree to any leaf (height) represents worst case number of comparisons for given value of $n$

For any given $n$, lower bound on heights of **all** decision trees where each permutation appears as leaf is thus lower bound on running time of **any** comparison based sort algorithm

![[Lower bound diagram.png]]
#### Theorem
Any comparison-based sorting algorithm requires $\Omega (n \log n)$ comparisons in the worst case

##### Proof
- Sufficient to determine minimum height of a decision tree in which each permutation appears as leaf
- Consider decision tree of height $h$ with $\ell$ leaves corresponding to a comparison sort of $n$ elements
- Each of the $n!$ permutations of input appears as some leaf: $\ell \geq n!$
- Binary tree of height $h$ has at most $2^h$ leaves: $\ell \leq 2^h$
- Together: $n! \leq \ell \leq 2^h$ and therefore $n! \leq 2^h$
- Take $\log$: $h \geq \log (n!)$ = $\Omega (n \log n)$

# Lower bounds for selection
## Lower bounds via adversaries
### Adversary
- Is a second algorithm intercepting access to input
- Gives answers so that there’s always a consistent input
	- i.e. adversary can never be caught cheating
- ensures that original algorithm has **not enough info** to make a decision, for **as long as possible**
	- alternative view: dynamically constructs a bad input for it
- doesn’t know what original algorithm will do in the future
	- i.e. must work for any original algorithm 

To get a good lower bound, design a good adversary

### Finding max
**Goal**: find max element in an unsorted array
In an array of size n, can do this with $n-1$ comparisons
Only **comparisons** are relevant

#### Theorem
Any comparison-based algorithm for this problem requires at least $n-1$ comparisons in the worst case

##### Proof
After $\leq n-2$ comparisons, $\geq 2$ elements never lost
$\implies$ Adv can make any of them max and be consistent
$\implies$ not enough info for algorithm to make a decision
Hence algorithm needs to make at least $n-1$ comparisons

#### Designing Adversary's strategy
Adversary's strategy can be represented as a status update table with the number of bits of new relevant info
When algorithm asks to compare $i:j$, reply as follows:

| Status for i,j | Adv Reply   | New status | New info |
| -------------- | ----------- | ---------- | -------- |
| $N:N$          | $a_i > a_j$ | $N:L$      | $1$      |
| $N:L$          | $a_i > a_j$ | No change  | $0$      |
| $L,N$          | $a_i < a_j$ | No change  | $0$      |
| $L:L$          | Consistent  | No change  | $0$      |
One comparison gives $\leq 1$ bit of new relevant info (i.e. new $L$)
In total, Algorithm needs $n-1$ bits of info to make a decision
Hence $\geq n-1$ comparisons are necessary

### Finding $2^{nd}$ largest
**Goal:** find the $2^{nd}$ largest element in an unsorted array

#### Theorem
Any comparison-based algorithm for this problem requires at least $n+[\log_2 n]-2$ comparisons in the worst case

##### Observations
1. Any correct algorithm must determine the max

$$n-1 \; elements \; must \; lose \; 1 \; comparisons$$

2. The $2^{nd}$ largest must lose to max directly
3. If max had direct comparisons with $m$ elements, then $m \; 1$ of these elements must lose $2$ comparisons
4. Hence, at least $n-1+m-1=n+m-2$ comparisons are required

#### Adversary's strategy
Enough to prove the following

##### Lemma
Adversary can force $[\log_2 n]$ comparisons involving max

##### Proof
Adversary assigns weight $w_i$ to each input $a_i$
Initially all $w_i=1$, then update using these rules

| Weights       | Adv Reply   | Update               |
| ------------- | ----------- | -------------------- |
| $w_i > w_j$   | $a_i > a_j$ | $w_i=w_i+w_j, w_j=0$ |
| $w_i < w_j$   | $a_i < a_j$ | $w_j=w_i+w_j, w_i=0$ |
| $w_i = w_j>0$ | $a_i > a_j$ | $w_i=w_i+w_j, w_j=0$ |
| $w_i = w_j=0$ | Consistent  | No change            |
###### Analysis
- $w_i=0 \iff i$ lost $\geq 1$ comparison
- Weight of an element at most doubles after a comparison
- If max is involved in $m$ comparisons, its weight is $\geq 2^m$
- In the end, max accumulates all the weight, so  $n\geq 2^m$.
- Taking logs, $\log_2 n \geq m$, as required.

So, Adversary can force $\log_2 n$ comparisons with max, which proves the lemma and hence the theorem