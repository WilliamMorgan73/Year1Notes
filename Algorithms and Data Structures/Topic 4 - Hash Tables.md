A hash table consists of a bucket array and a hash function
A bucket array for a hash table is an array *A* of size *N* (capacity of the hash table), where each cell of A is thought as a bucket storing a collection of key-value pairs

## Hash function

A hash function *h* is a function mapping each key *k* to an integer in the range $[0, N-1]$
The main idea is to use *h(k)* as an index into the bucket array *A*. That is we store the key-value pair $(k, v)$ in the bucket $A[h(k)]$

If there are two keys with the same hash value *h(k)* then a collision has occurred

A hash function is usually specified as the composition of 2 functions:
1. Hash code
	- Keys to integers
2. Compression function
	- Integers to $[0, N-1]$

Ideal goal: Scramble the keys uniformly
- Hash function should be efficiently computable
- Each table position equally likely for each key

### Collisions
A good hash functions minimalizes collisions as much as possible
Several methods to deal with collisions
1. Separate chaining
2. Linear probing
3. Quadratic probing
4. Double hashing
Methods 2 and 4 are open addressing policies for collision resolution

#### Separate chaining
Each bucket *A[ i ]* stores a list holding the entries *(k , v)* such that $h(k) = i$

**Performance**
- $Cost \propto length \; of \; the \; list$
- $Average \; length = \frac{N}{M} \; (N=Amount \; of \; data, \: M = Size \; of \; array)$ 
- Worst case - All keys hash to same value

#### Linear probing
We try to insert an entry *(k , v)* into a bucket *A[ i ]* that is already occupied, where $i=h(k)$, then we try next as $A[(i+1) \; mod \; N]$
If $A[(i+1) \; mod \; N]$ is also occupied we try $A[(i+2) \; mod \; N]$ and so on

**Costs**
- Insert and search cost depend on length of cluster
- Average length of cluster is $\frac{N}{M}$
- Worst case: All keys hash to same cluster

#### Quadratic probing
Iteratively tries the buckets

$A[(i+f(j)) \; mod \; N]$ for $j=0,1,2, ...$, where $f(j)=j^2$

Until finding an empty bucket
Results in secondary clustering
May not find an empty bucket even if one exists

#### Double hashing
We chose a secondary hash function $h'$ and if *h* maps some key *k* to a bucket *A[ i ]*, with $i=h(k)$ that is already occupied then we iteratively try buckets

$A[(i+f(j)) \; mod \; N]$ for $j=0,1,2, ...$, where $f(j)=j \times h'(k)$

A common choice of a secondary hash function is
$h'(k) = q-(k \; mod \; q)$ for some prime number $q<N$

Secondary hash function must not evaluate to 0

#### Comparison
- The open addressing schemes are more memory efficient compared to separate chaining
- In experimental and theoretical analyses, the separate chaining method is either competitive or faster than other methods
- If memory space is not major issue - separate chaining best choice

#### Deletions
Must not hinder future searches 
- If a bucket is left empty will hinder future searches
- Should not be left unusable

To solve this we use tombstones (A maker that is left after a deletion)
- If encountered when searching along a prove sequence, we know to continue
- If encountered during insertion, should continue probing to avoid creating duplicates but then the new record can be placed in the bucket where the tombstone was found

The use of tombstones lengthens the average probe sequence distance
Two possible remedies:
1. Local reorganization
	- After deleting a key, continue to follow the probe sequence of that key and move records into vacated bucket
	- This will not work for all collision resolution policies
2. Periodic refresh 
	- Periodically refresh the table by reinserting all records into a new hash table
	- If you  have a record of which keys are accessed most of these can be placed where they will be found most easily


