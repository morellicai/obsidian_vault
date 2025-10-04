```SQL
SELECT cidades.nome, pessoas.nome, pessoas.idade
FROM pessoas, cidades
WHERE pessoas.cidade_id = cidades.id
+--------------+---------------------+-------+
| nome         | nome                | idade |
+--------------+---------------------+-------+
| São Paulo    | José Dias           |    80 |
| Brasilia     | Ana Carolina Santos |    36 |
| São Joaquim  | João do Carmo       |    69 |
| Brasilia     | Marcos Alves        |    20 |
| São Paulo    | Maria das Dores     |    82 |
| Brasilia     | Priscila da Silva   |    79 |
| São Joaquim  | Caio Morelli        |    24 |
+--------------+---------------------+-------+
```