---
tags:
  - Curso
---
Caso a coluna pode ser deixada em branco é possível colocar um valor padrão para que o campo não fique vazio.

```sql {4}
CREATE TABLE table_name (
	column_name data_type,
	column_name data_type NOT NULL,
	column_name data_type DEFAULT default_value
);
```


