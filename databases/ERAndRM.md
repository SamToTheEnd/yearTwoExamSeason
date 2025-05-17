# Database Concepts Simplified

## Entity-Relationship Model

**E-R Model**: A way to visually represent database design showing how data entities relate to each other.

**Entity**: A real-world object or concept that we want to store information about (e.g., Student, Course).

**Relation**: A connection between entities (e.g., Student *takes* Course).

**Weak Entity**: An entity that cannot be uniquely identified by its attributes alone and depends on another entity.

**Partial Key**: Attributes that can partially identify instances of a weak entity.

**Cardinality Constraints**: Rules specifying how many instances of one entity can relate to instances of another entity:
- One-to-one (1:1)
- One-to-many (1:N)
- Many-to-many (M:N)

**Creating an ER diagram from text description**: Process of identifying entities, relationships, attributes and constraints from a written problem statement.

**Converting an ER diagram to tables**: Transforming visual ER diagrams into relational database tables with appropriate keys and columns.

## Relational Model

**Relational Model**: A database model representing data as tables with rows and columns.

**Relational Algebra**: Mathematical query language with operations to manipulate relations:

- **Project (π)**: Select specific columns from a relation
- **Select (σ)**: Filter rows based on a condition
- **Cartesian Product (×)**: Combine every row from one relation with every row from another
- **Natural Join (⋈)**: Join relations based on common attributes
- **Rename (ρ)**: Change the name of a relation or attribute
- **Division (÷)**: Find values that match all values in another relation

## SQL (Structured Query Language)

**CREATE TABLE**: SQL command to create a new table by defining its structure and constraints.

**DROP TABLE**: SQL command to completely remove a table and all its data.

**ALTER TABLE**: SQL command to modify an existing table's structure.

**SELECT FROM**: Core SQL command to retrieve data from one or more tables.

**Aggregation Functions**: Functions that perform calculations on data:
- SUM(): Calculates the total of values
- MIN(): Finds the minimum value
- MAX(): Finds the maximum value
- AVG(): Calculates the average of values
- COUNT(): Counts the number of rows

**GROUP BY**: SQL clause that groups rows with the same values into summary rows.

**Integrity Constraints**: Rules that maintain data accuracy and consistency:
- **Super Key**: A set of attributes that can uniquely identify a tuple (row)
- **Primary Key**: Minimal super key chosen to identify entities
- **Foreign Key**: Attribute(s) that reference the primary key of another table
- **Check Constraint**: Rule that limits the values that can be placed in a column

## Normalization

**Normalization**: Process of organizing data to reduce redundancy and improve data integrity.

**Functional Dependency**: When one attribute's value determines another attribute's value (e.g., StudentID → StudentName).

**Armstrong's Axioms**: Rules for inferring all functional dependencies from a given set:
- Reflexivity: If Y is a subset of X, then X → Y
- Augmentation: If X → Y, then XZ → YZ
- Transitivity: If X → Y and Y → Z, then X → Z

**Lossless Decomposition**: Splitting a table into smaller tables without losing information.

**Redundant Attributes**: Data stored multiple times unnecessarily, creating inconsistency risks.

**Boyce-Codd Normal Form (BCNF)**: A relation where every determinant is a candidate key.

**Third Normal Form (3NF)**: A relation where no non-prime attribute is transitively dependent on the primary key.

**Normalization Process**: Analyzing dependencies and systematically removing anomalies by creating new relations.

## Transactions

**ACID Properties**: Essential properties that guarantee database transactions are processed reliably:
- **Atomicity**: A transaction is all or nothing
- **Consistency**: A transaction brings the database from one valid state to another
- **Isolation**: Concurrent transactions don't interfere with each other
- **Durability**: Completed transactions survive system failures

**Schedules**: Sequences of operations from multiple transactions.

**Serializable Schedule**: Schedule that produces the same result as if transactions were executed in some sequential order.

**Schedule Evaluation**: Process of determining if a schedule is serializable and free from anomalies.