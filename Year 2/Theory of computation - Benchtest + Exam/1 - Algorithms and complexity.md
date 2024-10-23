# Algorithm
a computational procedure taking some value(s) as input (i.e. the input instance), and producing some value(s) as output.

# Problem
specifies a desired relationship between input / output. i.e. which outputs are correct for every input instance.  
- An algorithm is correct if, for every input instance, it halts (in finite time) with a correct output.  
- A correct algorithm solves the problem.  
	- In this course we only consider correct algorithms

# Asymptotic notation
For two given functions $f(n)$ and $g(n) \geq 0$ 
- $f (n) = O(g(n))$ if $\exists c \ge 0, n_0$ such that 
$$f (n) ≤ c · g(n) \forall n \geq n_0$$  
- $f (n) = \Omega(g(n))$ if $\exists c \ge 0, n_0$ such that  
$$f (n) \geq c · g(n) \exists n \geq n_0$$  
- $f (n) = \Theta(g(n))$ if $\exists c_1, c_2 \ge 0, n_0$ such that  
$$c_1g(n) \geq f (n) \geq c_2g(n) \forall n \geq n_0$$

For two given functions $f (n), g(n) \geq 0$  
- $f (n) = o(g(n))$ if for every $c_1 \ge 0, \exists n_0$ such that  
$$f (n) \geq c_1g(n) \forall n \geq n_0$$
- $f (n) = \omega(g(n))$ if for every $c_2 \ge 0, \exists n_0$ such that  
$$f (n) \geq c_2g(n) \forall n \geq n_0$$
(Think that $c_1$ can be as small as possible, and that $c_2$ can be as large as possible).

## Relationships

Relationships: For any $f (n), g(n)$:  
1. $f (n) = \Theta(g(n)) ⇔ g(n) = \Theta(f (n))$
2. $f (n) = \Theta(g(n)) ⇔ f (n) = O(g(n)) \; and \;  f (n) = \theta(g(n))$
3. $f (n) = O(g(n)) ⇔ g(n) = \Omega(f (n))$
4. $f (n) = o(g(n)) ⇔ g(n) = \omega(f (n))$
5. $f (n) = O(g(n)) ⇔ either \; f (n) = \Theta(g(n)) \; or \; f (n) = o(g(n))$
6. $f (n) = Ω(g(n)) ⇔ either \; f (n) = Θ(g(n)) \; or f (n) = \omega(g(n))$ 

# Running time
The running time $T (I)$ of an algorithm $\alpha$ on input $I$ is the time taken by $\alpha$ on $I$ until $\alpha$ halts. We classify inputs according to their size
What is the size? Ideally: Number of bits necessary to represent the input in a real computer program, but the encoding can be done in different ways
## Worst-case running time
We define the worst-case running time $T (n)$ of algorithm $\alpha$ on inputs of size $n$ as  
$$T (n) := max\; \{T (I) : \; I \; has \; size \; n\}$$
(Convention: If there are no inputs of size n, we define  $T (n) := 0$)
So for any input $I$ of size $n$,  
$$T (I) \leq T (n)$$
### Calculating running time
Let $I$ be input for algorithm $\alpha$ How do we compute $T (I)$?  
Let the pseudocode of algorithm $\alpha$ consist of $p$ lines.  
Assume that the execution of line $i$ requires time $1$.  
- the “RAM model” of computation: every primitive operation  takes constant time  
Let $q_i$ be the number of times line $i$ is executed on input $I$.  
Definition: The running time of $\alpha$ on input $I$ is  
$$T(I)=\Sigma^p_{i=1}q_i$$

## Example: Insertion sort
![[InsertionSortBigo.png]]

$$T(A)=\Sigma^7_{i=1} q_i = 4n-3+3\Sigma^n_{j=2}t_j-2(n-1)$$
$$=2n-1+3\Sigma^n_{j=2}t_j$$

