> Quando usamos o comando SELECT, estamos selecionando uma parte da tabela que gostaríamos de visualizar. Essa visualização é chamada de _result-set_ ou _Conjunto de Dados_

### Selecionando os Dados
```SQL
SELECT * FROM tabelaX;
```
- **SELECT**: Declaração de consulta de dados;
- **FROM**: De qual tabela será a visualização
> Quando passado o `*` é para visualizar todas as colunas da tebela]
- Exemplo de Saída:

```SQL
MariaDB [tabelas]> select * from pessoas;
+----+---------------------+-------+-----------+
| id | nome                | idade | cidade_id |
+----+---------------------+-------+-----------+
|  5 | José Dias           |    80 |         2 |
|  6 | Ana Carolina Santos |    36 |         1 |
|  7 | João do Carmo       |    69 |         3 |
|  8 | Marcos Alves        |    20 |         1 |
|  9 | Maria das Dores     |    82 |         2 |
| 10 | Priscila da Silva   |    79 |         1 |
| 11 | Caio Morelli        |    24 |         3 |
+----+---------------------+-------+-----------+
```

Podemos ver colunas especificas:
```SQL
SELECT column1, column2 FROM tabelaX;
```
- Exemplo:
```SQL
MariaDB [tabelas]> select nome, idade from pessoas;
+---------------------+-------+
| nome                | idade |
+---------------------+-------+
| José Dias           |    80 |
| Ana Carolina Santos |    36 |
| João do Carmo       |    69 |
| Marcos Alves        |    20 |
| Maria das Dores     |    82 |
| Priscila da Silva   |    79 |
| Caio Morelli        |    24 |
+---------------------+-------+
```

- Podemos ver que a seleção está filtrada apenas para ver os nomes e idade. As colunas que indiquei no select.

Podemos fazer seleções de uma coluna só dos dados:
```SQL
SELECT DISTINCT(column1) from tabelaX;
```
- Exemplo:
```SQL
MariaDB [tabelas]> select distinct(cidade_id) 
 -> from pessoas;
+-----------+
| cidade_id |
+-----------+
|         2 |
|         1 |
|         3 |
+-----------+
```