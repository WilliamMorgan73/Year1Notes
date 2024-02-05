We'll look at 2 types of iterative sorting algorithms
1. Insertion sort
2. Selection sort

And two recursive algorithms
1. Merge sort
2. Quick sort

## Insertion sort

```
Insertion Sort
---------------------------------------------------------
Input: List
Output: Sorted list
---------------------------------------------------------

for j = 2 to n do
    x = a_j
    i = j - 1
    
    while i > 0 and a_i > x do
        a_(i + 1) = a_i
        i = i - 1
    end while
    
    a_(i + 1) = x
end for
```

Running time between $n-1$ and $\frac{n(n-1)}{2}$
Worst case: $O(n^2)$

## Selection sort

```
Selection Sort
-------------------------------------------
Input: List
Output: Sorted list
-------------------------------------------

for i = 1 to n-1 do
    elem = a_i
    pos = i
    
    for j = i + 1 to n do
        if a_j < elem then
            elem = a_j
            pos = j
        end if
    end for
    
    swap a_i and a_pos
end for
```
Elem keeps track of current idea of value $i^{th}$ smallest element
Pos keeps track of current idea of position of $i^{th}$ smallest element

 Time complexity:
$$
\Sigma^{n-1}_{j=1} \Sigma^n_{j=i+1} 1 = \Sigma^{n-1}_{j=1}(n-1)
$$
$$
=(\Sigma^{n-1}_{j=1} n) - (\Sigma^{n-1}_{j=1} i)
$$
$$
=(n-1) \times n - \frac{n(n-1)}{2}
$$
$$
=\frac{n(n-1)}{2}
$$
$$
=O(n^2)
$$

## Bubble sort

```
Bubble Sort
---------------------------------------------------------
Input: List
Output: Sorted list
---------------------------------------------------------

for i = 1 to n-1 do
    for j = 1 to n-i do
        if a_j > a_(j+1) then
            swap a_j and a_(j+1)
        end if
    end for
end for
```

Time Complexity: O($n^2$)

## Merge sort

Merge Sort is a divide-and-conquer algorithm that follows these steps:

1. **Divide:** Divide the unsorted list into two halves.
2. **Conquer:** Recursively sort each half.
3. **Combine:** Merge the sorted halves to produce a single sorted list.

```
Merge Sort
---------------------------------------------------------
Input: List
Output: Sorted list
---------------------------------------------------------

merge_sort(list):
    if length of list <= 1 then
        return list
    
    mid = length of list / 2
    left_half = merge_sort(first half of list)
    right_half = merge_sort(second half of list)
    
    return merge(left_half, right_half)

merge(left, right):
    result = empty list
    
    while left is not empty and right is not empty do
        if first element of left <= first element of right then
            append first element of left to result
            remove first element from left
        else
            append first element of right to result
            remove first element from right
    
    append remaining elements of left to result
    append remaining elements of right to result
    
    return result
```

Time Complexity: O($n \log n$)

**Proof**

1. **Divide Step:** In each recursive call, the array is divided into two halves. This takes O(1) time.
2. **Conquer Step:** Recursively sorting each half takes time proportional to the size of the subarrays. The time complexity is therefore T($n$) = 2T($\frac{n}{2}$), where $n$ is the size of the array.
3. **Combine Step:** Merging two sorted halves into a single sorted array takes linear time O($n$).

Combining these steps and solving the recurrence relation gives the overall time complexity:

$$
T(n)=2T\left(\frac{n}{2}\right)+O(n)
$$

By the Master Theorem, this recurrence relation has a solution of O($n \log n$)

## Quick sort

A sorting algorithm that follows a divide-and-conquer approach. It works as follows:
1. **Partitioning:** Choose a pivot element from the array and partition the other elements into two sub-arrays according to whether they are less than or greater than the pivot.
2. **Recursion:** Recursively apply the same process to the sub-arrays.
3. **Combine:** No explicit combining is needed in Quick Sort, as the sorting is achieved during the partitioning step.

```
Quick Sort
---------------------------------------------------------
Input: List
Output: Sorted list
---------------------------------------------------------

quick_sort(list, low, high):
    if low < high then
        pivot_index = partition(list, low, high)
        quick_sort(list, low, pivot_index - 1)
        quick_sort(list, pivot_index + 1, high)

partition(list, low, high):
    pivot = list[high]
    i = low - 1
    
    for j = low to high - 1 do
        if list[j] <= pivot then
            i = i + 1
            swap list[i] and list[j]

    swap list[i + 1] and list[high]
    return i + 1
```

**Time complexity:**
- Average-case: O$(n \log n)$
- Worst case: O$(n^2)$

**Proof**

1. **Partitioning:** The partition step takes O($n$) time, where $n$ is the size of the array.
2. **Recursion:** On average, the array is divided into two roughly equal halves. If we assume that the partitioning is reasonably balanced, the recurrence relation is 

$$
T(n) = 2T\left(\frac{n}{2}\right) + O(n).
$$

By the Master Theorem, this recurrence relation has a solution of O($n \log n$), proving the average-case time complexity of Quick Sort.

### Randomised quick sort
If we chose a pivot that isn't in the centre, how do we analyse that
There would be a short branch and a long branch
How do we analyse this?

If X is a random variable that denotes the number of comparisons during a run of randomised quick sort then:
$$E[X] = O(n \log n)$$
**Proof

$$T(n) = (n - 1) + \frac{1}{n} \underset{\text{average over split}}{\sum_{i=0}^{n} (T(i) + T(n - i - 1))}$$
This expression can be further simplified:
$$= (n - 1) + \frac{1}{n} \left[ \sum_{i=0}^{n-1} T(i) + \sum_{i=0}^{n-1} T(n - i - 1) \right]$$
$$= (n - 1) + \frac{1}{n} \left[ \sum_{i=0}^{n-1} T(i) + \sum_{i=0}^{n-1} T(i) \right]$$
$$= (n - 1) + \frac{2}{n} \sum_{i=0}^{n-1} T(i)$$

## Bucket Sort
Suppose that values are in the range $0 ... k-1$ start with $k$ empty buckets numbered $0$ to $k-1$
Scan the list and place element $s[i]$ in bucket $s[i]$, and then output the buckets in order

We need an array of buckets and the values in the list to be stored will be the indexes of the buckets
- No comparisons will be necessary
- However, if large range, we need a large number of buckets

**Algorithm**
```
BucketSort(S)
----------------------------------------------------------------------
Values in S are in between 0 and k-1
----------------------------------------------------------------------
for j = 0 to k-1 do
	b[j] = 0
end for

for i = 0 to n-1 do
	b[S[i]] = b[S[i]] + 1
end for

i = 0

for j = 0 to k-1 do
	for j = 0 to k-1 do
		S[i] = j
		i += 1
	end for
end for
```

**Values/Entries**
If we were sorting values, each bucket is just a counter that we increment whenever a value matching the bucket's number is encountered
If we were sorting entries according to keys, then each bucket is a queue
 - Entries are enqueued into a matching bucket
 - Entries will be dequeued back into the array after the scan

**Time complexity

Bucket initialization: $O( k )$
From array to buckets: $O( n )$
From buckets to array: $O(n)$

Even though this stage is a nested loop, all we do is dequeue from each bucket until they are empty $n$ dequeue operations in all

Worst case:
$$O(n+k)$$
Since $k$ will likely be small compared to n
Bucket sort is 
$$O(n)$$

**Running time**
Running time is:
$$O(n+k)$$
This means that if $k$ is small, say $o(n \log n)$ the overall running time of bucket sort is:
$$o( n \log n)$$
Also, if $k$ gets really large, it will dominate:

If $k=\omega(n \log n)$
- Worse than that or Merge Sort
If $k=\omega(n^2)$
- Worst than that of any other sorting algorithm that we've seen

## Radix sort
Have as many buckets as you've got different digits, that is for base 10 you'll have 10 buckets max
Repeatedly bucket sort by given digit
Number of rounds depend on values, but number of buckets depends on number of different digits

**Example**
Consider the input $67,23,90,6,43,22,18,75,49,12,36$

First pass the right most digit which gives the following bucket (giving a new array)

**Pass 1:**
Bucket 0: 90
Bucket 1:
Bucket 2: 22, 12
Bucket 3: 23, 43
Bucket 4:
Bucket 5:
Bucket 6: 6, 36
Bucket 7: 67, 75
Bucket 8: 18, 49
Bucket 9:

**Pass 2:**
Bucket 0: 12
Bucket 1:
Bucket 2: 22, 23
Bucket 3: 36, 43
Bucket 4: 49
Bucket 5:
Bucket 6: 6, 67
Bucket 7: 75, 90
Bucket 8: 18
Bucket 9:

**Pass 3:**
Bucket 0: 6, 12, 18
Bucket 1: 22, 23
Bucket 2: 36, 43
Bucket 3: 49
Bucket 4: 67
Bucket 5: 75
Bucket 6:
Bucket 7: 90
Bucket 8:
Bucket 9:

Works if the bucket sort phases are stable meaning work done in previous rounds won't be destroyed

**Time complexity**
Compare to plain bucket sort for range ${0, ..., k-1}$
- Radix sort $d=\log_{10} k$ giving $O(n \log k)$
- Bucket sort $O(n+k)$

Not immediately clear which is better in terms of times (Radix sort obviously better whenever k non-trivial)

Examples:
- If $k=n$ then $O(n \log n)$ vs $O(n)$
	- Bucket sort wins
- If $k=n^2$ then $O(n \log n)$ vs $O(n^2)$
	- Radix sort wins
- If $k=2^n$ then $O(n \log n)$ vs $O(2^n)$
	- Radix sort wins

Anyways, if $k$ is constant then both are linear time $\theta(n)$
