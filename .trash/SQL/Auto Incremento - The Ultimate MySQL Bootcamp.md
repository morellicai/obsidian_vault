---
tags:
  - Curso
---

`{sql} AUTO_INCREMENT`
- Não precisa passa o valor
- Não impede de um valor ser inserido manualmente
- Tira a necessidade de usar o [[Dado Obrigatório - The Ultimate MySQL Bootcamp |NOT NULL]]



```sql {3}
CREATE TABLE table_name (
	column_name data_type,
	column_name_id data_type NOT NULL AUTO_INCREMENT,
	column_name data_type DEFAULT default_value,
	PRIMARY KEY (column_name_id)
);
```
