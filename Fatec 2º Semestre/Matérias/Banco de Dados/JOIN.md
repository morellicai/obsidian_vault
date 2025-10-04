# Inner Join
> É o ato de mesclar linhas de tabelas de acordo com determinada condição. Ele permite mesclar tabelas relacionadas

Sintaxe:
```SQL
SELECT
	column1,
	column2
FROM
	table1
	INNER JOIN table2 ON condition;
```

- Primeiro selecionamos as colunas e a tabela que queremos passar primeiro para a comparação,
- Depois, na cláusula INNER JOIN, passamos a tabela que relacionará
- E a condição vem após
## Exemplo:
Suponha que temos duas tabelas `employees` e `departments`. A tabela employees está assim:

| employee_id | name  | departmend_id |
| ----------- | ----- | ------------- |
| 1           | Jane  | 1             |
| 2           | Bob   | 2             |
| 3           | Maria | NULL          |
E departments está assim:

| departmend_id | department_name |
| ------------- | --------------- |
| 1             | Sales           |
| 2             | Marketin        |
Para que eu junte as duas, posso usar o `inner join` dessa maneira:

```SQL
SELECT
	employee_id,
	name,
	department_name
FROM
	employees
	INNER JOIN departmens ON 
		departments.department_id = employees.department_id;
```
**OUTPUT**:
```SQL
 employee_id | name | department_name
-------------+------+-----------------
           1 | Jane | Sales
           2 | Bob  | Marketing
```
Não preciso utilizar apenas o `=`, é possivel utilizar todos os operadores de comparação e logico do SQL.
- Se preciso utilizar varias condições, posso usar o comparador lógico `AND`