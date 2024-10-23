# Question 1
**Calculate value-to-weight ratio**
$$\frac{v_1}{w_{1}}=\frac{25}{5}=5$$
$$\frac{v_2}{w_{2}}=\frac{120}{60}=2$$
$$\frac{v_{3}}{w_{3}}=\frac{50}{50}=1$$
$$\frac{v_4}{w_4}=\frac{25}{50}=0.5$$
$$\frac{v_5}{w_{5}}=\frac{60}{40}=1.5$$
**Sort items by value-to-weight**
1. $v_{1}$
2. $v_2$
3. $v_{5}$
5. $v_{3}$
6. $v_4$

**Select items greedily based on the sorted order**

1. **Item 1**: Entire item can be taken
    Remaining capacity: $100−5=95$
    Total value: $25$
    
2. **Item 2**: Entire item can be taken 
    Remaining capacity: $95−60=35$
    Total value: $25+120=145$
    
3. **Item 5**: We can't take the full item
    The value of 35 units of weight: $\frac{60}{40}\times35=52.5$
    Remaining capacity: $35−35=0$
    Total value: $145+52.5=197.5$
    

**Final result**

The total value obtained from the fractional knapsack is $197.5$.

# Question 2
Take item 2 and item 5

# Question 3
#### 1. **Compute Ratios**:

First, compute the value-to-weight ratio for each item:

$$r_{i}=\frac{v_{i}}{w_{i}}$$

Store these ratios along with their corresponding items (values and weights).

#### 2. **Apply PARTITION***:

Using the PARTITION algorithm, you can partition the list of ratios, such that items with larger ratios are moved to one side of the list. This allows us to iteratively select items with the largest value-to-weight ratio without sorting.

This reduces the average running time to $O(n)$

# Question 4
