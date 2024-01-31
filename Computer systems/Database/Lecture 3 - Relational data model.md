Data definition language (DDL)
- Too low-level
- Need more abstract data model to describe structure
- Should be mathematically sound
Relational data model
- Based on the concept of mathematical relations
- Relations between data are stored in tables
Schema of a relation 
$$
R:R(A_1, A_2, ..., A_n)
$$
- A = attributes
- Example
	- STUDENT (StudentNo, Prename, … )

## Terminology
Relation
- Table (With rows and columns)
- Only refers to the logical structure, not storage, etc
Attribute
- Named column in a table
- Unique name (At least in the relation)
Tuple
- A row in the table
- Holds the specific values for attributes
Domain (Of an attribute)
- Set of allowed values
Cell
- Value of specific attribute in a tuple (intersection of row and column)
Degree
- Number of attributes (#Elements in a tuple/column)
Cardinality
- Number of tuples (# of tuples/rows)
Normalised
- A relation is normalised if it's appropriately structured
- Fulfils certain conditions
- Every cell has exactly 1 value
- No repetition of identical tuples
Relational database
- A collection of normalised relations
- Each relation has a unique name


IMAGES

### Domain of an attribute
Every attribute is defined on a domain
Central place to define meaning and allowed values for an attribute
May be distinct or the same for different attributes
Semantically (in)correct operations can be (avoided) permitted

IMAGE

### NULL
Indicates the absence of a value
Represents an attribute value that is:
- Either currently unknown
- Or not applicable
Not a normal value
Has to be handled in a special way
Not the same as, 0, False, ""

### Keys
A set of attributes whose values uniquely determine a tuple
#### Candidate key
Minimal set of attributes that is a key
Minimal: You cannot drop any attribute
Not: smallest possible number of attributes

#### Primary key
One candidate key selected to identify tuples
#### Alternate key
Any candidate key that is not the primary key
#### Simple key
A key that consists of a single attribute
#### Composite key
A key that consists of multiple attributes
#### Foreign key
An attribute in a relation that must:
- Either match the primary key of another table B(relation A references relation B)
- Or be NULL

### Integrity constraints
Domain constraints for attributes
	Attribute values have to lie within their respective domain
Entity integrity
	Attributes of the PK cannot be NULL
	Guarantees that each entity has a unique identifier
	Ensures that FK values form proper references
Referential integrity
	FK must match some PK or be NULL
	Ensures references to be valid
	Prevents deleting a tuple if its referenced somewhere else

### Views
View:
	Different type of relation
	Virtual relation (not stored physically)
	Derived from one (or more) base relations
	Computed upon request by a user (at the time of request)
Main use:
	Show customised information to every user
	Compute dynamic request
Updates:
	Allowed for views that:
		- Involve only a single base relation
		- Contain either the PK or a candidate key of the base relation
		- Do not use aggregation or grouping operations

### Alternatives to the relational data model