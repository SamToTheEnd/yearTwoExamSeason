# SQL Queries for Database Exams

Based on the past exam papers (CS2855-22, CS2855-23, CS2855-24), here's a comprehensive guide to SQL queries that you need to know for your exam.

## Basic SQL Query Structure

The basic SELECT query structure:

```sql
SELECT [columns]
FROM [tables]
WHERE [conditions]
GROUP BY [columns]
HAVING [group conditions]
ORDER BY [columns] [ASC|DESC]
```

## 1. Basic Queries

### SELECT, FROM, WHERE

```sql
-- Select all columns from a table
SELECT * FROM Driver;

-- Select specific columns
SELECT Name, Salary FROM Driver;

-- Select with conditions
SELECT DriverID, Name FROM Driver WHERE Salary > 30000;
```

From CS2855-24 Question 2(b)(v):
```sql
-- Find drivers with salaries less than 15,000 who drove specific cars
SELECT DISTINCT Driver.Name
FROM Driver 
JOIN Transport ON Driver.DriverID = Transport.DriverID
JOIN Vehicle ON Transport.Registration = Vehicle.Registration
WHERE Driver.Salary < 15000 
  AND Vehicle.Mileage <= 50000 
  AND Vehicle.Year > 2019;
```

## 2. Joins

### Inner Join
```sql
-- Natural join (implicitly joining on same-named columns)
SELECT * FROM Driver NATURAL JOIN Transport;

-- Explicit join
SELECT *
FROM Driver JOIN Transport 
ON Driver.DriverID = Transport.DriverID;
```

From CS2855-24 Question 2(b)(iv):
```sql
-- For each vehicle, find drivers who drove it more than 3 times
SELECT v.Registration, d.Name
FROM Vehicle v
JOIN Transport t ON v.Registration = t.Registration
JOIN Driver d ON t.DriverID = d.DriverID
GROUP BY v.Registration, d.Name
HAVING COUNT(*) > 3;
```

### Left, Right, and Full Outer Joins
```sql
-- Left outer join (keeps all rows from the left table)
SELECT * FROM Driver LEFT JOIN Transport 
ON Driver.DriverID = Transport.DriverID;

-- Right outer join (keeps all rows from the right table)
SELECT * FROM Driver RIGHT JOIN Transport 
ON Driver.DriverID = Transport.DriverID;

-- Full outer join (keeps all rows from both tables)
SELECT * FROM Driver FULL OUTER JOIN Transport 
ON Driver.DriverID = Transport.DriverID;
```

## 3. Aggregation Functions

```sql
-- Count
SELECT COUNT(*) FROM Driver;

-- Sum
SELECT SUM(Salary) FROM Driver;

-- Average
SELECT AVG(Salary) FROM Driver;

-- Minimum and Maximum
SELECT MIN(Salary), MAX(Salary) FROM Driver;
```

From CS2855-23 Question 2(d)(ii):
```sql
-- Output trip_id alongside total number of booked seats
SELECT tri_id, SUM(seats) AS seats
FROM booking
GROUP BY tri_id;
```

## 4. GROUP BY and HAVING

```sql
-- Group by a column
SELECT DriverID, COUNT(*) AS TripCount
FROM Transport
GROUP BY DriverID;

-- Group by with conditions
SELECT DriverID, COUNT(*) AS TripCount
FROM Transport
GROUP BY DriverID
HAVING COUNT(*) > 2;
```

From CS2855-22 Question 2(d)(iii):
```sql
-- For every book, output its title and the number of copies owned
SELECT b.title, SUM(o.copies) AS copies
FROM book b
JOIN owns o ON b.book_id = o.book_id
GROUP BY b.title;
```

From CS2855-23 Question 2(d)(iii):
```sql
-- List operators and show number of trips offered, ordered by count
SELECT operator, COUNT(*) AS trip_count
FROM trip
GROUP BY operator
ORDER BY COUNT(*) DESC;
```

## 5. Subqueries

```sql
-- Subquery in WHERE clause
SELECT Name
FROM Driver
WHERE Salary > (SELECT AVG(Salary) FROM Driver);

-- Subquery in FROM clause
SELECT d.Name, avgs.avg_salary
FROM Driver d, (SELECT AVG(Salary) AS avg_salary FROM Driver) avgs
WHERE d.Salary > avgs.avg_salary;
```

From CS2855-24 Question 2(b)(vi):
```sql
-- Find vehicles with mileage higher than average that have been driven by at least 3 drivers
SELECT v.Registration
FROM Vehicle v
JOIN Transport t ON v.Registration = t.Registration
WHERE v.Mileage > (SELECT AVG(Mileage) FROM Vehicle)
GROUP BY v.Registration
HAVING COUNT(DISTINCT t.DriverID) >= 3;
```

## 6. Set Operations

```sql
-- Union
SELECT DriverID FROM Driver
UNION
SELECT DriverID FROM Transport;

-- Intersection
SELECT DriverID FROM Driver
INTERSECT
SELECT DriverID FROM Transport;

-- Difference
SELECT DriverID FROM Driver
EXCEPT
SELECT DriverID FROM Transport;
```

From CS2855-23 Question 2(b)(i):
```sql
-- Find users who booked tickets with both North Line and Eastern
-- This can be written using intersection:
SELECT user_id
FROM booking b
JOIN trip t ON b.tri_id = t.tri_id
WHERE t.operator = 'North Line'
INTERSECT
SELECT user_id
FROM booking b
JOIN trip t ON b.tri_id = t.tri_id
WHERE t.operator = 'Eastern';
```

## 7. Order By

```sql
-- Order by one column ascending (default)
SELECT Name, Salary FROM Driver ORDER BY Salary;

-- Order by one column descending
SELECT Name, Salary FROM Driver ORDER BY Salary DESC;

-- Order by multiple columns
SELECT Name, Salary FROM Driver ORDER BY Salary DESC, Name ASC;
```

From CS2855-22 Question 2(d)(i):
```sql
-- Output title and price of every book ordered by year and title
SELECT title, price
FROM book
ORDER BY year, title;
```

From CS2855-23 Question 2(d)(i):
```sql
-- Output name and points of users with more than 2000 points in ascending order
SELECT name, points
FROM user
WHERE points > 2000
ORDER BY points ASC;
```

## 8. Data Manipulation Language (DML)

### INSERT
```sql
-- Insert a single row
INSERT INTO Driver (DriverID, Name, Salary)
VALUES (1234, 'Sarah', 28000);

-- Insert multiple rows
INSERT INTO Driver (DriverID, Name, Salary)
VALUES 
  (1234, 'Sarah', 28000),
  (1235, 'Michael', 32000);

-- Insert from query results
INSERT INTO HighPaidDrivers (DriverID, Name)
SELECT DriverID, Name
FROM Driver
WHERE Salary > 30000;
```

### UPDATE
```sql
-- Update all rows
UPDATE Driver SET Salary = Salary * 1.05;

-- Update with condition
UPDATE Driver SET Salary = Salary * 1.1 WHERE Salary < 25000;
```

From CS2855-24 Question 2(b)(iii):
```sql
-- Increase salary based on different conditions
UPDATE Driver
SET Salary = 
    CASE
        WHEN Salary <= 20000 THEN Salary * 1.05
        WHEN Salary > 20000 AND Salary < 30000 THEN Salary * 1.03
        ELSE Salary * 1.01
    END;
```

From CS2855-22 Question 2(c)(i):
```sql
-- Increase price of every book by 5%
UPDATE book
SET price = price * 1.05;
```

From CS2855-22 Question 2(c)(ii):
```sql
-- Decrease price of books written before 1920 by 10%
UPDATE book
SET price = price * 0.9
WHERE year < 1920;
```

### DELETE
```sql
-- Delete all rows
DELETE FROM Driver;

-- Delete with condition
DELETE FROM Driver WHERE Salary < 20000;
```

From CS2855-22 Question 2(c)(iii):
```sql
-- Delete all users that do not own any book
DELETE FROM user
WHERE user_id NOT IN (SELECT user_id FROM owns);
```

From CS2855-23 Question 2(c)(i):
```sql
-- Delete all trips without any tickets booked
DELETE FROM trip
WHERE tri_id NOT IN (SELECT tri_id FROM booking);
```

## 9. Data Definition Language (DDL)

### CREATE TABLE
```sql
-- Create a new table
CREATE TABLE Driver (
    DriverID INT PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    Salary DECIMAL(10,2),
    HireDate DATE DEFAULT CURRENT_DATE
);

-- Create table with foreign key
CREATE TABLE Transport (
    TransportID INT PRIMARY KEY,
    DriverID INT,
    Registration VARCHAR(10),
    Driver_Mileage INT,
    FOREIGN KEY (DriverID) REFERENCES Driver(DriverID),
    FOREIGN KEY (Registration) REFERENCES Vehicle(Registration)
);
```

From CS2855-23 Question 2(d)(v):
```sql
-- Define a relation for delays
CREATE TABLE delay (
    delay_id VARCHAR(6) PRIMARY KEY,
    tri_id VARCHAR(10),
    date DATE,
    delay INT,
    FOREIGN KEY (tri_id) REFERENCES trip(tri_id)
);
```

From CS2855-22 Question 2(d)(v):
```sql
-- Create a reviews table for bookstore
CREATE TABLE review (
    reviewid VARCHAR(10) PRIMARY KEY,
    user_id INT,
    book_id INT,
    text TEXT,
    FOREIGN KEY (user_id) REFERENCES user(user_id),
    FOREIGN KEY (book_id) REFERENCES book(book_id)
);
```

### ALTER TABLE
```sql
-- Add a column
ALTER TABLE Driver ADD COLUMN Phone VARCHAR(15);

-- Drop a column
ALTER TABLE Driver DROP COLUMN Phone;

-- Modify a column
ALTER TABLE Driver ALTER COLUMN Name VARCHAR(100);

-- Add a constraint
ALTER TABLE Driver ADD CONSTRAINT min_salary CHECK (Salary >= 20000);
```

From CS2855-24 Question 2(b)(i):
```sql
-- Adding a list of phones for drivers
ALTER TABLE Driver 
ADD COLUMN Phones VARCHAR(255);
-- Or creating a separate table for normalization
CREATE TABLE DriverPhones (
    DriverID INT,
    Phone VARCHAR(15),
    PRIMARY KEY (DriverID, Phone),
    FOREIGN KEY (DriverID) REFERENCES Driver(DriverID)
);
```

### DROP TABLE
```sql
-- Drop a table
DROP TABLE Driver;
```

## 10. Advanced SQL Concepts

### Common Table Expressions (CTEs)
```sql
-- Define a temporary result set
WITH HighPaidDrivers AS (
    SELECT DriverID, Name, Salary
    FROM Driver
    WHERE Salary > 30000
)
SELECT * FROM HighPaidDrivers
WHERE Name LIKE 'A%';
```

### Window Functions
```sql
-- Rank drivers by salary
SELECT 
    DriverID,
    Name,
    Salary,
    RANK() OVER (ORDER BY Salary DESC) AS SalaryRank
FROM Driver;

-- Calculate running total
SELECT 
    DriverID,
    Name,
    Salary,
    SUM(Salary) OVER (ORDER BY DriverID) AS RunningTotal
FROM Driver;
```

## Common Exam Tasks

From analyzing all three past papers, here are the most common types of SQL query tasks:

1. **Simple data retrieval with conditions**
    - Selecting specific columns with WHERE conditions
    - Using JOIN operations to combine tables

2. **Aggregate queries with GROUP BY**
    - Counting occurrences
    - Calculating sums, averages, etc.
    - Using HAVING to filter groups

3. **Updates based on conditions**
    - Using CASE statements for conditional updates
    - Percentage increases or decreases

4. **Complex JOINs with multiple tables**
    - Usually 3-way joins to answer complex questions

5. **Subqueries**
    - Especially for comparing with aggregates like AVG
    - For filtering out records (using IN, NOT IN)

6. **Table creation with constraints**
    - Creating new tables with PRIMARY KEY and FOREIGN KEY constraints
    - Adding columns to existing tables

7. **Deletes with subqueries**
    - Removing records based on their presence or absence in other tables

8. **Sorting results**
    - Using ORDER BY with multiple columns and directions

## Exam Strategy

When tackling SQL questions in exams:

1. **Understand the schema**: First, identify the tables, their columns, and the relationships between them.

2. **Identify key columns**: Find primary and foreign keys to understand how to join tables.

3. **Break down complex queries**: For complex questions, sketch the steps:
    - Which tables are needed?
    - What are the join conditions?
    - What filters (WHERE conditions) are needed?
    - What aggregations or groupings are required?
    - How should the results be ordered?

4. **Pay attention to edge cases**:
    - Handle NULL values appropriately
    - Ensure your query works for all possible data, not just the example

5. **Double-check syntax**: Common syntax issues include:
    - Missing semicolons
    - Incorrect join syntax
    - Forgetting GROUP BY columns
    - Incorrect usage of aggregation functions