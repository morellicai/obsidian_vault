This guide provides a quick overview of essential SQL statements in MariaDB, categorized by their function in data definition, data manipulation, and transaction control. Find brief descriptions and links to detailed documentation for each statement, along with a simple illustrative example sequence.

_(If you need a basic tutorial on how to use the MariaDB database server and execute simple commands, see_ [_A MariaDB Primer_](https://mariadb.com/docs/server/server-usage/basics/mariadb-usage-guide-1)_. Also see_ [_Essential Queries Guide_](https://mariadb.com/docs/server/mariadb-quickstart-guides/mariadb-advanced-sql-guide) _for examples of commonly-used queries.)_

### Defining How Your Data Is Stored (Data Definition Language - DDL)

- [**CREATE DATABASE**](https://mariadb.com/docs/server/reference/sql-statements/data-definition/create/create-database): Used to create a new, empty database.
    
- [**DROP DATABASE**](https://mariadb.com/docs/server/reference/sql-statements/data-definition/drop/drop-database): Used to completely destroy an existing database.
    
- **USE**: Used to select a default database for subsequent statements.
    
- [**CREATE TABLE**](https://mariadb.com/docs/server/reference/sql-statements/data-definition/create/create-table): Used to create a new table, which is where your data is actually stored.
    
- [**ALTER TABLE**](https://mariadb.com/docs/server/reference/sql-statements/data-definition/alter/alter-table): Used to modify an existing table's definition (e.g., add/remove columns, change types).
    
- [**DROP TABLE**](https://mariadb.com/docs/server/reference/sql-statements/data-definition/drop/drop-table): Used to completely destroy an existing table and all its data.
    
- [**DESCRIBE**](https://mariadb.com/docs/server/reference/sql-statements/administrative-sql-statements/describe) (or `DESC`): Shows the structure of a table (columns, data types, etc.).
    

### Manipulating Your Data (Data Manipulation Language - DML)

- [**SELECT**](https://mariadb.com/docs/server/reference/sql-statements/data-manipulation/selecting-data/select): Used when you want to read (or select) your data from one or more tables.
    
- [**INSERT**](https://mariadb.com/docs/server/reference/sql-statements/data-manipulation/inserting-loading-data/insert): Used when you want to add (or insert) new rows of data into a table.
    
- [**UPDATE**](https://mariadb.com/docs/server/reference/sql-statements/data-manipulation/changing-deleting-data/update): Used when you want to change (or update) existing data in a table.
    
- [**DELETE**](https://mariadb.com/docs/server/reference/sql-statements/data-manipulation/changing-deleting-data/delete): Used when you want to remove (or delete) existing rows of data from a table.
    
- [**REPLACE**](https://mariadb.com/docs/server/reference/sql-statements/data-manipulation/changing-deleting-data/replace): Works like `INSERT`, but if an old row in the table has the same value as a new row for a `PRIMARY KEY` or a `UNIQUE` index, the old row is deleted before the new row is inserted.
    
- [**TRUNCATE TABLE**](https://mariadb.com/docs/server/reference/sql-statements/table-statements/truncate-table): Used to quickly remove all data from a table, resetting any `AUTO_INCREMENT` values. It is faster than `DELETE` without a `WHERE` clause for emptying a table.
    

### Transactions (Transaction Control Language - TCL)

- [**START TRANSACTION**](https://mariadb.com/docs/server/reference/sql-statements/transactions/start-transaction) (or `BEGIN`): Used to begin a new transaction, allowing multiple SQL statements to be treated as a single atomic unit.
    
- [**COMMIT**](https://mariadb.com/docs/server/reference/sql-statements/transactions/commit): Used to save all changes made during the current transaction, making them permanent.
    
- [**ROLLBACK**](https://mariadb.com/docs/server/reference/sql-statements/transactions/rollback): Used to discard all changes made during the current transaction, reverting the database to its state before the transaction began.