---
tags:
  - Curso
---
```sql
CREATE TABLE table_name (
	column_name data_type,
	column_name data_type
);
```

- É interessante a utilização de `{sql} NOT NULL` e `{sql} DEFAULT` juntos para impedir que seja inserido um valor `NULL` de proposito 
	- `{sql} INSERT INTO table_name(column_one, ...) VALUES(NULL, ...);` : seria aceito caso a coluna um não fosse configurada para não receber valores nulos.
	- É muito bom para segurança


[[Dado Obrigatório - The Ultimate MySQL Bootcamp]]

[[Valor Padrão - The Ultimate MySQL Bootcamp]]

[[The Ultimate MySQL Bootcamp - Primary Key]]

[[Auto Incremento - The Ultimate MySQL Bootcamp]]

[[Visualização - The Ultimate MySQL Bootcamp]]

[[The Ultimate MySQL Bootcamp - Deleção]]

[[The Ultimate MySQL Bootcamp - Inserção de dados]]

[[Seleção - The Ultimate MySQL Bootcamp]]

[[Update - The Ultimate MySQL Bootcamp]]

[[Delete - The Ultimate MySQL Bootcamp]]