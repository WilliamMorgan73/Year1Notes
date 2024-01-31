## Database Languages
A good database language should allow users to:
- Create a database
	- Define relations, attribute domains, constraints
- Basic data management
	- Insert, modify, delete data
- Perform simple and complex queries
And it should be simple and portable
- Syntax/command structure easy to learn and use
- Conform to a recognised standard
- Same language can be used with many DBMS

- **SQL (Structured Query Language)**
	- Most common database language
	- ISO/ANSI standard
	- Simple syntax
	- Two components DDL & DML
- **Data definition language (DDL)**
	- Define the **schema** for each relation (attributes)
	- Define the **domain** of each attribute (types for attribute values)
	- Specify **integrity constraints** (e.g. primary/foreign keys)
-   **Data Manipulation Language (DML)**
	- **insert / update / delete / retrieve** data from the database
	- **Query Language**: the part of the DML that involves retrieval
-   **Big picture**
- two types of DB languages:
		1. declarative
		2. procedural
	- SQL is declarative
	- query is internally transformed to procedural form
	- different possible transformations → used to optimise for performance


![[Pasted image 20240130141554.png]]

## SQL Statements

  
SQL statements consist of:
- reserved words: a fixed part of SQL
	- SELECT
	- WHERE
	- IS NOT NULL
	- operators etc.
- user-defined words/names
	- names of relations, attributes, etc.
- literals
	- non-numeric / string literals must be enclosed in 'single quotes'
	- numeric literals must not be enclosed in single quotes e.g. 142.89
	
```
		SELECT fName, lName
		FROM Staff
		WHERE staff.position != 'Assistant' AND Staff.salary > 10000
```

- Most components are case insensitive
	- Except for table names and character literals e.g., 'SMITH' != 'Smith'
- SQL is free-format
	- Line breaks, white space, and indentation do not matter
- Statements may be chained and terminated with a semi colon;
	- Termination with semicolon is required in some implementation

## Data Manipulation Language (DML)
- To create a database in MySQL:
	- Either use DDL commands
	
```
CREATE TABLE TableName (attributes);
```

- Or interactive tools - phpMyAdmin

Main statements of interest in DML

```
	- SELECT: Query data in the database
	- INSERT: Insert data into table
	- UPDATE: Update data in table
	- DELETE: Delete table
```

### Select statement

```
SELECT [ DISTINCT ] { * | column1 [AS newName] [, ...] }
FROM table1 [alias] [, ...]
[WHERE conditions]
[GROUP BY columnList]
[HAVING conditions]
[ORDER BY columnList [ ASC | DESC ]
```

### Distinct
- Normalised relations do not contain duplicate rows

```
SELECT salary
FROM Staff;
```

![[Pasted image 20240130142749.png]]

```
SELECT DISTINCT salary
FROM Staff;
```

![[Pasted image 20240130142822.png]]

#### Constructing Conditions
- Usual signs 
	- =
	- !=
	- <>
	- etc
- Range
	- x BETWEEN y AND z
- Set membership
	- IN (x, y, z, … )
- Pattern matching
	- Like 'some pattern'
- Testing for NULL
	- IS NULL
	- IS NOT NULL
- Combining conditions
	- AND
	- OR
	- NOT
##### Ranges

```
SELECT attributes
FROM table
WHERE attribute BETWEEN min AND max
```

Between does not add expressivity, equivalent to:

```
SELECT attributes
FROM table
WHERE attribute >= min AND attribute <= max
```

##### Set membership (IN)

```
SELECT attributes
FROM table
WHERE attribute IN ('x', 'y', ... )
```

Between does not add expressivity, equivalent to:

```
SELECT attributes
FROM table
WHERE attribute = x OR attribute = y
```

##### Pattern matching (Like)
Sometimes you need to search for strings that follow a certain pattern
SQL has two special pattern-matching symbols
- %
	- Represents an arbitrary sequence of zero or more characters (called wildcard, some dialects use * instead)
- _
	- Represents an arbitrary single character (some dialects use ? instead)

```
LIKE 'H%'
```
Means first character is 'H' but the rest can be anything

```
LIKE 'H _ _ _'
```
Means exactly 4 characters, the first being 'H'

```
LIKE '%e'
```
Means any string ending in 'e'

```
NOT LIKE 'H%'
```
Means first character is not 'H'

##### Combining conditions
Use parentheses to group expressions
- Technically NOT binds stronger than AND which in turn binds stronger than OR
- Using parentheses is safer and more readable

```
SELECT attributes
FROM Table
WHERE attribute NOT IN ('x', 'y') AND (attribute LIKE 'z%' OR attribute > min)
```

##### ORDER BY clause
When using SELECT, rows are not ordered
ORDER BY can be used to sort rows in ascending or descending order

```
SELECT attributes
FROM Table
ORDER BY attribute ASC/DESC
```
By default set to ascending order

##### Aggregate functions
Operate on a single column
Returns a single value

![[Pasted image 20240130144439.png]]

##### GROUP BY clause
Group by is used in combination with aggregate functions
1. First groups rows by one (or more) attributes
2. The aggregate functions are applied to each group seperately

```
SELECT attribute, Aggregate function(attribute)
FROM Table
GROUP BY attribute
```

##### As
Allows us to rename attributes, good when using aggregate functions

```
SELECT Aggregate function(attribute) AS name
```

