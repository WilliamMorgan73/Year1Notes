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

**SQL (Structured Query Language)**
- Most common database language
- ISO/ANSI standard
- Simple syntax
- Two components DDL & DML

**Data definition language (DDL)**
- Define the **schema** for each relation (attributes)
- Define the **domain** of each attribute (types for attribute values)
- Specify **integrity constraints** (e.g. primary/foreign keys)

**Data Manipulation Language (DML)**
- **insert / update / delete / retrieve** data from the database
- **Query Language**: the part of the DML that involves retrieval

Two types of DB languages:
	1. declarative
	2. procedural

SQL is declarative
Query is internally transformed to procedural form
Different possible transformations → used to optimise for performance

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

### Salary Table with Duplicate Values

| employee_id | employee_name | salary |
| ---- | ---- | ---- |
| 1 | John Doe | 50000 |
| 2 | Jane Smith | 60000 |
| 3 | Bob Johnson | 55000 |
| 4 | Alice Brown | 60000 |
| 5 | Charlie Green | 50000 |

```
SELECT DISTINCT salary
FROM Staff;
```

| employee_id | employee_name | salary |
| ---- | ---- | ---- |
| 1 | John Doe | 50000 |
| 3 | Bob Johnson | 55000 |
| 4 | Alice Brown | 60000 |

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

- SUM
	- Sum of numeric values in column
- AVG
	- Average value of given column
- MIN
	- Smallest value in column
- MAX
	- Largest value in column
- COUNT
	- Total number of values in column (excluding NULL)
- COUNT( * )
	- Number of rows in a table (Includes NULL)

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

# Lecture 8
## Joins: Inner and Outer
### Inner Join
JOIN ON
	Efficient and general solution

```
[INNER] JOIN ON <matching_criterion>
```

Without using JOIN

```
SELECT *
FROM Tables
WHERE attribute1 = attribute2;
```

JOIN USING: Shorthand/syntactic sugar
	Not implemented by all DBMS

```
SELECT *
FROM Table JOIN Table 2 using attribute;
```

All matching combinations
#### Example

Suppose we have two tables: `employees` and `departments`. The inner join result would look like this:

|employee_id|employee_name|department_name|
|---|---|---|
|1|John Doe|IT|
|2|Jane Smith|HR|
|3|Bob Johnson|Finance|

### Left Join

```
LEFT [OUTER] JOIN ON <matching_criterion>
```

All matching combinations +
Missing records from left table

#### Example
For a left join where we want to include all employees and their corresponding departments:

|employee_id|employee_name|department_name|
|---|---|---|
|1|John Doe|IT|
|2|Jane Smith|HR|
|3|Bob Johnson|Finance|
|4|Alice Brown|NULL|
### Right Join

```
RIGHT [OUTER] JOIN ON <matching_criterion>
```

All matching combinations +
Missing records from right table

#### Example

For a right join where we want to include all departments and their associated employees:

|employee_id|employee_name|department_name|
|---|---|---|
|1|John Doe|IT|
|2|Jane Smith|HR|
|3|Bob Johnson|Finance|
|NULL|NULL|Marketing|

### Full Join

```
FULL [OUTER] JOIN ON <matching_criterion>
```

All matching combinations +
missing records from both tables

#### Example
For a full join where we want to include all records from both tables:

|employee_id|employee_name|department_name|
|---|---|---|
|1|John Doe|IT|
|2|Jane Smith|HR|
|3|Bob Johnson|Finance|
|4|Alice Brown|NULL|
|NULL|NULL|Marketing|

This table includes all employees and departments, even if there is no match in one of the tables.

### Subqueries
You can reuse the result of one query in another query
Three types of subqueries
1. A single-value (scaler) subquery
2. A multi-value subquery
3. A tabular subquery
#### Single-Value
Single column and single row

```
SELECT AGGREGATE(*) AS name
FROM Table
WHERE attribute = (SELECT attribute 
		FROM Table
		WHERE Condition);
```

#### Multi-value subquery
Single column and multiple rows

```
SELECT attribute
FROM Table
WHERE attribute = (SELECT attribute 
		FROM Table
		WHERE  (SELECT attribute 
				FROM Table
				WHERE Condition));
```
#### Tabular subquery
Multiple columns and multiple rows

```
SELECT attributes
FROM Table
WHERE Condition;
```

## Data Manipulation Language (DML)
Commands for modifying data in the DB

### Insert

```
INSERT INTO Table [(ColumnList)]
VALUES (ValueList)
WHERE Condition;
```
### Modify

```
UPDATE Table
SET ColumnName = dataValue
WHERE Condition;
```
### Delete

```
DELETE FROM Table
WHERE Condition
```

### Create
Create a new table

```
CREATE Table name (
    column1 datatype1,
    column2 datatype2,
    ...,
    PRIMARY KEY (column1)
);
```

### Alter
Alter a table

```
ALTER TABLE name
ADD colummn datatype;
```

### Drop
Delete entire table

```
DROP TABLE Table;
```

### Create View
Define a virtual table that appears to the user

```
CREATE VIEW Name AS
SELECT Columns
FROM Table
WHERE Condition;
```

### Main Domain Types in SQL
- CHAR(n)
	- Character string of fixed length n
- VARCHAR(n)
	- Character string of length at most n
- BIT(n)
	- Bit string of fixed length n
- INTEGER
	- Large $\pm$ Integer
- SMALLINT
	- Small $\pm$ integer value (Up to 32767)
- NUMERIC( p , d )
	- Positive/Negative decimal number with at most
	- precision p
		- Total number of digits
	- scale d
		- Number of decimal digits

We can define our own custom domain types and

```
CREATE DOMAIN name AS type
CHECK (VALUE IN ('values'))
```

Values can be a query

### Integrity and referential constraints
You can specify integrity & referential constraints when creating a table
- Primary key
- Foreign key
And specify what to do with foreign key when the corresponding PK is updated/Deleted
- ON UPDATE
- ON DELTE

Available options for these actions
- CASCADE
	- Delete the FK/ Delete the tuple
- SET NULL
	- Set to NULL
- SET DEFAULT
	- Set to default value
- NO ACTION
	- Do nothing
	- Dangerous