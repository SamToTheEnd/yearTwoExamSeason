# Database Transactions

## What is a Transaction?

A transaction is a logical unit of work that consists of one or more database operations (read, write, update, delete) that must be executed as a single, indivisible unit. Either all operations in a transaction are successfully completed, or none are.

## ACID Properties

Transactions follow the ACID properties to ensure database integrity and reliability:

### Atomicity

**Definition**: A transaction is an atomic unit of work. Either all operations within a transaction are completed successfully, or none are applied.

**Example**: Consider a bank transfer transaction that withdraws money from account A and deposits it into account B:

```sql
BEGIN TRANSACTION;
    UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 'A';
    UPDATE Accounts SET Balance = Balance + 100 WHERE AccountID = 'B';
COMMIT;
```

If the system fails after the first UPDATE but before the second, atomicity ensures that the first UPDATE is rolled back, maintaining the consistency of the database.

### Consistency

**Definition**: A transaction must transform the database from one consistent state to another. All integrity constraints must be satisfied before and after the transaction.

**Example**: If a database has a constraint that account balances cannot be negative:

```sql
BEGIN TRANSACTION;
    -- This would be rejected if A's balance is less than 100
    UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 'A';
    UPDATE Accounts SET Balance = Balance + 100 WHERE AccountID = 'B';
COMMIT;
```

The transaction will only be committed if it doesn't violate this constraint.

### Isolation

**Definition**: The effects of concurrent transactions are isolated from each other. Each transaction appears to execute as if it were the only transaction in the system.

**Example**: Two concurrent transactions trying to modify the same data:

```
Transaction T1:
    READ(A)
    A = A + 100
    WRITE(A)

Transaction T2:
    READ(A)
    A = A * 2
    WRITE(A)
```

Without isolation, if T1 reads A=100, then T2 reads A=100, then T1 writes A=200, then T2 writes A=200, the multiplication effect of T2 is lost. With proper isolation, T2 would see T1's changes.

### Durability

**Definition**: Once a transaction is committed, its effects are permanent and survive system failures.

**Example**: After a transaction is committed:

```sql
BEGIN TRANSACTION;
    UPDATE Accounts SET Balance = Balance - 100 WHERE AccountID = 'A';
    UPDATE Accounts SET Balance = Balance + 100 WHERE AccountID = 'B';
COMMIT;
```

Even if the system crashes immediately after the COMMIT, when it restarts, the changes will still be applied to the database.

## Transaction Schedules

### Serial Schedule

A schedule where transactions are executed one after another with no interleaving.

**Example**:
```
T1: Read(A), Write(A), Read(B), Write(B)
T2: Read(A), Write(A), Read(B), Write(B)

Serial Schedule S1:
T1: Read(A), Write(A), Read(B), Write(B)
T2: Read(A), Write(A), Read(B), Write(B)
```

### Serializable Schedule

A schedule that produces the same result as some serial schedule. It's not necessarily a serial schedule itself, but it's equivalent to one.

## Testing Serializability

### Conflict Serializability

Two operations are in conflict if:
1. They belong to different transactions
2. They access the same data item
3. At least one of them is a write operation

To test for conflict serializability:
1. Create a precedence graph with transactions as nodes
2. Add an edge from Ti to Tj if an operation in Ti conflicts with and precedes an operation in Tj
3. If the graph has a cycle, the schedule is not conflict serializable

**Example**:
```
Schedule S:
T1: Read(A)
T2: Read(A)
T1: Write(A)
T2: Write(A)
```

Precedence graph: T1 → T2 (T1's Read(A) conflicts with T2's Write(A))
T2 → T1 (T2's Read(A) conflicts with T1's Write(A))

The graph has a cycle, so S is not conflict serializable.

### View Serializability

A schedule S is view serializable if it is view equivalent to a serial schedule.

Two schedules are view equivalent if:
1. For each data item, initial reads see the same values
2. For each data item, each read operation that is not the initial read sees the same write operation
3. For each data item, the final write is the same

## Exam Example 1: Testing Serializability

Consider the following schedule:
```
T1     | T2
----------------
Read(A) |
       | Read(B)
Write(A)|
       | Write(B)
Read(B) |
Write(B)|
```

Is this schedule serializable? If yes, provide an equivalent serial schedule.

**Solution**:
Create a precedence graph:
- T1 → T2 (T1's Write(A) precedes T2's Read(A) - but T2 never reads A, so no edge)
- T2 → T1 (T2's Write(B) precedes T1's Read(B))

The graph is acyclic, so the schedule is serializable.
Equivalent serial schedule: T2 followed by T1.

## Exam Example 2: ACID Violation

For the following schedule of transactions T1 and T2, where initially A=10, B=20:
```
Time | T1         | T2
--------------------------
1    | Read(A)    |
2    |            | Read(B)
3    | A = A + 10 |
4    |            | B = B - 5
5    | Write(A)   |
6    |            | Write(B)
7    | Read(B)    |
8    | B = B * 2  |
9    | Write(B)   |
```

What are the final values of A and B? Which ACID properties are violated?

**Solution**:
- After T1 executes, A = 20 (A=10+10)
- After T2 executes, B = 15 (B=20-5)
- Then T1 reads B (which is now 15)
- T1 sets B = 30 (B=15*2)
- Final values: A=20, B=30

The isolation property is violated because T1 reads B after T2 has modified it.

## Exam Example 3: Testing Serializability

Consider the schedule:
```
T1     | T2
----------------
Read(A) |
       | Read(B)
       | Read(A)
       | Write(A)
Write(A)|
       | Write(B)
Read(B) |
Write(B)|
```

Is this schedule serializable? Explain your answer.

**Solution**:
Create a precedence graph:
- T1 → T2 (T1's Read(A) conflicts with T2's Write(A))
- T2 → T1 (T2's Write(A) conflicts with T1's Write(A))

The graph has a cycle, so the schedule is not serializable.

## Concurrency Control Techniques

### Locking

Transactions acquire locks on data items before accessing them:
- **Shared (Read) Lock**: Multiple transactions can hold read locks on the same item
- **Exclusive (Write) Lock**: Only one transaction can hold a write lock on an item

**Two-Phase Locking (2PL)**:
1. **Growing Phase**: Acquire locks, do not release any locks
2. **Shrinking Phase**: Release locks, do not acquire any new locks

**Example**:
```
T1:
  Lock-X(A)     -- Acquire exclusive lock on A
  Read(A)
  A = A + 100
  Write(A)
  Lock-X(B)     -- Acquire exclusive lock on B
  Read(B)
  B = B + 50
  Write(B)
  Unlock(A)     -- Release lock on A
  Unlock(B)     -- Release lock on B
```

### Timestamping

Each transaction gets a unique timestamp when it starts.
- For each data item X, maintain ReadTimestamp(X) and WriteTimestamp(X)
- If a transaction wants to read X and its timestamp is less than WriteTimestamp(X), abort and restart
- If a transaction wants to write X and its timestamp is less than ReadTimestamp(X), abort and restart

### Multi-Version Concurrency Control (MVCC)

Keep multiple versions of data items to allow transactions to read a consistent snapshot of the database.

### Optimistic Concurrency Control

Assume transactions will not conflict, check for conflicts at commit time.

## Transaction Isolation Levels

SQL defines four isolation levels:

1. **Read Uncommitted**: Allows dirty reads, nonrepeatable reads, and phantom reads
2. **Read Committed**: Prevents dirty reads, allows nonrepeatable reads and phantom reads
3. **Repeatable Read**: Prevents dirty reads and nonrepeatable reads, allows phantom reads
4. **Serializable**: Prevents all three anomalies

**Example**:
```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
BEGIN TRANSACTION;
    SELECT * FROM Accounts WHERE AccountID = 'A';
    -- Other operations
COMMIT;
```

## Exam Examples: Concurrency Issues

### Dirty Read

Transaction T1 reads a value written by T2, but T2 is rolled back:
```
T1:              | T2:
-----------------|------------------
                 | BEGIN
                 | UPDATE A = A + 100
READ(A)          |
                 | ROLLBACK
```
T1 reads a value that never actually existed in the database.

### Non-repeatable Read

Transaction T1 reads a value, then T2 modifies it, then T1 reads it again and gets a different value:
```
T1:              | T2:
-----------------|------------------
BEGIN            |
READ(A)          |
                 | BEGIN
                 | UPDATE A = A + 100
                 | COMMIT
READ(A)          |
COMMIT           |
```

### Phantom Read

Transaction T1 reads a set of rows, then T2 inserts a new row that matches T1's query, then T1 reads again and sees the new row:
```
T1:                          | T2:
----------------------------|------------------
BEGIN                       |
SELECT * FROM Accounts      |
WHERE Balance > 1000        |
                            | BEGIN
                            | INSERT INTO Accounts VALUES ('C', 1500)
                            | COMMIT
SELECT * FROM Accounts      |
WHERE Balance > 1000        |
COMMIT                      |
```

## Recovery Techniques

### Log-Based Recovery

Keep a log of all database operations:
- Before-image: Value before change
- After-image: Value after change

**Example**:
```
T1: BEGIN
T1: UPDATE A = 100 (before: 50, after: 100)
T1: UPDATE B = 200 (before: 150, after: 200)
T1: COMMIT
```

### Checkpointing

Periodically save the state of the database to disk.

### ARIES Recovery Algorithm

1. **Analysis**: Determine active transactions at crash time
2. **Redo**: Redo all operations from the last checkpoint
3. **Undo**: Undo operations of incomplete transactions