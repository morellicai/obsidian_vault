---
tags:
  - Curso
---
[Docs](https://www.tutorialspoint.com/sql/sql-primary-key.htm)


```sql {3}
CREATE TABLE table_name (
	column_name data_type,
	column_name_id data_type NOT NULL PRIMARY KEY,
	column_name data_type DEFAULT default_value
);
```

ou 


```sql {3, 5}
CREATE TABLE table_name (
	column_name data_type,
	column_name_id data_type NOT NULL,
	column_name data_type DEFAULT default_value,
	PRIMARY KEY (column_name_id)
);
```
