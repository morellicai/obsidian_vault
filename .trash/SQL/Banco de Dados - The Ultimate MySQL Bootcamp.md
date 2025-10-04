---
tags:
  - Curso
---


```sql
GRANT ALL PRIVILEGES 
	ON data_base.table_name
	TO 'username'@'hostname' 
	IDENTIFIED BY 'password';
```


- `{sql} SHOW DATABASES;` : Mostras todos os bancos de dados
- `{sql} CREATE DATABASE data_base;` : Cria um banco de dados.
- `{sql} DROP DATABASE data_base;` : Deleta um banco de dados
- `{sql} USE data_base;` : Entra em um banco de dados
	- Não há comando para sair do banco de dados, más é possível usar o mesmo comando para ir para outro banco de dados.
- `{sql} SELECT DATABASE();` : Mostra qual banco está em uso
