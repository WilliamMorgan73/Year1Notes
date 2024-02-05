## Searching
### Binary search
Assumptions
1. Peek right into the middle of given array, at position
$$p=\left[\frac{n}{2}\right]$$
2. If $A[p] = x$ then we're done and can return $p$
3. Otherwise if $x>A[p]$ we may focus our search on stuff to the right of $A[p]$ and completely ignore the left side
4. Otherwise if $x<A[p]$ we may focus our search on stuff to the left of $A[p]$ and completely ignore the right side

```
Recursive binary search
------------------------------------------------------
int search(int A[1 .. n], int left, int right, int x)
{
	if (right == left and A[left] != x)
		handle error; Leave functiomn

	p = middle_index between left and right

	if (A[p] == x) then
		return p

	// Here come the recursive calls (if x is not yet found)
	if (x > A[P]) then
		return search(A, p+1, right, x)) // In right half
	else // x < A[P]
		return search(A, left, p-1, x)) // In left half
	
}
```

**Complexity**
$$T(n) = T \left(\frac{n}{2}\right) + O(1) = O(\log n)$$
Which, for large $n$, is an awful lot quicker

## Selection
### Quick select
- Recursive
- Partition() function
- Not two recursive calls but 1
	- Dividing into the part (LOW or HIGH) where we know the $i^{th}$ smallest element is to be found
	- Know that after partitioning, pivot is in correct position w.r.t overall sortedness so can simply compare pivot position after partitioning with sought index $i$

```
QuickSelect(int A[1 .. n], int left, int right, int i)
------------------------------------------------------
	if (right == left) then
		return A[left]
	else

		// rearrange/partition in place
		// Return value 'pivot' is index of pivot element
		// in A[] after partitioning

		pivot = Partition(A, left, right)
		
		// Now
		// Everything in A[left...pivot-1] is smaller than pivot
		// Everything in A[pivot+1...right] is bigger than picot
		// The pivot is in correct position w.r.t sortedness

		if (i === pivot) then
			return A[i]
		else if (i<pivot) then
			return QuickSelect(A, left, pivot-1, i)
		else
			return QuickSelect(A, pivot+1, i)
		end if
	end if
```

**Example**
`Array: [6, 2, 8, 4, 5, 1, 3, 7]`
1. **Initial Array:** `[6, 2, 8, 4, 5, 1, 3, 7]`
    - Let's choose the pivot. For simplicity, let's say we choose the first element, `6`.
2. **Partitioning:**
    - Partition the array into elements less than `6` and elements greater than `6`.
    - `[2, 4, 5, 1, 3] | 6 | [8, 7]`
3. **Recursive Call:**
    - Since we are looking for the 4th smallest element, and there are 5 elements on the left of the pivot, we recursively call QuickSelect on the left subarray with `k = 4`.
4. **Recursive Step 1:**
    - New subarray: `[2, 4, 5, 1, 3]`
    - Choose a pivot (let's say `3`) and partition the array.
    - `[2, 1] | 3 | [4, 5]`
5. **Recursive Call 1:**
    - Since `k = 4` and the size of the left subarray is 2, we now need to find the 2nd smallest element in the right subarray `[4, 5]`.
6. **Recursive Step 2:**
    - New subarray: `[4, 5]`
    - Choose a pivot (let's say `4`) and partition the array.
    - `[4] | 5`
7. **Recursive Call 2:**
    - Since `k = 2` and the size of the left subarray is 1, we now need to find the 1st smallest element in the left subarray `[4]`.
8. **Base Case:**
    - The size of the subarray is 1, so the 1st smallest element is `4`.
9. **Result:**
    - The 4th smallest element in the original array `[6, 2, 8, 4, 5, 1, 3, 7]` is `4`

**Performance**
**Worst Case:** O(n^2)
- The worst-case scenario occurs when the chosen pivot does not effectively divide the array, leading to unbalanced partitions. 
$$T(n) = T(n-1)+O(n) = O(n^2)$$ 
### Median of medians