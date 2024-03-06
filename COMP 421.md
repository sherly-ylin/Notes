### Content
- [Chapter 2](#chapter-2)
  - [Relational Algebra](#relational-algebra)
- [SQL](#sql)
  - [SQL Basics](#sql-basics)
      - [DDL](#ddl)
        - [SQL Constraints](#sql-constraints)
      - [Data Manipulation Language (DML)](#data-manipulation-language-dml)
  - [SQL Query Language](#sql-query-language)
    - [Joins](#joins)
        - [(INNER) JOIN (the default join)](#inner-join-the-default-join)
        - [NATURAL JOIN](#natural-join)
      - [OUTER JOIN](#outer-join)
        - [LEFT JOIN](#left-join)
    - [Views](#views)

# Chapter 2
## Relational Algebra

**Select $\sigma$**
$\sigma_{<predicate>}(relation)$

```
SELECT * 
FROM relation 
WHERE <predicate>
```

**Project $\Pi$**
$\Pi_{id, name}(relation)$
```
SELECT id, name 
FROM relation
```

**Cartesian-product $\times$**
$r_1 \times r_2$
-> equivalent to Cross Join - a combined tuple of each possible pair
-> # of rows in resulting table = (# of rows in $r_1$) (# of rows in $r_2$) 
```

```


**Join $\Join$**
$r_1 \Join_a r_2 = \sigma_a (r_1 \times r_2)$
Equivalent:
$Movies \Join_{movies.director=directors.name} Directors$
$\sigma_{movies.director=directors.name} (Movies \times Directors)$

```
SELECT * 
FROM movies m 
JOIN directors d ON m.director=director.name
```


**Union $\cup$**
$\Pi_{name}(Movies)\cup\Pi_{name}(Series)$
```
SELECT name FROM Movies
UNION
SELECT name FROM Series
```

**Intersection $\cap$**

**Set-difference $-$**


**Assignment $\leftarrow$**
$Physics\leftarrow\sigma_{department='Physics'}(instructor)$
```
WITH Physics AS (SELECT * 
                  FROM instructor 
                  WHERE department='Physics')
```

**Rename $\rho$**
$\rho_x(E)$, a relational-algebra expression E is remaned "x"

# SQL

## SQL Basics
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

#### DDL 
- Basic Schema Definition
<table>
<tr>
<td> Command </td> <td> Format </td> <td> Usage </td>
</tr>
<tr>
<td> CREATE </td>

<td> 

```
CREATE TABLE table_name(
  column_1 datatype [constraint],
  column_2 datatype,
  ...,
  integraty constraint_1,
  ...)
```

</td>
<td>

```
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

```
DROP TABLE table_name
```

</td>
<td>

```
DROP TABLE IF EXISTS table_name
```
</td>
</tr>
<td> ALTER </td>
<td> 

```
ALTER TABLE table_name
```

</td>
<td>

```
ALTER TABLE student ADD(address VARCHAR2(20) DEFAULT '');  
ALTER TABLE student MODIFY (address VARCHAR2(20));  
```
</td>
</tr>
</tr>
<td> TRUNCATE </td>
<td> 

```
TRUNCATE TABLE table_name
```

</td>
<td>
Used to delete all the rows from the table, and free up the space in the table.
</td>
</tr>
</table>

##### SQL Constraints

- **`PRIMARY KEY(A1, …, Am)`**
  - the primary-key attributes have to be non null and unique
- **`FOREIGN KEY(A1, …, Am) REFERENCE r2(B1,…,Bm)`**
  - the values of A1,…,Am for any tuple in the relation must correspond to values of the primary key attributes of some tuples in relation s.
- **`NOT NULL`**: null value is not allowed for this attribute
- **`UNIQUE`**
- **`CHECK`**: used to limit the value range that can be placed in a column.
- **`on delete/update cascade`**

#### Data Manipulation Language (DML)

<table>
<tr>
<td> Command </td> <td> Format </td> <td> Usage </td>
</tr>
<tr>
<td> INSERT </td>
<td> 

```
INSERT INTO table (column_1, column_2, ...) 
VALUES (value_1, value_2, ...);  
```

</td>
<td>

```
INSERT INTO student (id, name, age) 
VALUES (13, 'Alex', 21);  
```

</td>
</tr>
<tr>
<td> DELETE </td>
<td> 

```
DELETE FROM <table> WHERE <predicate>
```

</td>
<td>

```
DELETE FROM student WHERE name='Alex'
DELETE FROM student -- all records will be deleted
```
</td>
</tr>
<td> UPDATE </td>
<td> 

```
UPDATE TABLE table_name
SET <column> = <value>  
WHERE <predicate>  
```

</td>
<td>

```
UPDATE TABLE student
SET age = 22  
WHERE name='Alex' 
```

</td>
</tr>
</table>




## SQL Query Language




### Joins
##### (INNER) JOIN (the default join)
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
  
- Both <code>customer_id</code> columns will remain in the result
- use <code>USING</code> when the column names(and type) match

##### NATURAL JOIN
- Automatically use the common column names to define the join relationship
- There must be at least one common attribute
- Delete duplicate columns and inconsistant tuples

```
SELECT c.customer_id id, o.amount
FROM customers c NATURAL JOIN orders o 
```


#### OUTER JOIN
##### LEFT JOIN 

RIGHT JOIN
  
FULL JOIN



### Views

Format:
```
CREATE VIEW <view_name> as <query expression>
```
Example:

```
CREATE VIEW **department_total_salary(name, total_salary)** AS
  SELECT dept_name, sum(salary)
  FROM instructor
  GROUP BY dept_name
```
Equivalent:
```
CREATE VIEW department_total_salary AS
  SELECT dept_name AS name, sum(salary) AS total_salary 
  FROM instructor
  GROUP BY name
```
Using views: (like a table)
```
SELECT * FROM department_total_salary
```
Delete views:
```
DROP VIEW (IF EXIST) <view_name>
```