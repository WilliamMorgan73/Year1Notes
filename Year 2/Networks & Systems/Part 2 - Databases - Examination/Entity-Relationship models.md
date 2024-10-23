Data models are collections of intuitive concepts describing data, their relationships and constraints
# Entity-relationship (ER) model
Top down approach to database design
- graphical description of database
Basic concepts:
- The important data objects (entities)
- the important properties of the entities (attributes)
- the associations between the entities (relationships) 
Furthermore:
- constraints on the entities, relationships, and attributes
Several notations for representing the ER model
- Unified Modeling Language (UML) (most popular diagrammatic notation)

## Entities
Entity type:
- group of objects with the same properties, identified as having independent existence, e.g.: ‘Client’
Entity occurrence:
- a uniquely identifiable instance e.g.: a specific Client called ‘James Smith’
- We use ‘entity’ when the meaning is clear from the context
Diagrammatic representation of entities:
- a rectangle labelled by the name of the entity type

![[Entities.png]]
## Relationships
Relationship (type):
- a meaningful association between two (or more) entity types
Degree of a relationship:
- the number of entities that participate in a relationship
Diagrammatic representation of binary relationships:
- a line connecting the participating entities, labelled by the name of the relationship (has also a direction)

![[Relationship.png]]
When n-ary relationships we use:
- A diamond labelled by the name of the relationship connecting the participating entities

![[n-ary relationship.png]]
When they have degree 1:
- We need role names to indicate the purpose of each entity occurrence in the relationship

![[Recursive relationship.png]]
## Attributes
a descriptive property of an entity or relationship
Attribute domain
- the set of allowable attribute values
Attributes may be:
- simple / composite (e.g.: ‘salary’ / ‘address’)
- single-valued / multi-valued (e.g.: ‘staffNo’ / ‘telNumbers’)
- sometimes derived (e.g.: ‘age’ is derived by ‘dateOfBirth’)
- Null valued

### Candidate key:
- a minimal set of attributes, whose values uniquely identify an entity occurrence
- cannot be null

### Primary key:
- we choose exactly one candidate key

Simple composite key
- A candidate key that consists of one (many) attribute(s)

Factors for choice of primary key
- number of attributes (preferably smaller)
- attribute length (preferably smaller)
- future certainty of uniquenes

## Attributes on Entities
Diagrammatic representation
- Divide the rectangle of the entity into two parts
	- The upper part has the entity name
	- The lower part has the list of attributes
- The primary key is usually
	- Underlined 
	- Labelled {PK}

![[PK diagram.png]]
## Multiplicity
Number of entity occurrences, to which another entity can be associated with this relationshi

Relationships can be:
- One-to-one (1:1)
- One-to-many (1:$*$)
- Many-to-many($*:*$)

![[Multiplicity1.png]]
![[Multiplicity2.png]]

## Problems with the ER model
Limiting when modelling modern and complex DB applications with large amounts of data
### Solutions:
- Additional semantic modelling concepts
	- Reduce the complexity of the ER model
	- More intuitive
	- Enhanced ER diagrams (EER)

The main concepts of the EER model are:
- Specialization
- Generalization

# The Enhanced ER (EER) model
Subclass
- A subgrouping of occurrences of an entity type, which requires to be represented separately
Superclass
- An entity type that has two or more distinct subclasses

Superclass/subclass relationship
- Each member of a subclass is also a member of the superclass

## Attribute inheritance
All attributes of the superclass are also attributes of the subclasses
A subclass has additional attributes than its superclass

## Type hierarchy
An entity with its subclasses and their subclasses
Type hierarchy is also known as:
- Specialization hierarchy
- Generalization hierarchy
- IS-A hierarchy

Main advantages of the EER model
- Avoid describing similar concepts more than once
- Have relations that include a subclass but not in the superclass
- More semantic information to the design

## Specialization 
The top down process of maximizing the differences between entity occurrences by identifying their distinguishing characteristics
Giving superclass(es), it leads to identifying subclasses

## Generalization#
The bottom-up process of minimizing the differences between entity occurrences, by identifying their common characteristics
Given subclasses, it leads to identifying superclass(es)

### Diagrammatic representation
The subclasses are attached by lines to a triangle that points towards the superclass

![[generalization-specialization.png]]
### Constraints
Participation constraint
- Determines whether every member in the superclass must participate as a member of a subclass or not
- Can be mandatory or optional

Disjoint constraint
- Determines whether a member of a superclass can be a member of one or more subclasses
	- or
	- and

Diagrammatically

![[constraints EERD.png]]