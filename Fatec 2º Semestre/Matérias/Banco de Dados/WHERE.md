Usamos a cláusula WHERE para filtrar os dados. Para isso, usamos operadores de comparação e Operadores Lógicos
## Operadores de Comparação

| Operador  | Significado      |
| --------- | ---------------- |
| =         | Igual a          |
| < > ou != | Não igual a      |
| <         | Menor que        |
| >         | Maior que        |
| <=        | Menos ou igual a |
| >=        | Maior ou igual a |

Exemplos:
```SQL
-> select *  from pessoas where idade = 80;
+----+------------+-------+-----------+
| id | nome       | idade | cidade_id |
+----+------------+-------+-----------+
|  5 | José Dias  |    80 |         2 |
+----+------------+-------+-----------+

-> select *
-> from pessoas 
-> where nome = 'Caio Morelli';
+----+--------------+-------+-----------+
| id | nome         | idade | cidade_id |
+----+--------------+-------+-----------+
| 11 | Caio Morelli |    24 |         3 |
+----+--------------+-------+-----------+

-> Select *
-> from pessoas
-> where idade > 70;
+----+-------------------+-------+-----------+
| id | nome              | idade | cidade_id |
+----+-------------------+-------+-----------+
|  5 | José Dias         |    80 |         2 |
|  9 | Maria das Dores   |    82 |         2 |
| 10 | Priscila da Silva |    79 |         1 |
+----+-------------------+-------+-----------+
```
## Operadores Lógicos

| Operador | Significado                                                 |
| -------- | ----------------------------------------------------------- |
| IN       | Retorna 1 se o valor testado estiver na lista               |
| LIKE     | Retorna 1 se o valor testado coincidir com o padrão passado |
| AND      | Retorna 1 se as duas expressões testadas forem 1            |
| OR       | Retorna 1 se ao menos uma das expressões testadas forem 1   |
| BETWEEN  | Retorna 1 se o valor testado estiver no intervalo passado   |
Exemplos:
```SQL
> select * from pessoas where idade IN(30, 80);
+----+------------+-------+-----------+
| id | nome       | idade | cidade_id |
+----+------------+-------+-----------+
|  5 | José Dias  |    80 |         2 |
+----+------------+-------+-----------+

> select * from pessoas where nome LIKE '%Silva%';
+----+-------------------+-------+-----------+
| id | nome              | idade | cidade_id |
+----+-------------------+-------+-----------+
| 10 | Priscila da Silva |    79 |         1 |
+----+-------------------+-------+-----------+
MariaDB [tabelas]> select * from pessoas
-> where idade > 30 and cidade_id = 1;
+----+---------------------+-------+-----------+
| id | nome                | idade | cidade_id |
+----+---------------------+-------+-----------+
|  6 | Ana Carolina Santos |    36 |         1 |
| 10 | Priscila da Silva   |    79 |         1 |
+----+---------------------+-------+-----------+
MariaDB [tabelas]> select * from pessoas
    -> where idade = 30 or cidade_id = 3;
+----+----------------+-------+-----------+
| id | nome           | idade | cidade_id |
+----+----------------+-------+-----------+
|  7 | João do Carmo  |    69 |         3 |
| 11 | Caio Morelli   |    24 |         3 |
+----+----------------+-------+-----------+
MariaDB [tabelas]> select * from pessoas
    -> where idade between 30 and 39;
+----+---------------------+-------+-----------+
| id | nome                | idade | cidade_id |
+----+---------------------+-------+-----------+
|  6 | Ana Carolina Santos |    36 |         1 |
+----+---------------------+-------+-----------+
```
- [[Módulo DDL]] -> La vai ter mais alguns detalher sobre algumas formas que temos de usar os operadores

## Order By
Comando que ordena os resultados por ordem crescente de acordo com a tabela ASCII
- Exemplo:
```SQL
MariaDB [tabelas]> select * from
    -> pessoas order by idade;
+----+---------------------+-------+-----------+
| id | nome                | idade | cidade_id |
+----+---------------------+-------+-----------+
|  8 | Marcos Alves        |    20 |         1 |
| 11 | Caio Morelli        |    24 |         3 |
|  6 | Ana Carolina Santos |    36 |         1 |
|  7 | João do Carmo       |    69 |         3 |
| 10 | Priscila da Silva   |    79 |         1 |
|  5 | José Dias           |    80 |         2 |
|  9 | Maria das Dores     |    82 |         2 |
+----+---------------------+-------+-----------+
```
> Repare que a ordem foi estabelecida pelo valor da idade. De forma crescente

Também podemos ver por ordem decrescente
```SQL
MariaDB [tabelas]> select * from 
	-> pessoas order by idade desc;
+----+---------------------+-------+-----------+
| id | nome                | idade | cidade_id |
+----+---------------------+-------+-----------+
|  9 | Maria das Dores     |    82 |         2 |
|  5 | José Dias           |    80 |         2 |
| 10 | Priscila da Silva   |    79 |         1 |
|  7 | João do Carmo       |    69 |         3 |
|  6 | Ana Carolina Santos |    36 |         1 |
| 11 | Caio Morelli        |    24 |         3 |
|  8 | Marcos Alves        |    20 |         1 |
+----+---------------------+-------+-----------+
```

[[FUNÇÕES]]
