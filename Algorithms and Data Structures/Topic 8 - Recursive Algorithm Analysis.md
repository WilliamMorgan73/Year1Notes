## Solving recurrences by induction
Only need to:
- Guess correct solution
- Verify base case(s) and step

**Example**
Consider the recurrence for Merge Sort:

$$
T(n) \leq \begin{cases} 
      d & \text{if } n \leq c, \text{ for constants } c, d > 0 \\
      2 \cdot T\left(\frac{n}{2}\right) + a \cdot n & \text{otherwise}
   \end{cases}$
$$
Experience/Intuition tells me that this should be:
$$
T(n) = O(n \log_2 n)
$$
If not:
	Start big, and consecutively reduce upper bound

- $O(n^4)$ works, try $O(n^3)$
- Works? Try $O(n^2)$
- Still works? Try $O(n)$
- No luck? Back up to $O(n \log n)$

Use this graph as reference

![[Big O graph.png]]

Now we have a guess, we need to check if it is correct

Ignore $n=1$ and consider only $n  \geq 2$

Recurrence said:
$$
T(n) \leq d \; if \; n \leq c \; for \; constatns \; c \; and \; d. \; Make \; \alpha \; big \; enough
$$
$$d \leq \alpha n \log_2 n \; for \; 2 \leq n \leq c \Leftrightarrow \alpha \geq \frac{d}{2 \log_2 2} = \frac{d}{2}$$
Then for all $2 \leq n \leq c$, we have $T(n) \leq d \leq \alpha n \log_2 n$

As for the rest simply plug it in:

1. First Formula:    $$d \leq \alpha n \log_2 n$$ for $$2 \leq n \leq c$$ $$\Leftrightarrow \alpha \geq \frac{d}{2 \log_2 2} = \frac{d}{2}$$
2. Second Formula:   $$T(n) \leq 2T\left(\frac{n}{2}\right) + an$$
3. Substitution:
$$T(n) \leq 2\alpha n^2 \log_2 n^2 + an$$
4. Further Simplification:
$$T(n) \leq 2\alpha n^2 (\log_2(n) - \log_2(2)) + an$$
5. Continue Simplification:
$$T(n) \leq 2\alpha n^2 (\log_2(n) - 1) + an$$
6. More Simplification:
$$T(n) \leq \alpha n (\log_2(n) - 1) + an$$
7. Final Simplification:
$$T(n) \leq \alpha n \log_2(n) - \alpha n + an$$
8. Conclusion:
$$T(n) \leq \alpha n \log_2 n$$ if $$\alpha n \geq an$$ $$\Leftrightarrow \alpha \geq a$$
9. Overall Conclusion:
Altogether, it works for any $$\alpha \geq \max\{d^2, a\}$$

## Solving recurrences by iterative substitution
Expand recurrence, spot the pattern, then treat as above
Consider again the Merge Sort recurrence

$$
T(n) \leq \begin{cases} 
      d & \text{if } n \leq c, \text{ for constants } c, d > 0 \\
      2 \cdot T\left(\frac{n}{2}\right) + a \cdot n & \text{otherwise}
   \end{cases}$
$$

Expand:

1. Original Equation:
$$T(n) \leq 2T\left(\frac{n}{2}\right) + an$$
2. First Iteration:
$$\leq 2\left(2T\left(\frac{n}{4}\right) + \frac{an}{2}\right) + an = 4T\left(\frac{n}{4}\right) + an + an$$
3. Second Iteration:
$$\leq 4\left(2T\left(\frac{n}{8}\right) + \frac{an}{4}\right) + 2an = 8T\left(\frac{n}{8}\right) + an + 2an$$
4. Third Iteration:
$$\leq 8\left(2T\left(\frac{n}{16}\right) + \frac{an}{8}\right) + 3an = 16T\left(\frac{n}{16}\right) + an + 3an$$
5. Final Iteration:
$$\leq 16\left(2T\left(\frac{n}{32}\right) + \frac{an}{16}\right) + 4an = 32T\left(\frac{n}{32}\right) + an + 4an$$

Looks a lot like we can do this $log_2 n$ many times, and we'll find that after $i$ many times:

**First term:**
$$
2^i T\left(\frac{n}{2^i}\right)
$$
Second term:
$$
i an
$$
Therefore, after $log_2 n$ many times:
$$
2^{log_2 n} \times base \; case \; value + \log_2 (n) an = O(n \log n)
$$

## Solving recurrences using the Master Theorem
Can use if recurrence is of form 
$$T(n) = aT\left(\frac{n}{b}\right) + f(n)$$
for constants $a \geq 1$ and $b > 1$. E.g., MergeSort: $a = 2$, $b = 2$, $f(n) = a'n$.

Three cases:

1. If $f(n) = O(n^{\log_b(a) - \epsilon})$ for some constant $\epsilon > 0$, then $T(n) = \Theta(n^{\log_b(a)})$.

2. If $f(n) = \Theta(n^{\log_b(a) \cdot \log_k n})$ with $k \geq 0$, then $T(n) = \Theta(n^{\log_b(a) \cdot \log_{k+1} n})$.

3. If $f(n) = \Omega(n^{\log_b(a) + \epsilon})$ for some constant $\epsilon > 0$ and if $af\left(\frac{n}{b}\right) \leq cf(n)$ for some constant $c < 1$ and all $n$ large enough, then $T(n) = \Theta(f(n))$.

With Merge Sort, $n^{\log_b(a)} = n^{\log_2(2)} = n$ and $f(n) = a'n$, thus case 2 applies (with $k = 0$), and we find that $T(n) = \Theta(n \log n)$.

Note: $log_k n = (\log n)^k$

