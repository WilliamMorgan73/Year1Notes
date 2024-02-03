## Recursive algorithm
A recursive algorithm is an algorithm that calls itself to do part of its work
**Properties**
- Must have a base case
- Must change its state and move toward the base case
- Must call itself, recursively

### Memoization
Involves storing the result of that function call. 
The next time the function is called with the same parameters, instead of recomputing the result, the function retrieves the precomputed result from the cache.
Hash tables are a good choice of data structure to implement this

### Backtracking
Build up a solution one at a time and backtrack when not able to go further

**Generic algorithm**

```
extend_solution(current solution)
-------------------------------------------------
if current solution is valid then
	if current solution is complete then
		return current solution
	else
		for each extension of the current solution do
			extend_solution(extension)
		end for
	end if
end if
```

#### Example
##### A knights tour
A knight is placed on an empty chessboard and must visit each square exactly once, following the rules of chess knight's moves.

1. **Start Position:** Begin with an empty chessboard and place the knight on any square. This is the starting point for the tour.
2. **Move Generation:** Generate all possible moves for the knight from its current position, considering the valid knight moves. A knight moves in an "L" shape – two squares in one direction and one square in a perpendicular direction.
3. **Exploration and Backtracking:** For each valid move generated, recursively explore the next moves from that position. If a valid tour cannot be completed from a certain position, backtrack to the previous position and try a different move.
4. **Base Case:** The recursion stops when all squares on the chessboard are visited, and a complete knight's tour is found.