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

## Randomised quick sort
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

