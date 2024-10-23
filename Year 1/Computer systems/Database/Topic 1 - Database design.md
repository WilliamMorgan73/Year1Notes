A database (DB) is a shared collection of data
Structure of the DB is self-describing (data-about-data)
Data abstraction

## Database Management Systems (DBMS)
Software system to define, create, maintain, and control access to a DB
Components in a DBMS:
- Human
	- People
		- Anyone interacting with the DBMS
	- Procedures
		- Documented instructions on how to use/run the DBMS
- Bridge
	- Data
		- Include metadata
- Machine
	- Software
		- DBMS, OS, network software, applications
	- Hardware
		- From PC to server network
### Three-level ANSI-SPARC architecture
1. Internal
2. Conceptual
3. External

![[Pasted image 20240326140017.png]]

Realises data abstraction
- Users can access the same data but different views
- Users can change views without affecting other users
- Internal structure can be changed without affecting users

#### External level
- User's views of the DB
- Multiple different views of the same data
- Adapted to specific needs
- Different entities, attributes, relationships
- Possibly derived/Calculated/Combined
#### Conceptual level
- Community view of DB
- Shared by all users
- Describes what data is stored in the DB
	- Entities attributes, relationships
	- Constraints
	- Security/Integrity information
- Logical structure of the entire DB
- Must support external views
- No storage-specific details
#### Internal level
- Physical representation of the DB
- Describes how the data is stored
- Achieve optimal
	- Runtime performance
	- Storage space utilisation
- Interface to OS
- Compression and encryption
- Not clearly separate from physical organisation

	**Database Schema**

![[Pasted image 20240326140039.png]]

DBMS handles physical organisation
We mainly focus on the conceptual level

## Database schema (Intension)
- Complete description of the DB
- Result of DB design process
- Should not change afterwards
- Multiple external (sub)schema (different views)
- One conceptual schema (All entities/attributes/relationships)
- One internal schema (Low-level description; Storage, indexes, etc)

## Database instance (Extension/state)
- Concrete data in the DB at a particular point in time
- Changes frequently (Anytime data is inserted, updated, deleted)
- Many different instances (States of a DB) may correspond to the same schema

![[Pasted image 20240326140254.png]]

![[Pasted image 20240326140308.png]]

### Logical data independence
- External schema (Views) remain the same if we change the logical structure (i.e., the schema) on the conceptual level

### Physical data independence
- Conceptual schema remains the same if we change the internal schema (data structures, algorithms, … )

### Roles
- End users
	- "Naïve"/sophisticated users
- Application developers
	- Make use of the DB for specific purpose
- Database designers
	- Logical/Physical
- Administrators
	- Data admission (DA)/ Database administrators (DBA)

### Advantages
- Control over data redundancy, consistency, standards
- Improved accessibility and productivity (Sharing of data)
- Improved security. maintenance, backup/recovery, scaling

### Disadvantages
- Complexity, size, cost
- Performance (Compared to single-purpose systems)
- Single point of failure (Because of centralisation)

## Three phases of database design
1. Conceptual
2. Logical
3. Physical

### Conceptual design
Construct a first, high level model of the data
- Use entity-relationship modelling
- Identify appropriate entities, attributes, relationships, and constraints
Based on user's requirements specification
Independent of any physical considerations
Relevant for conceptual (but also external) level
Serves as the fundamental understanding of the system

![[Pasted image 20240326140536.png]]

### Logical design
Construct the relational data model of the data
Use the conceptual design
- Map entities/relationships -> tables
Use normalisation techniques to eliminate data redundancies and anomalies

![[Pasted image 20240326140551.png]]

### Physical design
Describe the implementation of the logical design
Define specific
- Storage structures
- Access methods
- Security protection
Consider concrete usage/transaction
Optimise for performance

