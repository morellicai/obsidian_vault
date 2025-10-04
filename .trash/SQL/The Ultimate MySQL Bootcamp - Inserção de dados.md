---
tags:
  - Curso
---
```sql
INSERT INTO table_name(column_one, column_two)
VALUES (data_one, data_two);
```

Os dados tem que estarem de acordo com o tipo de dados da coluna que estão sendo inseridos.

- ==Não é necessário colocar todas as colunas da tabela se todas elas serão preenchidas== : `{sql} INSERT INTO table_name VALUE(...);`
- Caso um dado (varchar) tiver aspas (simples ou duplas) dentro é necessário especificar que não é o fechamento do dado com o escape. Exemplo:
	- `{sql} ... VALUES ('mario\'s pizza');` ()
	- Se for aspas duplas dentro de aspas simples não precisa do escape


[[The Ultimate MySQL Bootcamp - Múltiplas inserções de dados]]