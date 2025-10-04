# Altering Tables Guide

This guide provides essential instructions for modifying existing table structures. Learn how to add, drop, and change columns, manage indexes and default values, and rename tables, along with key precautions for these operations when working with your database.

### Before You Begin: Backup Your Tables

Before making any structural changes to a table, especially if it contains data, **always create a backup**. The `mariadb-dump` utility is a common and effective tool for this.

Example: Backing up a single table

Suppose you have a database db1 and a table clients. Its initial structure is:

```sql
DESCRIBE clients;
+-------------+-------------+------+-----+---------+-------+
| Field       | Type        | Null | Key | Default | Extra |
+-------------+-------------+------+-----+---------+-------+
| cust_id     | int(11)     |      | PRI | 0       |       |
| name        | varchar(25) | YES  |     | NULL    |       |
| address     | varchar(25) | YES  |     | NULL    |       |
| city        | varchar(25) | YES  |     | NULL    |       |
| state       | char(2)     | YES  |     | NULL    |       |
| zip         | varchar(10) | YES  |     | NULL    |       |
| client_type | varchar(4)  | YES  |     | NULL    |       |
+-------------+-------------+------+-----+---------+-------+
```

To back up the `clients` table from the command-line:
`{sql} mariadb-dump --user='your_username' --password='your_password' --add-locks db1 clients > clients.sql`

- Replace `'your_username'` and `'your_password'` with your actual MariaDB credentials.
- `--add-locks`: Locks the table during the backup and unlocks it afterward.
- `db1 clients`: Specifies the database and then the table.
- `> clients.sql`: Redirects the output to a file named `clients.sql`.

### Adding Columns

Use the `ALTER TABLE` statement with the `ADD COLUMN` clause.

Add a column to the end of the table:

To add a status column with a fixed width of two characters:

```sql
ALTER TABLE clients
ADD COLUMN status CHAR(2);
```

Add a column after a specific existing column:

To add address2 (varchar 25) after the address column:

```sql
ALTER TABLE clients
ADD COLUMN address2 VARCHAR(25) AFTER address;
```

**Add a column to the beginning of the table:**

```sql
ALTER TABLE clients
ADD COLUMN new_first_column VARCHAR(50) FIRST;
```

_(Assuming_ `_new_first_column_` _is the one to be added at the beginning)._

After additions, the table structure might look like (excluding `new_first_column` for consistency with original example flow):

```sql
DESCRIBE clients;
+-------------+-------------+------+-----+---------+-------+
| Field       | Type        | Null | Key | Default | Extra |
+-------------+-------------+------+-----+---------+-------+
| cust_id     | int(11)     |      | PRI | 0       |       |
| name        | varchar(25) | YES  |     | NULL    |       |
| address     | varchar(25) | YES  |     | NULL    |       |
| address2    | varchar(25) | YES  |     | NULL    |       |
| city        | varchar(25) | YES  |     | NULL    |       |
| state       | char(2)     | YES  |     | NULL    |       |
| zip         | varchar(10) | YES  |     | NULL    |       |
| client_type | varchar(4)  | YES  |     | NULL    |       |
| status      | char(2)     | YES  |     | NULL    |       |
+-------------+-------------+------+-----+---------+-------+
```

### Changing Column Definitions

Use `ALTER TABLE` with `CHANGE` or `MODIFY`.

Change column type (e.g., to ENUM):

The status column name is specified twice even if not changing the name itself when using CHANGE.


```sql
ALTER TABLE clients
CHANGE status status ENUM('AC','IA');
```


Change column name and keep type:

To change status to active while keeping the ENUM definition:

```sql
ALTER TABLE clients
CHANGE status active ENUM('AC','IA');
```

When using `CHANGE`, the current column name is followed by the new column name and the complete type definition.

Modify column type or attributes without renaming:

Use MODIFY if you are only changing the data type or attributes, not the name.

```sql
ALTER TABLE clients
MODIFY address1 VARCHAR(40); -- Assuming 'address1' is an existing column
```

Complex Changes (e.g., ENUM migration with data):

Changing ENUM values in a table with existing data requires careful steps to prevent data loss. This typically involves:

1. Temporarily modifying the ENUM to include both old and new values.
    
2. Updating existing rows to use the new values.
    
3. Modifying the ENUM again to remove the old values.
    

Example of changing `address` to `address1` (40 chars) and preparing `active` ENUM for new values 'yes','no' from 'AC','IA':

```sql
ALTER TABLE clients
    CHANGE address address1 VARCHAR(40),
    MODIFY active ENUM('yes','no','AC','IA'); -- Temporarily include all
```


```sql
UPDATE clients
SET active = 'yes'
WHERE active = 'AC';

UPDATE clients
SET active = 'no'
WHERE active = 'IA';
```

Finally, restrict the ENUM to new values:
```sql
ALTER TABLE clients
MODIFY active ENUM('yes','no');
```

### Dropping Columns

To remove a column and its data (this action is permanent and irreversible without a backup):

```sql
ALTER TABLE clients
DROP COLUMN client_type;
```


### Managing Default Values

Set a default value for a column:

If most clients are in 'LA', set it as the default for the state column:

```sql
ALTER TABLE clients
ALTER state SET DEFAULT 'LA';
```

Remove a default value from a column:

This reverts the default to its standard (e.g., NULL if nullable, or determined by data type).

```sql
ALTER TABLE clients
ALTER state DROP DEFAULT;
```

This `DROP DEFAULT` does not delete existing data in the column.

