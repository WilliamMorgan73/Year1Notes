Relations are considered as sets of elements
- An element is a tuple of attribute values
- Each row in a table specifies one element of the set

Relational Calculus (declarative):
- Uses set theoretic expressions (predicate calculus / first-order logic)
- Defines a new set based on (one or more) existing ones

Relational Algebra (Procedural):
- Uses operators to construct a new set from (one or more) existing ones

Relational calculus and algebra are equivalent languages
- They can be used to define/create the same sets
- For every calculus expression there is one (or more) algebraic expressions

Non-user-friendly
- Used as formal basis to define and compare querying languages

Most modern query languages (like SQL):
- Are relational complete
	- Can produce any relation that relational algebra/calculus can
- Have additional operations (e.g., summing, grouping, ordering)
	- They have more expressive power than relational algebra/calculus
- But still not Turing complete
	- Not as powerful as general programming languages

# Relational Calculus
**Predicate**:
- A function that returns true/false when arguments are given
**Proposition**
- The expression obtained when replacing values for the arguments of a predicate
- (i.e. a proposition is either true or false)

Let $P(x)$ and $Q(x)$ be two predicates with argument $x$. Then:
	The set of all $x$ such that both $P(x)$ **and** $Q(x)$ are true is:
$$\{x | P(x) \wedge Q(x)\}$$
	The set of all $x$ such that $P(x)$ **or** $Q(x)$ are true is:
$$\{ x | P(x) \vee Q(x)\}$$
	The set of all $x$ such that $P(x)$ is **not** true is:
$$	\{ x | \sim P(x) \}$$
**Tuple versus Domain relational Calculus**
**Tuple relational calculus**
- The one we focus on
- More similar to SQL
- Variables values are tuples
- Notation
$$\{ t | P(t) \}$$
- Example 
	- Select all tuples from relation $R$, for which predicate $P$ holds
$$\{t | R(t) \wedge P(t)\}$$
- Example
	- Select all $A$ from relation $R(A,B)$, for which the value of $B>0$
$$\{ t.A |R(t) \wedge t.B >0 \}$$
**Domain Relational Calculus**
- More similar to mathematical notation
- Variables' values are attribute values from a specific domain
- Notation
$$\{ a_1, ...,a_n | P(a_1, ..., a_n) \}$$
Example 
	- Select all tuples from relation $R$, for which predicate $P$ holds
$$\{ a_1, ...,a_n | R(a_1, ..., a_n) \wedge P(a_1, ..., a_n)\}$$
- Example
	- Select all $A$ from relation $R(A,B)$, for which the value of $B>0$
$$\{ a | (\exists b)(R(a,b) \wedge b>0) \}$$
## Tuple relational Calculus
- Variable values are tuples
- To specify that tuple $s$ should be **in relation Name** use as predicate:
$$Table(s)$$
- Use $s.element$ for a name element in tuple $s$
- Use quantifiers for more complex predicates:
	- Existential quantifier: $\exists$
	- Universal quantifier $\forall$
**Examples**
- all tuples s of the relation Staff with attribute salary > 10000
$$\{𝑠 | Staff(s) \wedge 𝑠. 𝑠𝑎𝑙𝑎𝑟𝑦 > 10000\}$$
- the salaries of all members of staff who earn more than 10000
$$\{𝑠.𝑠𝑎𝑙𝑎𝑟𝑦 | Staff(𝑠) \wedge 𝑠.𝑠𝑎𝑙𝑎𝑟𝑦 > 10000\}$$
- the names of all staff who work in a branch in London
$$\{𝑠. 𝑛𝑎𝑚𝑒 | Staff(s) ∧ (\exists 𝑏)(Branch(𝑏)\wedge (𝑏. 𝑏𝑟𝑎𝑛𝑐ℎ𝑁𝑜 = 𝑠. 𝑏𝑟𝑎𝑛𝑐ℎ𝑁𝑜)\wedge (𝑏. 𝑐𝑖𝑡𝑦 = ′London′))\}$$

# Relational Algebra
Procedural
	Specifies operations to construct a new set from existing ones

**Basic operations**


| Unary | Binary |
| ---- | ---- |
| Selection (𝜎) | Union (⋃) |
| Projection (𝜋) | Set Difference (−) |
| Rename (𝜚) | Cartesian product (×) |
Several derived operations
- Intersection $\cap$
- Division $\div$
- Join ( $\Join$ Natural join, equi-join, theta join, outer join, semi-join)

## Selection
$\theta_{condition} (R)$
- Unary operation - Operates on a single relation
- Select the subset of **tuples** from $R$ that satisfy the specified **condition**/predicate
- Corresponding to SQL:
```
SELECT *
FROM R
WHERE <Condition>
```

**Example**
List all staff whose salary is greater than $12000$

**Staff table**

| staffNo | fName | lName | position  | gender | DOB        | salary | branchNo |
|---------|-------|-------|-----------|--------|------------|--------|----------|
| SA9     | Mary  | Howe  | Assistant | F      | 1970-02-19 | 9000   | B007     |
| SG14    | David | Ford  | Supervisor| M      | 1958-03-24 | 18000  | B003     |
| SG37    | Ann   | Beech | Assistant | F      | 1960-11-10 | 12000  | B003     |
| SG5     | Susan | Brand | Manager   | F      | 1940-06-03 | 24000  | B003     |
| SL21    | John  | White | Manager   | M      | 1945-10-01 | 30000  | B005     |
| SL41    | Julie | Lee   | Assistant | F      | 1965-06-13 | 9000   | B005     |
$\theta_{salary > 12000} (Staff)$

| staffNo | fName | lName | position  | gender | DOB        | salary | branchNo |
|---------|-------|-------|-----------|--------|------------|--------|----------|
| SG14    | David | Ford  | Supervisor| M      | 1958-03-24 | 18000  | B003     |
| SG5     | Susan | Brand | Manager   | F      | 1940-06-03 | 24000  | B003     |
| SL21    | John  | White | Manager   | M      | 1945-10-01 | 30000  | B005     |
## Projection
$\Pi_{col1, col2, ...}(R)$
- Unary operations (operates on a single relation)
- Selects the specified subset of **attributes** from $R$
- Eliminates duplicates (different from SQL!)
- Corresponding SQL:
```
SELECT DISTINCT col1, col2, ...
FROM R
```
**Example**
For all staff, list $staffNo$, $fName$, $lName$, and $salary$.
**Staff table**

| staffNo | fName | lName | position  | gender | DOB        | salary | branchNo |
|---------|-------|-------|-----------|--------|------------|--------|----------|
| SA9     | Mary  | Howe  | Assistant | F      | 1970-02-19 | 9000   | B007     |
| SG14    | David | Ford  | Supervisor| M      | 1958-03-24 | 18000  | B003     |
| SG37    | Ann   | Beech | Assistant | F      | 1960-11-10 | 12000  | B003     |
| SG5     | Susan | Brand | Manager   | F      | 1940-06-03 | 24000  | B003     |
| SL21    | John  | White | Manager   | M      | 1945-10-01 | 30000  | B005     |
| SL41    | Julie | Lee   | Assistant | F      | 1965-06-13 | 9000   | B005     |

$\Pi_{staffNo, fName, salary}(Staff)$

| staffNo | fName | lName | salary |
|---------|-------|-------|--------|
| SA9     | Mary  | Howe  | 9000   |
| SG14    | David | Ford  | 18000  |
| SG37    | Ann   | Beech | 12000  |
| SG5     | Susan | Brand | 24000  |
| SL21    | John  | White | 30000  |
| SL41    | Julie | Lee   | 900    |
## Combining Selection and Projection
We can combine operations
$$\Pi_{col1,col2,...}(\Theta_{predicate}(R)) \; or \; \Theta_{predicate}(\Pi_{col1,col2,...}(R))$$
- Outer operation is applied to the result of the inner operation
- Corresponding SQL:
```
SELECT DISTINCT col1, col2, ...
FROM R
WHERE <Condition>
```
**Example**
List $staffNo$, $fName$, $lName$, and $salary$ of all staff with a salary greater than 120000

**Staff table**

| staffNo | fName | lName | position  | gender | DOB        | salary | branchNo |
|---------|-------|-------|-----------|--------|------------|--------|----------|
| SA9     | Mary  | Howe  | Assistant | F      | 1970-02-19 | 9000   | B007     |
| SG14    | David | Ford  | Supervisor| M      | 1958-03-24 | 18000  | B003     |
| SG37    | Ann   | Beech | Assistant | F      | 1960-11-10 | 12000  | B003     |
| SG5     | Susan | Brand | Manager   | F      | 1940-06-03 | 24000  | B003     |
| SL21    | John  | White | Manager   | M      | 1945-10-01 | 30000  | B005     |
| SL41    | Julie | Lee   | Assistant | F      | 1965-06-13 | 9000   | B005     |

$\Pi_{staffNo,fName,lName, salary}(\Theta_{salary>12000}(Staff))$

| staffNo | fName | lName | salary |
|---------|-------|-------|--------|
| SG14    | David | Ford  | 18000  |
| SG5     | Susan | Brand | 24000  |
| SL21    | John  | White | 30000  |
## Union
$A \cup B$
- Binary operation (operates on a two relations)
- Selects tuples that are in A **or** in B
- Adds up tuples from both relations
- Corresponding SQL:
```
SELECT ...
UNION [ALL]
SELECT ...
```
**Example**
List all cities where there is either a branch or a property.

**Branch table**

| branchNo | city     |
|----------|----------|
| B005     | London   |
| B007     | Glasgow  |
| B003     | Bristol  |

**Property table**

| propertyNo | city     |
|------------|----------|
| P15        | Aberdeen |
| P98        | London   |
| P21        | Glasgow  |
$\Pi_{city}(Branch) \cup \Pi_{city}(Property)$

| city       |
|------------|
| Aberdeen   |
| London     |
| Glasgow    |
| Bristol    |
### Union compatibility
To compute $A \;cup \; B$ or $A-B$ or $A \; \cap \; B$
- The schemata of $A$ and $B$ must match
	- They must have the **same number of attributes**
	- Each pair of matching attributes must have the **same domain**
	- Attributes **names are ignored**
- $A$ and $B$ are then called **union compatible**

What if one of the relations has **additional attributes**
- Use projection to create union-compatible relations

$$\Pi_{city}(Property) \; \cup \; \Pi_{city}(Branch)$$
$$\Pi_{city}(Property) \; - \; \Pi_{city}(Branch)$$
$$\Pi_{city}(Property) \; \cap \; \Pi_{city}(Branch)$$
## Set difference
$A- B$
- Binary operation (operates on a two relations)
- **Selects** all tuples from (a copy of) $A$ that are also in $B$
- Corresponding to SQL:
```
SELECT ...
{MINUS | EXCEPT}
SELECT ...
```
**Example**
List all cities where there is a property but not a branch
$$\Pi_{city}(Property) \; - \; \Pi_{city}(Branch)$$
**Branch table**

| branchNo | city     |
|----------|----------|
| B005     | London   |
| B007     | Glasgow  |
| B003     | Bristol  |

**Property table**

| propertyNo | city     |
|------------|----------|
| P15        | Aberdeen |
| P98        | London   |
| P21        | Glasgow  |
$\Pi_{city}(Property) - \Pi_{city}(Branch)$

| city |
| ---- |
| Aberdeen |
## Intersection

$A\cap B$
- Binary operation (operates on a two relations)
- **Selects** tuples from  $A$ **and** $B$
- Corresponding to SQL:
```
SELECT ...
INTERSECT
SELECT ...
```
**Example**
List all cities where there is a branch and a property
$$\Pi_{city}(Property) \; \cap \; \Pi_{city}(Branch)$$
**Branch table**

| branchNo | city     |
|----------|----------|
| B005     | London   |
| B007     | Glasgow  |
| B003     | Bristol  |

**Property table**

| propertyNo | city     |
|------------|----------|
| P15        | Aberdeen |
| P98        | London   |
| P21        | Glasgow  |
$\Pi_{city}(Property) - \Pi_{city}(Branch)$

| city |
| ---- |
| London |
| Glasgow |

Intersection is a derived operation
$$A \cap B = A -(A-B) = B-(B-A)$$
## Cartesian Product
$A \times B$

- Binary operation (operates on two relations)
- Generates **all possible combinations** of tuples in A and in B by concatenating them
- Results in $r_A \times r_B$ tuples with $c_A + c_B$ attributes
	- (r: number of rows, c: number of columns)
- **No compatibility requirements** on $A$ and 'B'
- Attributes with the same name are **prefixed** with relation name
- Corresponding SQL:
```
SELECT * FROM A, B

or

SELECT * FROM A CROSS JOIN B
```
**Example**
**Branch table**

| branchNo | city     |
|----------|----------|
| B005     | London   |
| B007     | Glasgow  |
| B003     | Bristol  |

**Property table**

| propertyNo | city     |
|------------|----------|
| P15        | Aberdeen |
| P98        | London   |
| P21        | Glasgow  |

$Property \times Branch$

| propertyNo | Property.city | branchNo | Branch.city |
|------------|---------------|----------|-------------|
| P15        | Aberdeen      | B005     | London      |
| P98        | London        | B005     | London      |
| P21        | Glasgow       | B005     | London      |
| P15        | Aberdeen      | B007     | Glasgow     |
| P98        | London        | B007     | Glasgow     |
| P21        | Glasgow       | B007     | Glasgow     |
| P15        | Aberdeen      | B003     | Bristol     |
| P98        | London        | B003     | Bristol     |
| P21        | Glasgow       | B003     | Bristol     |
Often we are only interested in specific combinations
- Use select operation to filter for criterion
- Corresponding SQL:
```
SELECT *
FROM A CROSS JOIN B
WHERE <criterion>

or

SELECT *
FROM A JOIN B ON <criterion>
```
**Example**
List all combinations of properties and branches in the same city

**Branch table**

| branchNo | city     |
|----------|----------|
| B005     | London   |
| B007     | Glasgow  |
| B003     | Bristol  |

**Property table**

| propertyNo | city     |
|------------|----------|
| P15        | Aberdeen |
| P98        | London   |
| P21        | Glasgow  |
$\Theta_{Property.city = Branch.city}(Property \times Branch)$

| propertyNo | Property.city | branchNo | Branch.city |
|------------|---------------|----------|-------------|
| P98        | London        | B005     | London      |
| P21        | Glasgow       | B007     | Glasgow     |
## Rename
- Algebraic expressions quickly become very complex
	- Decompose them into a series of smaller operations
	- Give names to the intermediate expressions to reuse them
	- Can use the assignment operation: $Name \leftarrow \; <expression>$
	- But this creates multiple expressions
- An alternative is the rename operation
	- $P_Y(X)$ return $X$ renamed as $Y$
	- $P_{Y(A,B,C,...)}(X)$ returns $X$ named as $Y$ with attributes renamed as $A,B,C,...$
- When is that useful
	- When **reusing the same relation** in different roles
**Example**
Who are the grandparents (parents-of-parents) of Thomas?
**A**

| Parent | Child |
|--------|-------|
| Mary   | Thomas|
| Peter  | Mary  |
| Sarah  | Nick  |
| Nick   | Thomas|
| Andrew | Nick  |
| Nick   | Helen |
| Kate   | Mary  |
**B**

| Parent | Child |
|--------|-------|
| Mary   | Thomas|
| Peter  | Mary  |
| Sarah  | Nick  |
| Nick   | Thomas|
| Andrew | Nick  |
| Nick   | Helen |
| Kate   | Mary  |

**Family**

| Parent | Child |
|--------|-------|
| Mary   | Thomas|
| Peter  | Mary  |
| Sarah  | Nick  |
| Nick   | Thomas|
| Andrew | Nick  |
| Nick   | Helen |
| Kate   | Mary  |

$\Pi_{A.Parent}(\Theta_{(A.Child=B.parent \wedge B.Child='Thomas')}(\rho_A(Family) \times \rho_B(Family)))$

**Example 2**
Find the largest salary
**Staff**

| staffNo | fName | lName | position  | gender | DOB        | salary | branchNo |
|---------|-------|-------|-----------|--------|------------|--------|----------|
| SA9     | Mary  | Howe  | Assistant | F      | 1970-02-19 | 9000   | B007     |
| SG14    | David | Ford  | Supervisor| M      | 1958-03-24 | 18000  | B003     |
| SG37    | Ann   | Beech | Assistant | F      | 1960-11-10 | 12000  | B003     |
| SG5     | Susan | Brand | Manager   | F      | 1940-06-03 | 24000  | B003     |
| SL21    | John  | White | Manager   | M      | 1945-10-01 | 30000  | B005     |
| SL41    | Julie | Lee   | Assistant | F      | 1965-06-13 | 9000   | B005     |
- First find all that are **not** the largest
$$NotLargest \leftarrow \Pi_{Staff.salary}(\Theta_{Staff.salary<Other.Salary}(Staff \times \rho_{Other}(Staff))) $$

| salary |
|--------|
| 9000   |
| 18000  |
| 12000  |
| 24000  |
| 9000   |
| 30000  |

- Then only keep the rest
$$\Pi_{Staff.Salary}(Staff)-NotLargest$$

| salary |
|--------|
| 30000  |
## Division
$A \div B$
- Binary operation (operates on two relations)
- Only keep tuples from A that exist in all possible combinations with B
- Non-basic and not part of SQL but appears often in applications

**Example**
Which clients have viewed **all** properties with three rooms?

$\Pi_{Client.No, PropertyNo}(Viewing)$

| ClientNo | propertyNo |
| ---- | ---- |
| CR56 | PA14 |
| CR76 | PG4 |
| CR56 | PG4 |
| CR62 | PA14 |
| CR56 | PG34 |

$\Pi_{propertyNo}(\Theta_{rooms=3}(Property)))$

| PropertyNo |
| ---- |
| PG4 |
| PG36 |

$\Pi_{Client.propertyNo}(Viewing) \div \Pi_{PropertyNo}(\Theta_{rooms=3}(Property)))$

| ClientNo |
| ---- |
| CR56 |
Why is it called division?
- $(A \div B) \times B$ is the relevant part of $A$

| ClientNo | propertyNo |
| ---- | ---- |
| CR56 | PG4 |
| CR56 | PG36 |

B has a subset of attributes from $A: A(X_1, X_2,...,Y_1,Y_2,...)$ and $B(Y_1,Y_2,...)$
Find all possible combinations
Only keep tuples and attributes that are in A
- Find combinations that are not in A
- Project to attributes that are only in A
- Remove them from A

$$A \div B = \Pi_{X1, X2, ...}(A)\;  – \; \Pi_{X1, X2, ...} \; ((\Pi_{X1, X2, ...}(A) \times B) \; - A)$$
$\Pi_{X_1,X_2,...}$ projecting down
$(\Pi_{X1, X2, ...}(A) \times B)$ All combinations
$((\Pi_{X1, X2, ...}(A) \times B) \; - A)$ Combinations not in A

## Joins
- $A [INNER] \; JOIN \;  B \; ON \; <criterion>$
	- Theta join $( \Theta-join)$  for general criterion $\Theta$
	- Equijoin: some equality criterion
	- Natural join: equijoin over all common attributes
	- Semijoin: inner join & project to attributes of the left relation

**Table A**
$A \Join_{attr1=attr2} B$

| id1  | attr1 |
|------|-------|
| A    | X     |
| B    | Y     |
| C    | Z     |

**Table B**

| id2 | attr2 |
| ---- | ---- |
| 1 | W |
| 2 | X |
**Inner**

| id1 | attr1 | id2 | attr2 |
| ---- | ---- | ---- | ---- |
| A | X | 2 | X |
- $A \; LEFT \; [OUTER] \; JOIN \; B \; ON \; <criterion>$
$A\Join_{attr1=attr2} B$
**Left**

| id1 | attr1 | id2 | attr2 |
| ---- | ---- | ---- | ---- |
| A | X | 2 | X |
| B | Y | NULL | NULL |
| C | Z | NULL | NULL |


- $A \; RIGHT \; [OUTER] \; JOIN \; B \; ON \; <criterion>$
$A\Join_{attr1=attr2} B$
**Right**

| id1 | attr1 | id2 | attr2 |
| ---- | ---- | ---- | ---- |
| A | X | 2 | X |
| NULL | NULL | 1 | W |
- $A \; FULL \; [OUTER] \; JOIN \; B \; ON \; <criterion>$
$A\Join_{attr1=attr2} B$
**FULL**

| id1 | attr1 | id2 | attr2 |
| ---- | ---- | ---- | ---- |
| A | X | 2 | X |
| B | Y | NULL | NULL |
| C | Z | NULL | NULL |
| NULL | NULL | 1 | W |
