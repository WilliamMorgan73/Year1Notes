# The number of leaves in a tree
## Lemma
A tree with at least $2$ vertices, $n_3$ of which have degree of at least $3$, has at least $n_3 +2$ leaves

### Proof
Let $T$ be a tree on $n \ge 2$ vertices. We can use induction on $n$
- Let $\gamma (T)$ denote the number of leaves in $T$ , and $n_3(T)$ denote the number of vertices of degree at least $3$ in $T$
- Induction base:
	- if $n=2$, then $n_3=0$ and $T$ has $2$ leaves
- Step
	- Now suppose that every tree $<n$ vertices has at least $n_3+2$ leaves (induction hypothesis) and consider a tree $T$ on $n\ge 3$ vertices
- Since $T$ is a tree on at least $3$ vertices, $T$ has a leaf $u$
- Then $T'=T-u$ is a tree on $n-1$ vertices. By the induction hypothesis, we have $\gamma (T') \ge n_3(T')+2$
- Let $v$ be the (unique) neighbour of $u$ in $T$
- $T$ is connected and has at least $3$ vertices, so $v$ has at least 2 neighbours in $T$

The rest of the proof is by **case analysis**

1. Suppose that $v$ has exactly two neighbours in $T$

Then $n_3(T')=n_3(T)$ and $\gamma (T')=\gamma (T)$
Hence, $\gamma (T)=\gamma (T') \ge n_3 (T')+2 = n_3 (T)+2$

2. Suppose that $v$ has exactly three neighbours in $T$

Then $n_3(T')=n_3(T)-1$ and $\gamma (T')=\gamma (T)-1$
Hence, $\gamma (T)=\gamma (T')+1 \ge n_3 (T')+2+1 = n_3 (T)-1+2+1 = n_3(T)+2$

3. Suppose that $v$ has at least four neighbours in $T$

Then $n_3(T')=n_3(T)$ and $\gamma (T')=\gamma (T)-1$
Hence, $\gamma (T)=\gamma (T')+1 \ge n_3 (T')+2+1 = n_3 (T)+2+1 \ge n_3 (T) + 2$

# Every tree is a bipartite graph
## Proof
- Choose any vertex $v$ and put this vertex in the set $V_1$.
- For every vertex $u= v$, there is a unique path from $v$ to $u$ in $T$, consider the length of this path.
- If the length is odd, put $u$ in $V_2$; otherwise put $u$ in $V_1$. 
- We have to show that this is a valid bipartition.
- $V_1$ and $V_2$ are disjoint and together make up $V(T)$. 
- Every edge has end vertices in both $V_1$ and $V_2$. 
- This completes the proof.

# Graph isomorphism
Two graphs $G=(V,E)$ and $G'=(V',E')$ are **isomorphic** if there exists a **bijective** function $f: V \rightarrow V'$ such that for every $u,v \; \varepsilon \; V$ we have: 
$uv \; \varepsilon \; E$ if and only if $f(u)f(v) \; \varepsilon \; E'$. Then we write $G \approxeq G'$

## Example
![[Isomorphic graphs.png]]
bijective function $f$ for the first and second graph:
$1 \rightarrow a, \; 2 \rightarrow d, \;, 3 \rightarrow b, \; 4 \rightarrow e, \; 5 \rightarrow c, \; 6 \rightarrow f$ 

Bijective function $f$ for the second and third graph:
$a \rightarrow x, \; b \rightarrow c, \;, c \rightarrow z, \; d \rightarrow u, \; e \rightarrow w, \; f \rightarrow y$

In other words $G \approxeq G'$ when:
- There exists a correspondence between vertices of $G$ and $G'$ which maintains the "neighbourhood property"
- There is a "renaming" of $G'$ such that it coincides with $G$

Isomorphism is an equivalence relationship:
- $G \approxeq G$ i.e., every graph is isomorphic to itself, and
- if $G_1 \approxeq G_2$ and $G_2 \approxeq G_3$ then also $G_1 \approxeq G_3$

## Properties

If $G$ and $G'$ are isomorphic they shared **all** their structural characteristics e.g.,
- Number of vertices and edges, degree sequence, (Strong) connectivity
- Euler circuit, Hamiltonian circuit, chromatic number, size of largest independent set...

But none of these alone determines isomorphism
![[Pasted image 20240228132714.png]]
Not isomorphic:
- although same number of vertices / edges, degree sequence 
- Euler circuit, Hamiltonian Circuit: yes 
- chromatic number, size of largest independent set: no

All these (and all other characteristics) can **only** be used to show **non-isomorphism**

