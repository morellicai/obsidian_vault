The Essential Queries Guide offers a concise collection of commonly-used SQL queries. It's designed to help developers and database administrators quickly find syntax and examples for typical database operations, from table creation and data insertion to effective data retrieval and manipulation.

### Creating a Table

To create new tables:
`{sql} CREATE TABLE t1 ( a INT );`
`{sql} CREATE TABLE t2 ( b INT );`


```sql
CREATE TABLE student_tests (
 name CHAR(10), test CHAR(10),
 score TINYINT, test_date DATE
);
```

### Inserting Records

To add data into your tables:

`{sql} INSERT INTO t1 VALUES (1), (2), (3);`
`{sql} INSERT INTO t2 VALUES (2), (4);`

```sql
INSERT INTO student_tests
 (name, test, score, test_date) VALUES
 ('Chun', 'SQL', 75, '2012-11-05'),
 ('Chun', 'Tuning', 73, '2013-06-14'),
 ('Esben', 'SQL', 43, '2014-02-11'),
 ('Esben', 'Tuning', 31, '2014-02-09'),
 ('Kaolin', 'SQL', 56, '2014-01-01'),
 ('Kaolin', 'Tuning', 88, '2013-12-29'),
 ('Tatiana', 'SQL', 87, '2012-04-28'),
 ('Tatiana', 'Tuning', 83, '2013-09-30');
```

For more information, see the official INSERT documentation.

### Using AUTO_INCREMENT

The `AUTO_INCREMENT` attribute automatically generates a unique identity for new rows.

Create a table with an `AUTO_INCREMENT` column:

```sql
CREATE TABLE student_details (
 id INT NOT NULL AUTO_INCREMENT, name CHAR(10),
 date_of_birth DATE, PRIMARY KEY (id)
);
```

When inserting, omit the `id` field; it will be automatically generated:

```sql
INSERT INTO student_details (name,date_of_birth) VALUES
 ('Chun', '1993-12-31'),
 ('Esben','1946-01-01'),
 ('Kaolin','1996-07-16'),
 ('Tatiana', '1988-04-13');
```

Verify the inserted records:
`{sql} SELECT * FROM student_details;`


```sql
+----+---------+---------------+
| id | name    | date_of_birth |
+----+---------+---------------+
|  1 | Chun    | 1993-12-31    |
|  2 | Esben   | 1946-01-01    |
|  3 | Kaolin  | 1996-07-16    |
|  4 | Tatiana | 1988-04-13    |
+----+---------+---------------+
```

For more details, see the [AUTO_INCREMENT](https://mariadb.com/docs/server/reference/data-types/auto_increment) documentation.

### Querying from two tables on a common value (JOIN)

To combine rows from two tables based on a related column:

`{sql} SELECT * FROM t1 INNER JOIN t2 ON t1.a = t2.b;`

This type of query is a join. For more details, consult the documentation on [JOINS](https://mariadb.com/docs/server/reference/sql-statements/data-manipulation/selecting-data/joins-subqueries/joins).

### Finding the Maximum Value

To find the maximum value in a column:
`{sql} SELECT MAX(a) FROM t1;`

```sql
+--------+
| MAX(a) |
+--------+
|      3 |
+--------+
```

See the [MAX() function](https://mariadb.com/docs/server/reference/sql-functions/aggregate-functions/max) documentation. For a grouped example, refer to _Finding the Maximum Value and Grouping the Results_ below.

### Finding the Minimum Value

To find the minimum value in a column:
`{sql} SELECT MIN(a) FROM t1;`

```sql
+--------+
| MIN(a) |
+--------+
|      1 |
+--------+
```

See the MIN() function documentation.

### Finding the Average Value

To calculate the average value of a column:

`{sql} SELECT AVG(a) FROM t1;`

```sql
+--------+
| AVG(a) |
+--------+
| 2.0000 |
+--------+
```

See the [AVG() function](https://mariadb.com/docs/server/reference/sql-functions/aggregate-functions/avg) documentation.

### Finding the Maximum Value and Grouping the Results

To find the maximum value within groups:
`{sql} SELECT name, MAX(score) FROM student_tests GROUP BY name;`


```sql
+---------+------------+
| name    | MAX(score) |
+---------+------------+
| Chun    |         75 |
| Esben   |         43 |
| Kaolin  |         88 |
| Tatiana |         87 |
+---------+------------+
```

Further details are available in the MAX() function documentation.

### Ordering Results

To sort your query results (e.g., in descending order):

```sql
SELECT name, test, score FROM student_tests 
 ORDER BY score DESC; -- Use ASC for ascending order
```

```sql
+---------+--------+-------+
| name    | test   | score |
+---------+--------+-------+
| Kaolin  | Tuning |    88 |
| Tatiana | SQL    |    87 |
| Tatiana | Tuning |    83 |
| Chun    | SQL    |    75 |
| Chun    | Tuning |    73 |
| Kaolin  | SQL    |    56 |
| Esben   | SQL    |    43 |
| Esben   | Tuning |    31 |
+---------+--------+-------+
```

For more options, see the [ORDER BY](https://mariadb.com/docs/server/reference/sql-statements/data-manipulation/selecting-data/order-by) documentation.

### Finding the Row with the Minimum of a Particular Column

To find the entire row containing the minimum value of a specific column across all records:

```sql
SELECT name, test, score FROM student_tests 
 WHERE score = (SELECT MIN(score) FROM student_tests);
```

```sql
+-------+--------+-------+
| name  | test   | score |
+-------+--------+-------+
| Esben | Tuning |    31 |
+-------+--------+-------+
```

### Finding Rows with the Maximum Value of a Column by Group

To retrieve the full record for the maximum value within each group (e.g., highest score per student):
```sql
SELECT name, test, score FROM student_tests st1
 WHERE score = (SELECT MAX(st2.score) FROM student_tests st2 WHERE st1.name = st2.name);
```

```sql
+---------+--------+-------+
| name    | test   | score |
+---------+--------+-------+
| Chun    | SQL    |    75 |
| Esben   | SQL    |    43 |
| Kaolin  | Tuning |    88 |
| Tatiana | SQL    |    87 |
+---------+--------+-------+
```

