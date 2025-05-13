


## Relational Algebra

### Basic Operations

1. **Selection (σ)**: Selects rows based on a condition
    - Example: σ<sub>name = "John"</sub>(user)

2. **Projection (π)**: Selects specific columns
    - Example: π<sub>book_id</sub>(owns)

3. **Cartesian Product (×)**: Combines all rows from two relations
    - Example: user × book

4. **Natural Join (⋈)**: Joins tables on matching column names
    - Example: user ⋈ owns

5. **Join (⋈<sub>condition</sub>)**: Joins tables based on a condition
    - Example: user ⋈<sub>user.user_id = owns.user_id</sub> owns

6. **Union (∪)**: Combines rows from two compatible relations
    - Example: π<sub>user_id</sub>(R1) ∪ π<sub>user_id</sub>(R2)

7. **Set Difference (−)**: Returns rows in first relation but not in second
    - Example: π<sub>user_id</sub>(R1) − π<sub>user_id</sub>(R2)

8. **Intersection (∩)**: Returns rows present in both relations
    - Example: π<sub>user_id</sub>(R1) ∩ π<sub>user_id</sub>(R2)

### Complex Query Example

To find users who booked tickets with both "North Line" and "Eastern" operators:

```
(π₁user_id(σoperator="North Line"(trip ⋈ booking)) ∩ π₁user_id(σoperator="Eastern"(trip ⋈ booking)))
```

## SQL Queries and Operations

### Data Manipulation (DML)

#### SELECT Queries

Basic structure:
```sql
SELECT column(s)
FROM table(s)
WHERE condition
GROUP BY column(s)
HAVING condition
ORDER BY column(s) [ASC|DESC];
```

Examples:

1. **Basic Selection**: Get all users with more than 2000 points
```sql
SELECT name, points 
FROM user 
WHERE points > 2000 
ORDER BY points ASC;
```

2. **Join**: Get books owned by a specific user
```sql
SELECT book.title, book.price
FROM book JOIN owns ON book.book_id = owns.book_id
WHERE owns.user_id = 102;
```

3. **Aggregation**: Count books owned by each user
```sql
SELECT book.title, SUM(owns.copies) AS total_copies
FROM book JOIN owns ON book.book_id = owns.book_id
GROUP BY book.title;
```

4. **Complex Query**: Users who booked trips with at least 5 different operators
```sql
SELECT user_id
FROM (
    SELECT DISTINCT user_id, operator
    FROM booking JOIN trip ON booking.tri_id = trip.tri_id
) AS user_operators
GROUP BY user_id
HAVING COUNT(DISTINCT operator) >= 5;
```

#### UPDATE Operations

Basic structure:
```sql
UPDATE table
SET column = value, ...
WHERE condition;
```

Examples:

1. **Simple update**: Increase all book prices by 5%
```sql
UPDATE book
SET price = price * 1.05;
```

2. **Conditional update**: Different price adjustments based on conditions
```sql
UPDATE user
SET points = 
    CASE 
        WHEN points <= 1500 THEN points * 1.10
        ELSE points * 1.15
    END;
```

#### DELETE Operations

Basic structure:
```sql
DELETE FROM table
WHERE condition;
```

Examples:

1. **Delete specific rows**: Remove users without books
```sql
DELETE FROM user
WHERE user_id NOT IN (SELECT user_id FROM owns);
```

2. **Delete based on joins**: Remove trips without bookings
```sql
DELETE FROM trip
WHERE tri_id NOT IN (SELECT tri_id FROM booking);
```

#### CREATE TABLE

Basic structure:
```sql
CREATE TABLE table_name (
    column_name data_type constraints,
    ...
    PRIMARY KEY (column_name),
    FOREIGN KEY (column_name) REFERENCES other_table(column_name)
);
```

Example:
```sql
CREATE TABLE review (
    review_id VARCHAR(10),
    user_id INTEGER,
    book_id INTEGER,
    text TEXT,
    PRIMARY KEY (review_id),
    FOREIGN KEY (user_id) REFERENCES user(user_id),
    FOREIGN KEY (book_id) REFERENCES book(book_id)
);
```

## Transaction Management

### ACID Properties

1. **Atomicity**: Transactions are all-or-nothing
2. **Consistency**: Transactions bring the database from one valid state to another
3. **Isolation**: Effects of a transaction are not visible to other transactions until it completes
4. **Durability**: Once a transaction is committed, it remains in the system even if there's a system failure

### Serializability

A schedule is serializable if its effect is equivalent to some serial schedule (where transactions run one after another without overlapping).

#### Testing Serializability

1. **Create a precedence graph**:
    - Nodes represent transactions
    - Edge from T₁ to T₂ if operation in T₁ must precede conflicting operation in T₂

2. **Check for cycles**: If no cycles, the schedule is serializable

#### Example Analysis

For the 2024 exam schedule:
```
T1 | T2
-----------------
        | Read(B)
Read(A) |
        | Read(A)
        | Write(A)
Write(A)|
        | Write(B)
Read(B) |
Write(B)|
```

This schedule creates a cycle in the precedence graph:
- T₁ → T₂ (because T₁ writes A before T₂ writes A)
- T₂ → T₁ (because T₂ writes B before T₁ writes B)

Therefore, this schedule is NOT serializable.

## Database Normalization

### Normal Forms

1. **First Normal Form (1NF)**:
    - No repeating groups
    - All attributes are atomic

2. **Second Normal Form (2NF)**:
    - Is in 1NF
    - No partial dependency of non-key attributes on the primary key

3. **Third Normal Form (3NF)**:
    - Is in 2NF
    - No transitive dependency of non-key attributes on the primary key

4. **Boyce-Codd Normal Form (BCNF)**:
    - For every non-trivial functional dependency X → Y, X is a superkey

### Definitions

#### Third Normal Form (3NF)
A relation R is in 3NF if for every non-trivial functional dependency X → A:
- X is a superkey, OR
- A is part of some candidate key

#### Boyce-Codd Normal Form (BCNF)
A relation R is in BCNF if for every non-trivial functional dependency X → A:
- X is a superkey (i.e., X determines all attributes)

## Functional Dependencies

### Basic Concepts

- **Functional Dependency**: X → Y means that the values of X determine the values of Y
- **Candidate Key**: A minimal set of attributes that uniquely identifies a tuple
- **Primary Key**: The chosen candidate key
- **Superkey**: A set of attributes that contains a candidate key

### Lossless Join Decomposition

A decomposition of R into R₁ and R₂ is lossless if:
- R₁ ∩ R₂ → R₁, OR
- R₁ ∩ R₂ → R₂

This means the common attributes between R₁ and R₂ must be a superkey for at least one of them.

### Finding Candidate Keys

#### Steps:
1. Identify attributes that don't appear on the right side of any FD (these must be part of every candidate key)
2. Use the closure of attribute sets to verify if a set determines all attributes
3. Check minimality by ensuring no subset determines all attributes

#### Example from 2024 Exam
For R = (A, B, C, D, E) with FDs {AB → C, BD → A, DC → E}:

1. B doesn't appear on the right side, so B must be part of any candidate key
2. Test closures: (B)⁺ = {B}, (BD)⁺ = {B,D,A}, (BDC)⁺ = {B,D,C,A,E}
3. Therefore, BD is a candidate key, since BD determines A, and with A we can determine C, and with C and D we can determine E

### Attribute Closure

The closure of a set of attributes X with respect to a set of FDs F, denoted X⁺, is the set of all attributes determined by X under F.

#### Algorithm:
1. Start with X⁺ = X
2. If there's a FD Y → Z such that Y ⊆ X⁺, add Z to X⁺
3. Repeat until no more attributes can be added