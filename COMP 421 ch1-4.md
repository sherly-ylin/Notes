## Content

- [Chapter 1 - Introduction](#chapter-1---introduction)
  - [Data Abstraction](#data-abstraction)
  - [Database Languages](#database-languages)
    - [The Database Engine](#the-database-engine)
- [Chapter 2](#chapter-2)
  - [Keys](#keys)
  - [Relational Algebra](#relational-algebra)
      - [Project $\Pi$](#project-pi)
      - [Cartesian-product $\times$](#cartesian-product-times)
      - [Join $\Join$](#join-join)
      - [Union $\cup$](#union-cup)
      - [Intersection $\cap$](#intersection-cap)
      - [Set-difference $-$](#set-difference--)
      - [Assignment $\leftarrow$](#assignment-leftarrow)
      - [Rename $\rho$](#rename-rho)
- [SQL](#sql)
  - [Data Definition Language (DDL)](#data-definition-language-ddl)
  - [SQL Constraints](#sql-constraints)
  - [Data Manipulation Language (DML)](#data-manipulation-language-dml)
  - [SQL Query](#sql-query)
    - [Where](#where)
    - [String operations](#string-operations)
    - [Group by](#group-by)
    - [Aggregate Functions](#aggregate-functions)
    - [Set Operations](#set-operations)
      - [Set Comparison](#set-comparison)
    - [Joins](#joins)
      - [Join (Inner Join)](#join-inner-join)
      - [Natural Join](#natural-join)
      - [Outer Joins](#outer-joins)
  - [Views](#views)
  - [SQL Commands Summary](#sql-commands-summary)
    - [Order of Exectution](#order-of-exectution)

# Chapter 1 - Introduction

**Database Management System (DBMS)**

- database and software that manages databases
- to store and retrieve data efficiently and conveniently

**DBMS vs typical file-processing system**

- Data redundancy and inconsistency
- Difficulty in accessing/retrival (filter)
- Data integrity problems
- Atomicity problems
- Concurrent Access problems

**Data Models**
Relational Model

- A record-based model
- Data is organized in tables (relations)
  - Each table contains records of a particular type
  - Each record types defines a fixed number of attributes
- Relationships between tables

## Data Abstraction

**Physical Level**

- How data are actually stored
- (Physical storage, storage devices, data structures, etc)
- a record ≈ a block of consecutive bytes

**Logical Level**

- What data are stored and what relationship exists among them
- Users interact with the database through queries and transactions expressed in a data manipulation language (such as SQL) at this level
- Data administrators use this level.
- The logical level provides a way to view the database independently of its physical storage implementation. (Physical data independence)
- a record ≈ a type definition

**View Level**

- describes only part of the entire database
- provides a customized view of the database tailored to the specific needs of different users or applications, & add secutiry mechanism
- The system may provide many views for the same database.
- user see a set off application programs that can hide details of the data types

## Database Languages

**Data Definition Language (DDL)**

- to specify database schima
  - domain constraint, referential integrity, authorization
- ```CREATE```, create new table
- ```ALTER```, modify existing table structure(add/edit attribute)
- ```DROP```, delete table
- ```TRUNCATE```, delete all data inside a table

**Data Manipulation Language (DML)**

- Queries and updates
- ```SELECT```, retrieve records
- ```INSERT```, insert records(rows)
- ```DELETE```, delete records
- ```UPDATE```, modify records

### The Database Engine

**Storage Manager**

- responsible for storing, retrieving, and updating data in the database.
- interact with the file manager
- translate DML statment into low-level file-system commands
- Components: authorization and intergrity manager, transaction manager, file manager, buffer manager...

**Query Processor**

- responsible for processing and executing queries
- Components: DDL interperter, DML compiler, query evaluation engine

**Transaction Management**

- reponsible for ensuring the ACID properties (Atomicity, Consistensy, Isolation, Durability)
- coordinates the execution of transactions -- sequences of operations that constitute a logical unit of work, and ensures that they are executed
  - atomically (all or nothing),
  - consistently (maintaining data integrity constraints),
  - isolated (without interference from other transactions), and
  - durably (persistently stored).
- Components: recovery manager, concurrency-control manager

# Chapter 2

**Database schema** -- logical design of the database
**Database instances** -- a snapshot of database content at a point in time
**A relation instance** = a specific iinstance of a relation

## Keys

Key - a principal means of identifying a tuple in a relation

**Super Key**

- a set of attribute(S) that uniquely identify a tuple in the relation
- a superset of super key is a super key

**Candidate Key**

- a minimal superkey -- no subset of it is a superkey

**Primary Key**

- a candidate key
- chosen by the database designer as the main way if identifying tuples within a relation
- the `PRIMARY KEY` constraint: the constrained columns' values must uniquely identify each row

**Foreign Key**

- an attribute in a relation that is also the primary key of another relation (reference)
- the `FOREIGN KEY` constraint:

## Relational Algebra

####Select $\sigma$

<table>
<tr>
<td> 

$\sigma_{<predicate>}(relation)$

</td>
<td>

```sql
SELECT * 
FROM relation 
WHERE <predicate>
```

</td>
</tr>
</table>


#### Project $\Pi$
<table>
<tr>
<td> 

$\Pi_{id, name}(relation)$

</td>
<td>

```sql
SELECT id, name 
FROM relation
```

</td>
</tr>
</table>


#### Cartesian-product $\times$
-> equivalent to `CROSS JOIN` - a combined tuple of every possible pair
-> # of rows in resulting table = (# of rows in $r_1$) (# of rows in $r_2$) 

<table>
<tr>
<td> 

$r_1 \times r_2$

</td>
<td>

```sql
r1 CROSS JOIN r2
```

</td>
</tr>
</table>


#### Join $\Join$
- a derivative of Cartesian product


<table>
<tr>
<td> 

$r_1 \Join_P r_2 $

</td>
<td>

```sql
r1 JOIN r2 ON [P]
```

</td>
</tr>

<tr>
<td> 

$ \sigma_P (r_1 \times r_2)$

</td>
<td>

```sql
r1 CROSS JOIN r2  WHERE [P]
-- SQL will keep the column used for join from both tables
-- but not in relational algebra
```

</td>
</tr>
</table>

$r_1 \Join_P r_2 = \sigma_P (r_1 \times r_2)$


Equivalent:
- $Customers \Join_{Customers.customer_id=Orders.customer_id} Orders$
- $\sigma_{Customers.customer_id=Orders.customer_id} (Customers \times Orders)$

```sql
SELECT * 
FROM customers c
JOIN orders o ON c.customer_id=o.customer_id
--
SELECT * 
FROM customers c
CROSS JOIN orders
WHERE c.customer_id=o.customer_id
```


#### Union $\cup$
SQL : `UNION`

$\Pi_{name}(Movies)\cup\Pi_{name}(Series)$
```
SELECT name FROM Movies
UNION
SELECT name FROM Series
```

#### Intersection $\cap$
SQL : `INTERSECT`

#### Set-difference $-$
SQL : `EXCEPT`

#### Assignment $\leftarrow$
- works like assignment in a programming language
$Physics\leftarrow\sigma_{department='Physics'}(instructor)$
```
WITH Physics AS (SELECT * 
                  FROM instructor 
                  WHERE department='Physics')
```

#### Rename $\rho$
$\rho_x(E)$
- result of a relational-algebra expression E is remaned "x"




# SQL

- Data-definition language (DDL)
  - specification of information about relations
    - schema for each relation
    - types of values associated with attributes
    - integrity constraint
    - the set of indices to be maintained for the relations
    - the security and authorization information for the relation
    - the physical storage structure of relations on disk
  - changes a table’s structure
- Data-manipulation language (DML)
  - for modifying a database's data

## Data Definition Language (DDL)
- Basic Schema Definition
<table>
<tr>
<td> Command </td> <td> Format </td> <td> Usage </td>
</tr>
<tr>
<td> CREATE </td>

<td> 

```sql
CREATE TABLE table_name(
  column_1 datatype [constraint],
  column_2 datatype,
  ...,
  integraty constraint_1,
  ...)
```

</td>
<td>

```sql
CREATE TABLE Student(
  id int NOT NULL,
  name varchar(25) NOT NULL ,
  age int,
  PRIMARY KEY (id),
  FOREIGN KEY (id) REFERENCE Takes(student_id)
  CHECK (age>=18)
  ...)
```
</td>

</tr>
<tr>
<td> DELETE </td>
<td> 

```sql
DROP TABLE table_name
```

</td>
<td>

```sql
DROP TABLE IF EXISTS table_name
```
</td>
</tr>
<td> ALTER </td>
<td> 

```sql
ALTER TABLE table_name
```

</td>
<td>

```sql
ALTER TABLE student ADD(address VARCHAR2(20) DEFAULT '');  
ALTER TABLE student MODIFY (address VARCHAR2(20));  
```
</td>
</tr>
</tr>
<td> TRUNCATE </td>
<td> 

```sql
TRUNCATE TABLE table_name
```

</td>
<td>
Used to delete all the rows from the table, and free up the space in the table.
</td>
</tr>
</table>

## SQL Constraints

- **`PRIMARY KEY(A1, …, Am)`**
  - the primary-key attributes have to be non null and unique
- **`FOREIGN KEY(A1, …, Am) REFERENCE r2(B1,…,Bm)`**
  - the values of A1,…,Am for any tuple in the relation must correspond to values of the primary key attributes of some tuples in relation s.
- **`NOT NULL`**: null value is not allowed for this attribute
- **`UNIQUE`**
- **`CHECK`**: used to limit the value range that can be placed in a column.
- **`on delete/update cascade`**

## Data Manipulation Language (DML)

<table>
<tr>
<td> Command </td> <td> Format </td> <td> Usage </td>
</tr>
<tr>
<td> INSERT </td>
<td> 

```sql
INSERT INTO table (column_1, column_2, ...) 
VALUES (value_1, value_2, ...);  
```

</td>
<td>

```sql
INSERT INTO student (id, name, age) 
VALUES (13, 'Alex', 21);  
```

</td>
</tr>
<tr>
<td> DELETE </td>
<td> 

```sql
DELETE FROM <table> WHERE <predicate>
```

</td>
<td>

```sql
DELETE FROM student WHERE name='Alex'
DELETE FROM student -- all records will be deleted
```
</td>
</tr>
<td> UPDATE </td>
<td> 

```sql
UPDATE TABLE table_name
SET <column> = <value>  
WHERE <predicate>  
```

</td>
<td>

```sql
UPDATE TABLE student
SET age = 22  
WHERE name='Alex' 
```

</td>
</tr>
</table>




### SELECT - SQL Query 
General order of clauses:
```sql
SELECT [column]
FROM [table]
WHERE [predicate]
ORDER BY [selected column] [desc, default asc]
LIMIT [number of rows]
```

`SELECT` 
- `DISTINCT` - remove duplicates
- `ALL` - explicitly keep duplicates
- `TOP` [number]


#### Where
`WHERE`

- `[predicate] AND [predicate] OR [predicate]`
  - AND has higher priority that OR
- `[column] IN (value1, value2, ...)`
- `[column] BETWEEN [number] AND [number]`
- `[column] IS (NOT) NULL`
- `EXIST (subquery)`
- `UNIQUE (subquery)`


`EXIST` - return TRUE if there exist any record in the subquery, i.e. the outer SQL query is executed only if the subquery is not null
```sql
SELECT ... FROM ....
WHERE EXIST 
(SELECT column_name FROM table_name WHERE condition)
```

`WHERE EXISTS (subquery)` <=> `WHERE 0 <> (subquery)`
- `0 <> (subquery)` : 0 ≠ [# of rows of subquery]

`UNIQUE` -- if subquey contains duplicates in the results

#### String operations

`(string) LIKE (exp)`
- `'%'` - any number of characters,
- `'_'` - a single character
`‘%y’` 		- ends with y
`‘_y’` 		- exactly 2 characters ends with y

Escape character `\` to escape special characters, &, \
- `like 'ab∖%cd%' escape '∖'` matches all strings beginning with “ab%cd”
- `like 'ab∖∖cd%' escape '∖'` matches all strings beginning with “ab∖cd”


#### Group by
`GROUP BY`
- usually only need `group by` with aggregate functions
- **attribute in `select` clause outside of aggregate function must appear in group by list**

Group by multiple columns:
- `Group By X` : put all records with the same value for X in the one group (row)

- `Group By X, Y` : put all records with the same values for both X and Y in the one group.

<table>
<tr>
  <td>

  ```
  select * from Seletcion
  ```

  </td>
  <td>

  | Subject | Section | Attendee |
  | ------- | ----- | ------- |
  | A       | 101   | Joel
  | A       | 102   | Alex
  | A       | 102   | Michael
  | A       | 102   | David
  | B       | 101   | Joel
  | B       | 101   | Amy

  </td>
</tr>
<tr>
  <td>

  ```
  select Subject, count(*)
  from Selection
  group by Subject
  ```

  </td>
  <td>

  | Subject | Count | 
  | ------- | ----- | 
  | A       | 4   | 
  | B       | 2   | 

  </td>
</tr>

<tr>
  <td>

  ```
  select Subject, Section, count(*)
  from Selection
  group by Subject, Section
  ```

  </td>
  <td>

  | Subject | Section | Count | 
  | ------- | ----- | ----- | 
  | A       | 101   |   1   | 
  | A       | 102   |   3   | 
  | B       | 101   |   2   |

  </td>
</tr>
</table>

`**HAVING**` 
- after groups have formed, aggregate functions can be used 
 

#### Aggregate Functions
- `MIN(column)`
- `MAX(column)`
- `COUNT(column)`, `COUNT(DISTINCT column)` 
- `SUM(column)`
- `AVG(column)`
- Often **used with the GROUP BY** clause of the SELECT statement, use **HAVING** for $condition on aggregated column 
- **Aggregate functions are not allowed in the WHERE clause**


#### Set Operations
- the number of columns must be equal, compatible types
- set oprations automatically remove duplicate
- use `ALL` to keep duplicate
`UNION`
`INTERSECT` 
`EXCEPT`
```
(query) 
UNION/INTERSECT/EXCEPT (ALL)
(query)
```
#### Set Comparison
- `= some` <=> `in`
- `≠ some` <=> `not in`
- `≠ all` <=> `not in`
- 
### Joins

`JOIN` 
- `ON `
- `USING()`


#### Join (Inner Join)
`JOIN` = `INNER JOIN` (the default join)
- R
Equivalent:
<table>
<tr>
<td>

```
SELECT c.customer_id id, o.amount
FROM customers c 
JOIN orders o 
USING(customer_id)
```

</td>
<td>

```
SELECT c.customer_id id, o.amount
FROM customers c 
JOIN orders o 
ON c.customer_id=o.customer_id
```
</td>

<td>

```
SELECT c.customer_id id, o.amount
FROM customers c, orders o 
WHERE c.customer_id=o.customer_id
```
</td>
</tr>
</table>
  
- Both `customer_id` columns will remain in the result
- use `USING` when the column names(and type) match

#### Natural Join
`NATURAL JOIN`
- Automatically use the common column names to define the join relationship
- There must be at least one common attribute
- Delete duplicate columns and inconsistant tuples
- perform Cartesian product --> find matching tuples & delete duplicates --> delete duplicate column
```
SELECT c.customer_id id, o.amount
FROM customers c NATURAL JOIN orders o 
```


#### Outer Joins
`LEFT JOIN`
`RIGHT JOIN`
`FULL JOIN` = 



## Views

Format:
```sql
CREATE VIEW <view_name> as <query expression>
```
Example:

```sql
CREATE VIEW **department_total_salary(name, total_salary)** AS
  SELECT dept_name, sum(salary)
  FROM instructor
  GROUP BY dept_name
```
Equivalent:
```sql
CREATE VIEW department_total_salary AS
  SELECT dept_name AS name, sum(salary) AS total_salary 
  FROM instructor
  GROUP BY name
```
Using views: (like a table)
```sql
SELECT * FROM department_total_salary
```
Delete views:
```sql
DROP VIEW (IF EXIST) <view_name>
```


## SQL Commands Summary




<table>
<tr>
  <td>

  ```sql
  SELECT DISTINCT 
  SELECT ALL
  SELECT TOP 3
  ```
  
  </td>
  <td>1</td>
</tr>

<tr>
  <td>

  ```sql
  r1 JOIN r2 USING(col)
  r1 JOIN r2 ON r1.col=r2.col
  ```
  
  </td>
  <td></td>
</tr>

<tr>
  <td></td>
  <td></td>
</tr>

<tr>
  <td></td>
  <td></td>
</tr>

<tr>
  <td></td>
  <td></td>
</tr>

<tr>
  <td></td>
  <td></td>
</tr>

</table>


`Distinct` mean : count all the values as 1, even if there was more than one.
`Unique` mean : count only the value that are not repeated in the particular column


### Order of Exectution

1. from / joins
2. where
3. group by
4. having
5. select
6. distinct
7. order by
8. limit

- the joins are executed in the order they are specified in the `FROM` clause
- Having clause applied after the formation of groups
- Where clause applied before the formation of groups

---

```sql
WITH var_name AS (subquery)
```
![alt text](<TEST FOR EMPTY RELATIONS.png>)
![alt text](<USE OF NOT EXISTS CLAUSE.png>)
![alt text](<TEST FOR ABSENCE OF DUPLICATE.png>)