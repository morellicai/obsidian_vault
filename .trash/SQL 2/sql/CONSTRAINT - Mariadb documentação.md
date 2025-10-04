MariaDB supports the implementation of constraints at the table-level using either [CREATE TABLE](https://mariadb.com/docs/server/reference/sql-statements/data-definition/create/create-table) or [ALTER TABLE](https://mariadb.com/docs/server/reference/sql-statements/data-definition/alter/alter-table) statements. A table constraint restricts the data you can add to the table. If you attempt to insert invalid data on a column, MariaDB throws an error.



## 0.1	Syntax


```sql
[CONSTRAINT [symbol]] constraint_expression

constraint_expression:
  | PRIMARY KEY [index_type] (index_col_name, ...) [index_option] ...
  | FOREIGN KEY [index_name] (index_col_name, ...) 
       REFERENCES tbl_name (index_col_name, ...)
       [ON DELETE reference_option]
       [ON UPDATE reference_option]
  | UNIQUE [INDEX|KEY] [index_name]
       [index_type] (index_col_name, ...) [index_option] ...
  | CHECK (check_constraints)

index_type:
  USING {BTREE | HASH | RTREE}

index_col_name:
  col_name [(length)] [ASC | DESC]

index_option:
  | KEY_BLOCK_SIZE [=] value
  | index_type
  | WITH PARSER parser_name
  | COMMENT 'string'
  | CLUSTERING={YES|NO}

reference_option:
  RESTRICT | CASCADE | SET NULL | NO ACTION | SET DEFAULT
```


## 0.2	Description

Constraints provide restrictions on the data you can add to a table. This allows you to enforce data integrity from MariaDB, rather than through application logic. When a statement violates a constraint, MariaDB throws an error.

There are four types of table constraints:

| Constraint  | Description                                                               |
| ----------- | ------------------------------------------------------------------------- |
| PRIMARY KEY | Sets the column for referencing rows. Values must be unique and not null. |
| FOREIGN KEY | Sets the column to reference the primary key on another table.            |
| UNIQUE      | Requires values in column or columns only occur once in the table.        |
| CHECK       | Checks whether the data meets the given condition.                        |

The [Information Schema TABLE_CONSTRAINTS Table](https://mariadb.com/docs/server/reference/system-tables/information-schema/information-schema-tables/information-schema-table_constraints-table) contains information about tables that have constraints.

### 0.2.1	FOREIGN KEY Constraints

[InnoDB](https://mariadb.com/docs/server/server-usage/storage-engines/innodb) supports [foreign key](https://mariadb.com/docs/server/ha-and-performance/optimization-and-tuning/optimization-and-indexes/foreign-keys) constraints. The syntax for a foreign key constraint definition in InnoDB looks like this:

```sql
[CONSTRAINT [symbol]] FOREIGN KEY
    [index_name] (index_col_name, ...)
    REFERENCES tbl_name (index_col_name,...)
    [ON DELETE reference_option]
    [ON UPDATE reference_option]

reference_option:
    RESTRICT | CASCADE | SET NULL | NO ACTION
```

The [Information Schema REFERENTIAL_CONSTRAINTS](https://mariadb.com/docs/server/reference/system-tables/information-schema/information-schema-tables/information-schema-referential_constraints-table) table has more information about foreign keys.

### 0.2.2	CHECK Constraints

Constraints are enforced. Before [MariaDB 10.2.1](https://mariadb.com/docs/release-notes/community-server/old-releases/release-notes-mariadb-10-2-series/mariadb-1021-release-notes) constraint expressions were accepted in the syntax but ignored.

You can define constraints in 2 different ways:

- `CHECK(expression)` given as part of a column definition.
    
- `CONSTRAINT [constraint_name] CHECK (expression)`
    

Before a row is inserted or updated, all constraints are evaluated in the order they are defined. If any constraint expression returns false, then the row will not be inserted or updated. One can use most deterministic functions in a constraint, including [UDFs](https://mariadb.com/docs/server/server-usage/user-defined-functions).


```sql
CREATE TABLE t1 (a INT CHECK (a>2), b INT CHECK (b>2), CONSTRAINT a_greater CHECK (a>b));
```

f you use the second format and you don't give a name to the constraint, then the constraint will get an automatically generated name. This is done so that you can later delete the constraint with [ALTER TABLE DROP constraint_name](https://mariadb.com/docs/server/reference/sql-statements/data-definition/alter/alter-table).

One can disable all constraint expression checks by setting the [check_constraint_checks](https://mariadb.com/docs/server/server-management/variables-and-modes/server-system-variables#check_constraint_checks) variable to `OFF`. This is useful for example when loading a table that violates some constraints that you want to later find and fix in SQL.

### 0.2.3	Replication

In [row-based](https://mariadb.com/docs/server/server-management/server-monitoring-logs/binary-log/binary-log-formats#row-based) [replication](https://github.com/mariadb-corporation/docs-server/blob/test/server/reference/sql-statements/data-definition/broken-reference/README.md), only the master checks constraints, and failed statements will not be replicated. In [statement-based](https://mariadb.com/docs/server/server-management/server-monitoring-logs/binary-log/binary-log-formats#statement-based) replication, the slaves will also check constraints. Constraints should therefore be identical, as well as deterministic, in a replication environment.

### 0.2.4	Auto_increment

[auto_increment](https://mariadb.com/docs/server/reference/data-types/auto_increment) columns are not permitted in check constraints. Before [MariaDB 10.2.6](https://mariadb.com/docs/release-notes/community-server/old-releases/release-notes-mariadb-10-2-series/mariadb-1026-release-notes), they were permitted, but would not work correctly. See [MDEV-11117](https://jira.mariadb.org/browse/MDEV-11117).

## 0.3	Examples


```sql
CREATE TABLE product (category INT NOT NULL, id INT NOT NULL,
                      price DECIMAL,
                      PRIMARY KEY(category, id)) ENGINE=INNODB;
CREATE TABLE customer (id INT NOT NULL,
                       PRIMARY KEY (id)) ENGINE=INNODB;
CREATE TABLE product_order (NO INT NOT NULL AUTO_INCREMENT,
                            product_category INT NOT NULL,
                            product_id INT NOT NULL,
                            customer_id INT NOT NULL,
                            PRIMARY KEY(NO),
                            INDEX (product_category, product_id),
                            FOREIGN KEY (product_category, product_id)
                              REFERENCES product(category, id)
                              ON UPDATE CASCADE ON DELETE RESTRICT,
                            INDEX (customer_id),
                            FOREIGN KEY (customer_id)
                              REFERENCES customer(id)) ENGINE=INNODB;
```

The following examples will work from [MariaDB 10.2.1](https://mariadb.com/docs/release-notes/community-server/old-releases/release-notes-mariadb-10-2-series/mariadb-1021-release-notes) onwards.

Numeric constraints and comparisons:


```sql
CREATE TABLE t1 (a INT CHECK (a>2), b INT CHECK (b>2), CONSTRAINT a_greater CHECK (a>b));

INSERT INTO t1(a) VALUES (1);
ERROR 4022 (23000): CONSTRAINT `a` failed for `test`.`t1`

INSERT INTO t1(a,b) VALUES (3,4);
ERROR 4022 (23000): CONSTRAINT `a_greater` failed for `test`.`t1`

INSERT INTO t1(a,b) VALUES (4,3);
Query OK, 1 row affected (0.04 sec)
```

Dropping a constraint:


```sql
ALTER TABLE t1 DROP CONSTRAINT a_greater;
```

Adding a constraint:


```sql
ALTER TABLE t1 ADD CONSTRAINT a_greater CHECK (a>b);
```


Date comparisons and character length:


```sql
CREATE TABLE t2 (name VARCHAR(30) CHECK (CHAR_LENGTH(name)>2), start_date DATE, 
  end_date DATE CHECK (start_date IS NULL OR end_date IS NULL OR start_date<end_date));

INSERT INTO t2(name, start_date, end_date) VALUES('Ione', '2003-12-15', '2014-11-09');
Query OK, 1 row affected (0.04 sec)

INSERT INTO t2(name, start_date, end_date) VALUES('Io', '2003-12-15', '2014-11-09');
ERROR 4022 (23000): CONSTRAINT `name` failed for `test`.`t2`

INSERT INTO t2(name, start_date, end_date) VALUES('Ione', NULL, '2014-11-09');
Query OK, 1 row affected (0.04 sec)

INSERT INTO t2(name, start_date, end_date) VALUES('Ione', '2015-12-15', '2014-11-09');
ERROR 4022 (23000): CONSTRAINT `end_date` failed for `test`.`t2`
```

A misplaced parenthesis:

```sql
CREATE TABLE t3 (name VARCHAR(30) CHECK (CHAR_LENGTH(name>2)), start_date DATE, 
  end_date DATE CHECK (start_date IS NULL OR end_date IS NULL OR start_date<end_date));
Query OK, 0 rows affected (0.32 sec)

INSERT INTO t3(name, start_date, end_date) VALUES('Io', '2003-12-15', '2014-11-09');
Query OK, 1 row affected, 1 warning (0.04 sec)

SHOW WARNINGS;
+---------+------+----------------------------------------+
| Level   | Code | Message                                |
+---------+------+----------------------------------------+
| Warning | 1292 | Truncated incorrect DOUBLE value: 'Io' |
+---------+------+----------------------------------------+
```

Compare the definition of table _t2_ to table _t3_. `CHAR_LENGTH(name)>2` is very different to `CHAR_LENGTH(name>2)` as the latter mistakenly performs a numeric comparison on the _name_ field, leading to unexpected results.