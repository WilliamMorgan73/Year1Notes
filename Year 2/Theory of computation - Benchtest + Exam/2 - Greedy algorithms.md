# The knapsack problem
We consider two variants.  
1. The 0 − 1 knapsack problem (the “classic” variant): A thief robs a store and finds $n$ items. Item i is worth $v_i$ euros and weighs $w_i$ kilos. The thief can carry at most $W$ kilos in knapsack.
		Which items can he take to maximise his profit?

2. The fractional knapsack problem: Same setup, but this time the thief can take fractions of items. 
	- We can assume (without loss of generality) that the knapsack is not big enough to carry all items:  
$$W < w_1 + · · · + w_n.$$
- Otherwise the thief just takes everything

## Greedy strategy for fractional
Fractional knapsack problem is solvable by following greedy strategy:  
1. Compute the “value per kilo” $r_i = \frac{v_i}{w_i}$ for each item.  
2. Sort items by value per kilo in a non-increasing order.  
3. Take as much as possible of item with greatest “value per kilo”, then take as much as possible of item with the next greatest “value per kilo”, etc., until the total weight equals the knapsack capacity $W$

Suppose $W=10kg$
![[GreedyKnapsack.png]]
The greedy strategy stakes:
1. All of item 2
2. All of item 4
3. 3 kilos of item 3

Total value of $10+20+3\times 1.5 = 34.5$

### Running time of greedy strategy
Step 1 (computing $r_i$ for each i) can be done in $\Theta(n)$
Step 2 (sorting the $r_i$ array) can be done in $\Theta(n \log n)$  
Step 3 (selecting the items) can be done in $\Theta(n)$  
Thus, the worst-case running time is $\Theta(n \log n)$

#### Correctness of greedy for fractional knapsack
$n$ items are sorted by $r_i = \frac{v_i}{w_i}$ in non-increasing order, i.e.:  
$$r_1 \geq r_2 \geq . . . \geq r_n. $$
Two items $p$ and $q$ with $r_p = r_q$ are considered to be equivalent. Hence, we may assume that:  
$$r_1 \gt r_2 \gt . . . \gt r_n.  $$
The total available amount of item $i$ is $w_i$ . Let $k$ be such that  
$$w_1 + . . . + w_k \geq W \; and \; w_1 + . . . + w+{k+1} \gt W$$
(Recall that, as we assumed, the knapsack is not big enough to carry all items, hence such a $k$ exists.)

Let $x = (x_1, . . . , x_n)$ denote a solution: $0 \geq x_i \geq w_i$ is the amount the thief takes of item $i$ for $i = 1, . . . , n$  
The total value stolen is then $\Sigma^n_{i=1}r_i x_i$
The greedy solution x is given by :
$$x_i = w_i \;for \; 1 \geq i \geq k,  $$
$$x_{k+1} = W − (w_1 + . . . + w_k),$$
$$x_i = 0 \; for \;  k + 2 \leq i \leq n.$$
Let $x^∗ = (x^∗_1 , . . . , x^∗_n)$ be an optimal solution.  
First of all, note that we must have $x^∗_1 + . . . + x^∗_n = W$ .  
(We fill up the sack again!) 
We will show that $x^∗ = x.$

Suppose $x^* \neq x$ Then
- $x^*_i$ for some $i \leq k+1$ why? Let $j:= min\left(i:x^*_j \gt x_i\right)$
- Also $x^*_\lambda \gt x_\lambda$ for some $\lambda \gt j$

Let us add more of item $j$ to the optimal case. Let $y$ be another solution, defined by

$$y_i = min\left(w_j, \; x^*_j + \left( x^*_\lambda - x_\lambda \right) \right)$$
$$y_\lambda = x^*_\lambda - (y_j - x^*_j)$$
$$y_i = x^*_i$$
Otherwise,
1. Check that $y$ is a valid solution. i.e. $0\leq y_i \leq w_I$ for all $1 \leq i \leq n$ and that $y_1 + ... + y_n = W$
2. Check that $y$ is a better solution that $x^*$ i.e., $\Sigma^n_{i=1}r_i y_i \gt \Sigma^n_{i=1} r_i x^*_i$ Contradiction!

## Greedy strategy for 0-1 problem
The same algorithm does NOT work for the 0-1 knapsack  
problem.  
For instance, if $W = 6 kg$ and
![[Pasted image 20241017161831.png]]
Optimal solution: Steal objects 2 and 3 for a total of 4 euros
Greedy: Steal object 1 for a total of 3 euros

### Special case of 0-1 knapsack

Suppose that, in a 0-1 knapsack instance, the orders of the items:  
- when sorted by decreasing value $v_i$ , and  
- when sorted by increasing weight $w_i$ ,  
are the same (i.e. $v_1 \geq v_2 \geq . . . \geq v_n$ and $w_1 \geq w_2 \geq . . . \geq w_n$)  
Task: Give an efficient algorithm to find an optimal solution to this variant of 0-1 knapsack, and prove its correctness. 
Same as fractional
# Greedy algorithms for (some) optimization problems
-   In an optimization problem, we are looking for a solution that optimizes (i.e. maximizes / minimizes) some value.  
- In such a problem every solution has a value. 
- An optimal solution is a solution with optimal (minimum or maximum) value. There can be many optimal solutions.  
- Our task is to find one (any!) of them.  
- Any algorithm for an optimization problem (e.g. Knapsack) goes through a sequence of steps.  
- At each step there is a set of choices, among which we have to choose one.  
- A greedy algorithm makes in every step the choice that looks to be the best at the moment. 
- This is called a greedy choice or an locally optimal choice.  
- Not all optimization problems can be solved by greedy algorithms !

# Task scheduling
Another optimization problem: Task scheduling  
- We are given a set $T$ of $n$ tasks. Every task $i$ has a start time $s_i$ and a finish time $f_i$ .
- Every task is to be performed on a machine; every machine can only execute one task at a time.  
- two tasks $i, j$ can be scheduled on the same machine only if they are non-conflicting, i.e. either $f_i \lt s_j$ or $f_j \lt s_i$ .  
Goal:
- Schedule all tasks using the smallest number of machine

![[Pasted image 20241017164423.png]]

## Greedy algorithm

```
m ← 0  
while T is not empty do  
	Remove task i with the smallest si  
	if there is a free machine j for task i then  
		Schedule task i on machine j  
else  
	m ← m + 1
	Schedule task i on machine m
```

## Correctness idea (by contradiction)
- Suppose the algorithm gives k machines but there exists a better schedule with at most $k − 1$ machines.  
- Let $i$ be the first task scheduled on machine $k$. 
- By construction of the algorithm: 
- when we schedule task $i$, each of the machines $1, . . . , k − 1$ contains tasks that are in conflict with task $i$
- all these $k − 1$ tasks all conflict with each other too  
- impossible to schedule all tasks in $k − 1$ machines  
Running time:  
- again O(n log n) time (due to the sorting of the start times $s_1 \lt s_2 \lt . . . \lt s_n$)

