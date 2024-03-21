# Connecting the vertices
Input:
a graph $G=(V,E)$ with a weight $w(u,v)$ for each edge $(u,v)$

![[Pasted image 20240311171207.png]]

Our objective is to choose a subset of edges that connects the vertices in a way that costs the least

# Minimum Spanning Tree Problem
Find a **tree** that **spans** the vertices and has **minimum** cost
Basic properties of MSTs:
- Have $|V|-1$ edges
- Have no cycles
- Might not be unique

# Representation of Weighted Graphs
Be careful with the adjacency matrix $A$
- An entry $A(i,j)=0$ means the edge does not exist
- This is not the same as the edge has weight $0$
- As we are looking for a **minimum-cost**, we could assume $A(i,j)=0$ as $A(i,j)=\infty$

$$A=\begin{pmatrix}  
0 & 5 & 0 & 4 & 0 & 0 & 0 & 0 & 0\\
5 & 0 & 10 & 3 & 9 & 0 & 0 & 0 & 0\\
0 & 10 & 0 & 0 & 5 & 7 & 0 & 0 & 0\\
4 & 3 & 0 & 0 & 8 & 0 & 7 & 0 & 0\\
0 & 9 & 5 & 8 & 0 & 7 & 6 & 7 & 0\\
0 & 0 & 7 & 0 & 7 & 0 & 0 & 2 & 5\\
0 & 0 & 0 & 7 & 6 & 0 & 0 & 5 & 0\\
0 & 0 & 0 & 0 & 7 & 2 & 5 & 0 & 3\\
0 & 0 & 0 & 0 & 0 & 4 & 0 & 3 & 0
\end{pmatrix}$$

# Kruskal's Algorithm
- Sort the edges by weight
- Let $A=\emptyset$
- Consider edges in increasing order of weight. For each edge $e$, add $e$ to $A$ unless we create a cycle

## Algorithm

```
V is the set of vertices,
E is the set of edges
A is the empty set (will add edges until it is MST)
for each vertex v do
	C(v) = {v} (each vertex in component by itself)
end for
sort E
while E is not empty do
	choose e = (u, v) in E with min cost
	if C(u) 6 = C(v) then
		add e to A
		for each vertex w in C(u) and C(v) do
			update C(w) with C(u) ∪ C(v)
		end for
	end if
end while
return A
```

Implement the array using **Union-Find** data structure
- Sorting initially still takes time $O(E \log V)$
- Union-Find operations also takes time $O(E \log V)$
Running time is $O(E \log V)$

# Prim's Algorithm
1. Let $U=\{u\}$ where $u$ is some vertex chosen arbitrarily
2. Let $A= \emptyset$
3. Until $U$ contains all vertices:
	- Find the least-weight edge $e$ that joins a vertex in $v$ in $U$ to a vertex $w$ not in $U$
	- Add $e$ to $A$ and $w$ to $U$

## Algorithm

```
V is the set of vertices
E is the set of edges
U = {u}
A is the empty set (will add edges until it is MST)
for each vertex v except u do
	B(v) is the least-weight edge from v to U
end for
while U 6 = V do
	choose v with minimum cost B(v)
	A = A + e
	U = U + v
	update B
end while
return A
```

Implement the array using a **priority queue** (using a heap for example)
- To initialize, all edges considered
- iterate through While loop once for each vertex
- Extracting the minimum cost edge and performing updates take $O(\log V)$ time

Running time is $O(V \log V + E)$

# A generic MST Algorithm
Both Kruskal's and Prim's are special cases of a generic (greedy) MST- algorithm
- We iteratively build a vertex set $A$ such that
	- A is a subset of some minimum spanning tree (MST)

Some necessary definitions
- Let $A$ be a subset of an MST. If the set $A \cup \{(u,v)\}$ is also a subset of an MST, then $(u,v)$ is a **safe** edge for $A$
- A  $cut(S,V-S)$ of $G=(V,E)$ is a partition of $V$
- An edge $(u,v) \; \varepsilon \; E$ **crosses** the $cut(S,V-S)$ if $u \; \varepsilon \; S$ and $v \; \varepsilon \; V-S$ (or vice-versa)
- An edge $(u,v) \; \varepsilon \; E$ is a **light edge** crossing a cut if its weight is smallest among all edges crossing the cut
- A cut **respects** a set $A$ of edges if no edge of $A$ crosses the cut

## Algorithm

```
A <- emptySet
	while A does not form a spanning tree
		do find an edge (u,v) that is safe for A
			A <-- A set of {(u,v)}
	return A
```

## Theorem
Let $G=(V,E)$ be a connected undirected graph with a real-valued weight function $w$  defined on the edges $E$.
Let $A \subseteq E$ such that $A$ is included in some MST of $G$,
Let $(S,V-S)$ be any cut of $G$ that respects $A$, and
Let $(u,v)$ be a light edge crossing $(S,V-S)$.
Then the edge $(u,v)$ is **safe** for $A$

### Proof
The cut $(V_C, V - V_C)$ respects $A$ and $(u,v)$ is a light edge for this cut.
Therefore $(u,v)$ is safe for $A$ by the above theorem
