## Stacks
A stack is a collection of objects that are inserted and removed according to the **last-in-first-out (LIFO)** principle

### Methods
- push(e)
	- Insert element *e* at the top of the stack

```
push(e)
---------------------------------------------------
if size = N then
	throw a FullStackException
end if
t = t + 1
S[t] = e
```

- pop
	- Remove and return the top element of the stack
	- Error occurs if stack is empty

```
pop
----------------------------------------------------
if isEmpty then
	throw a EmptyStackException
end if
e = S[t]
S[t] = NULL
t = t - 1
return e
```

- size
	- Return the number of elements in the stack

```
size
-----------------------------------------------------
return t+1
```

- isEmpty
	- Return a Boolean indicating if the stack is empty

```
isEmpty
-------------------------------------------------------
return (t<0)
```

- top
	- Return the top element in the stack without removing it
	- Error occurs if stack is empty

```
top
----------------------------------------------------------
if isEmpty then
	throw a EmptyStackException
end if
return S[t]
```

### Implementation using arrays
In an array based implementation, the stack consists of:
- An N-element array S.
- Integer variable *t* that gives the top element of the stack
- Initialise *t* to -1 to identify an empty stack


The array based implementation is time efficient - Dependent on the stack
The fixed size N can be a limitation - Can waste memory of generate an exception (if size exceeded)

## Queues
A queue is a collection of objects that are inserted and removed according to the **first-in-first-out (FIFO)** principle

Elements removed from the front of the queue
Elements added to the back of the queue

### Methods
- enqueue(e)
	- Insert element *e* at the rear of the queue

```
enqueue(e)
---------------------------------------------------
if size = N - 1 then
	throw a FullQueueException
end if
Q[r] = e
r = r + 1 mod N
```

- dequeue
	- Remove and return from the queue the element at the front
	- An error occurs if the queue is empty

```
dequeue
----------------------------------------------------
if isEmpty then
	throw a EmptyQueueException
end if
temp = Q[f]
Q[f] = NULL
f = f + 1 mod N
return temp
```

- size
	- Return the number of elements in the queue

```
size
-----------------------------------------------------
return (r-f) mod N
```

- isEmpty
	- Returns a Boolean indicating if the queue is empty

```
isEmpty
-------------------------------------------------------
return (f=r)
```

- front
	- Return the front element without removing it
	- An error occurs if the queue is empty

```
front
----------------------------------------------------------
if isEmpty then
	throw a EmptyQueueException
end if
return Q[f]
```

### Implementation using arrays
Use 2 variables:
1. front
2. rear

Initially we assign $f=r=0$ indicating the queue is empty
After each enqueue operation, increment r - Can wrap around to stop array-out-of-bounds error
After each dequeue operation, we increment f

