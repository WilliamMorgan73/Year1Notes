## Elementary functions
We should know:

$log_a(b) = c \; \; \; iff \; \; \;  a^c = b$

$log_a(b \times c) = log_a(b) + log_a(c)$

$log_a(b / c) = log_a(b) - log_a(c)$

$log_a(b^c) = c \times log_a(b)$

$log_a(b) = \frac{log_c(b)}{log_c(a)}$

$log_b(b^x) = x$

$b^{a log_b x} = x^a$

## Time complexity
The time complexity of an algorithm can be expressed in terms of the number of basic operations used by the algorithm when the input has a particular size

Examples of basic operations are:
- Additions
- Multiplications
- Comparisons
- Swaps
- Assignments

### Worst-case time complexity
The worst-case time complexity of an algorithm can be expressed in terms of the largest number of basic operations used by the algorithm when the input has a particular size

Tells us how many operations an algorithm needs to guarantee a solution
Usually time complexity = Worst-case time complexity

Usually we don't need to compute the exact number of operations, it is sufficient to estimate this number using **bounds**
- We are most interested in **upper bounds** for worst-case analysis
- Should give us the possibility to estimate growth of the number of operations when the input size increases

## Big O notation
Let *f* and *g* be functions from the set of integers or the set of real numbers to the set of real numbers
We say that *f* is *O(g)* if there are constants *c* and *k* such that

$$
|f(x)| \leq C\times|g(x)|
$$
Whenever $x \geq k$

This reads:
	After a certain point, namely after *k*, the absolute value of *f(x)* is bounded from above by *C* times the absolute value of *g(x)*
	In terms of complexities f(x) is no worse than $C \times g(x)$ for all relatively large input sizes *x*
	*C* is a fixed constant usually depending on the choice of *k* (Not allowed to increase *C* as *x* increases)


The  constants *C* and *K* in the definition of Big-O are called **witnesses** to the relationship
There can be many witnesses

**Real definition**

$Let \; f: \; \mathbb{N} -> \mathbb{N}$

$$
O(f) = { g: \mathbb{N} -> \mathbb{N} \; | \; \exists}C, k > 0, \; \; g(x) \leq C \times f(x) \; for \; x \geq k \}
$$

| Big-O form            | Name                      |
|------------------------|---------------------------|
| O(1)                   | constant                  |
| O$(\log n)$               | logarithmic               |
| O$(n)$                   | linear                    |
| O$(n \log n)$             | $n \log n$                   |
| O$(n^2)$                 | quadratic                 |
| O$(n^3)$                 | cubic                     |
| O$(n^k)$ for $k = 0, 1, 2, \ldots$ | polynomial                |
| O$(c^n)$ for $c > 1$   | exponential               |

### Examples

Let  $f(x) = x^2 + 2x + 1$. Then $f(x) = O(x^2)$

**Proof:**

For $x \geq 1$), we have $1 \leq x \leq x^2$. That gives

$$f(x) = x^2 + 2x + 1 \leq x^2 + 2x^2 + x^2 = 4x^2$$

for $x \geq 1$ Because the above inequality holds for every positive $x \geq 1$ using $k = 1$ and $C = 4$ as witnesses, we get

$$f(x) \leq C \cdot x^2$$

for every $x \geq k$

---

Let $f(x) = 3x^3 - 7x^2 - 4x + 2$. Then $f(x) = O(x^3)$.

**Proof:**
For $x \geq 1$, we have $1 \leq x \leq x^2 \leq x^3$. That gives

$$ |f(x)| = |3x^3 - 7x^2 - 4x + 2| \leq 3x^3 + 7x^2 + 4x + 2$$
$$
\leq 3x^3 + 7x^3 + 4x^3 + 2x^3 = 16x^3 
$$


for $x \geq 1$. Because the above inequality holds for every positive $x \geq 1$, using $k = 1$ and $C = 16$ as witnesses, we get

$$|f(x)| \leq C \cdot |x^3|$$

for every $x \geq k$.

---
Let $f(x) = 3x$. Then $f(x)$ is not $O(2x)$.

**Proof:**
Assume that there are constants $k$ and $C$ such that $3x \leq C \cdot 2x$ when $x \geq k$. Then:
$$\left(\frac{3}{2}\right)^x \leq C$$when $x \geq k$.
But any exponential function $a^x$ grows monotonically whenever $a > 1$; a contradiction.

### Sum rule
**Theorem**
$$
If \; f1(x) \; is \; O(g1(x)) \; and \; f2(x) \; is \; O(g2(x)), \; then \; f1(x) + f2(x) \; is \; O(max{|g1(x)| \; ,\; |g2(x)|})
$$
**Proof:**

Let $C_i$ and $k_i$ be witness pairs for $f_i(x)$ is $O(g_i(x))$, for $i = 1, 2$.

Let $k = \max\{k_1, k_2\}$ and $C = C_1 + C_2$. Then for $x > k$, we have

$$|f_1(x) + f_2(x)| \leq |f_1(x)| + |f_2(x)| \leq C_1 \cdot |g_1(x)| + C_2 \cdot |g_2(x)| \leq C \cdot \max\{|g_1(x)|, |g_2(x)|\}$$

The last inequality is true because
$$C_1y_1 + C_2y_2 \leq C_1 \cdot \max\{y_1, y_2\} + C_2 \cdot \max\{y_1, y_2\} = (C_1 + C_2) \cdot \max\{y_1, y_2\} = C \cdot \max\{y_1, y_2\}$$

### Product rule
**Theorem**

If $f_1(x)$ is $O(g_1(x))$ and $f_2(x)$ is $O(g_2(x))$, then $f_1(x) \cdot f_2(x)$ is $O(g_1(x) \cdot g_2(x))$.

**Proof:**

Let $C_i$ and $k_i$ be witness pairs for $f_i(x)$ is $O(g_i(x))$, for $i = 1, 2$.

Let $k = \max\{k_1, k_2\}$ and $C = C_1 \cdot C_2$. Then for $x > k$, we have

$$|f_1(x) \cdot f_2(x)| = |f_1(x)| \cdot |f_2(x)| \leq C_1 \cdot |g_1(x)| \cdot C_2 \cdot |g_2(x)| = C \cdot |g_1(x) \cdot g_2(x)|$$
This proves the theorem.

## Lower bounds: Big-Omega notation
**Definition:**

Let $f(x)$ and $g(x)$ be functions from the set of real numbers to the set of real numbers. We say that $f(x)$ is $\Omega(g(x))$ if there are positive constants $C$ and $k$ such that
$$|f(x)| \geq C \cdot |g(x)|$$ whenever $x > k$. Note that this implies that $f(x)$ is $\Omega(g(x))$ if and only if $g(x)$ is $O(f(x))$.

## Same order growth rates: Big-theta notation
**Definition:**

Let $f(x)$ and $g(x)$ be functions from the set of real numbers to the set of real numbers. We say that $f(x)$ is $\Theta(g(x))$ if $f(x)$ is $O(g(x))$ and $f(x)$ is $\Omega(g(x))$.

This is equivalent to saying that $f(x)$ is $\Theta(g(x))$ if $f(x)$ is $O(g(x))$ and $g(x)$ is $O(f(x))$.

And this is equivalent to saying that there are constants $C_1$, $C_2$, and $k$ such that $|f(x)| \leq C_1 \cdot |g(x)|$ and $|g(x)| \leq C_2 \cdot |f(x)|$ whenever $x \geq k$.

**Examples:** All polynomials $a_nx^n + \ldots + a_1x + a_0$ with $a_n \neq 0$ are $\Theta(x^n)$.

## Little-o notation
Used to disregard 'small order' terms
Based on the concept of limits

**Definition:**

Let $f(x)$ and $g(x)$ be functions from the set of real numbers to the set of real numbers. We say that $f(x)$ is $o(g(x))$ ( "little-o" of $g(x)$) when
$$\lim_{{x \to \infty}} \frac{f(x)}{g(x)} = 0$$

Without limit:
$$o(g) = \{f : \mathbb{N} \to \mathbb{N} \,|\, \forall C > 0 \, \exists k > 0 : C \cdot f(n) < g(n) \, \forall n \geq k\}$$

Therefore:
$$ f(x) \; is \; o(g(x)) \; implies \; f(x) \; is \; O(g(x)) $$

### Sublinear functions
A function that grows slower than any linear function
With little-o notation we can make this very precise

**Definition:**
A function $f(x)$ is called sublinear if $f(x)$ is $o(x)$, so if 
$$\lim_{{x \to \infty}} \frac{f(x)}{x} = 0$$


## Little-omega
ω is to o what Ω is to O:

$f = \omega(g) \iff g = o(f)$

Or:

**Definition:**
$$
\omega(g) = \{f : \mathbb{N} \to \mathbb{N} \mid \forall C > 0 \, \exists k > 0 : f(n) > C \cdot g(n) \, \forall n \geq k\}
$$
