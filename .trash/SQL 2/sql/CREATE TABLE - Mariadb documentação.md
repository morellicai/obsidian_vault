## Syntax

```sql
CREATE [OR REPLACE] [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
    (create_definition,...) [table_options    ]... [partition_options]
CREATE [OR REPLACE] [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
    [(create_definition,...)] [table_options   ]... [partition_options]
    select_statement
CREATE [OR REPLACE] [TEMPORARY] TABLE [IF NOT EXISTS] tbl_name
   { LIKE old_table_name | (LIKE old_table_name) }

select_statement:
    [IGNORE | REPLACE] [AS] SELECT ...   (Some legal select statement)
```


## Description

Use the `CREATE TABLE` statement to create a table with the given name.

In its most basic form, the `CREATE TABLE` statement provides a table name followed by a list of columns, indexes, and constraints. By default, the table is created in the default database. Specify a database with `db_name.tbl_name`. If you quote the table name, you must quote the database name and table name separately as `` `db_name`.`tbl_name` ``. This is particularly useful for [CREATE TABLE ... SELECT](https://mariadb.com/docs/server/reference/sql-statements/data-definition/create/create-table#create-table-select), because it allows to create a table into a database, which contains data from other databases. See [Identifier Qualifiers](https://mariadb.com/docs/server/reference/sql-structure/sql-language-structure/identifier-qualifiers).

If a table with the same name exists, error 1050 results. Use [IF NOT EXISTS](https://mariadb.com/docs/server/reference/sql-statements/data-definition/create/create-table#create-table-if-not-exists) to suppress this error and issue a note instead. Use [SHOW WARNINGS](https://mariadb.com/docs/server/reference/sql-statements/administrative-sql-statements/show/show-warnings) to see notes.

The `CREATE TABLE` statement automatically commits the current transaction, except when using the [TEMPORARY](https://mariadb.com/docs/server/reference/sql-statements/data-definition/create/create-table#create-temporary-table) keyword.

For valid identifiers to use as table names, see [Identifier Names](https://mariadb.com/docs/server/reference/sql-structure/sql-language-structure/identifier-names).

If the `default_storage_engine` is set to `ColumnStore` , it needs setting on all UMs. Otherwise when the tables using the default engine are replicated across UMs, they will use the wrong engine. You should therefore not use this option as a session variable with ColumnStore.

[Microsecond precision](https://mariadb.com/docs/server/reference/sql-functions/date-time-functions/microseconds-in-mariadb) can be between 0-6. If no precision is specified it is assumed to be 0, for backward compatibility reasons.

## Privileges

Executing the `CREATE TABLE` statement requires the [CREATE](https://mariadb.com/docs/server/reference/sql-statements/account-management-sql-statements/grant#table-privileges) privilege for the table or the database.

## CREATE OR REPLACE

If the `OR REPLACE` clause is used and the table already exists, then instead of returning an error, the server will drop the existing table and replace it with the newly defined table.

This syntax was originally added to make [replication](https://mariadb.com/docs/server/ha-and-performance/standard-replication) more robust if it has to rollback and repeat statements such as `CREATE ... SELECT` on replicas.

```
CREATE OR REPLACE TABLE table_name (a INT);
```

is basically the same as:

```
DROP TABLE IF EXISTS TABLE_NAME;
CREATE TABLE TABLE_NAME (a INT);
```

with the following exceptions:

- If `table_name` was locked with [LOCK TABLES](https://mariadb.com/docs/server/reference/sql-statements/transactions/lock-tables) it will continue to be locked after the statement.
    
- Temporary tables are only dropped if the `TEMPORARY` keyword was used. (With [DROP TABLE](https://mariadb.com/docs/server/reference/sql-statements/data-definition/drop/drop-table), temporary tables are preferred to be dropped before normal tables).
    

### Things to be Aware of With CREATE OR REPLACE

- The table is dropped first (if it existed), after that the `CREATE` is done. Because of this, if the `CREATE` fails, then the table will not exist anymore after the statement. If the table was used with `LOCK TABLES` it will be unlocked.
    
- One can't use `OR REPLACE` together with `IF EXISTS`.
    
- [Replicas](https://mariadb.com/docs/server/ha-and-performance/standard-replication) will by default use `CREATE OR REPLACE` when replicating `CREATE` statements that don''t use `IF EXISTS`. This can be changed by setting the variable [slave-ddl-exec-mode](https://mariadb.com/docs/server/ha-and-performance/standard-replication/replication-and-binary-log-system-variables) to `STRICT`.
    

## CREATE TABLE IF NOT EXISTS

If the `IF NOT EXISTS` clause is used, then the table will only be created if a table with the same name does not already exist. If the table already exists, then a warning will be triggered by default.

## CREATE TEMPORARY TABLE

Use the `TEMPORARY` keyword to create a temporary table that is only available to the current session. Temporary tables are dropped when the session ends. Temporary table names are specific to the session. They will not conflict with other temporary tables from other sessions even if they share the same name. They will shadow names of non-temporary tables or views, if they are identical. A temporary table can have the same name as a non-temporary table which is located in the same database. In that case, their name will reference the temporary table when used in SQL statements. You must have the [CREATE TEMPORARY TABLES](https://mariadb.com/docs/server/reference/sql-statements/account-management-sql-statements/grant#database-privileges) privilege on the database to create temporary tables. If no storage engine is specified, the [default_tmp_storage_engine](https://mariadb.com/docs/server/server-management/variables-and-modes/server-system-variables#default_tmp_storage_engine) setting will determine the engine.