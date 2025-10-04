Temos em SQL algumas funções embutidas que realizam algum tipo de processamento. 

| Função | Descrição                         |
| ------ | --------------------------------- |
| AVG    | Retorna o valor da média do grupo |
| MIN    | Retorna o Menor valor             |
| MAX    | Retorna o Maior valor             |
| SUM    | Retorna a soma                    |
| COUNT  | Retorna a Quantidade de linhas    |
### AVG
Podemos pegar a média da idade de todas as pessoas da tabela:
``` SQL
> select avg(idade) from pessoas;
+------------+
| avg(idade) |
+------------+
|    55.7143 |
+------------+
```
### MIN
Podemos pegar a menor idade registrada na tabela pessoas:
```SQL
> select min(idade) from pessoas;
+------------+
| min(idade) |
+------------+
|         20 |
+------------+
```
### MAX
Podemos pegar a maior idade registrada na tabela pessoas:
```SQL
> select max(idade) from pessoas;
+------------+
| max(idade) |
+------------+
|         82 |
+------------+
```
### SUM
Podemos pegar a soma da idade de todas as pessoas registrada na tabela pessoas:
```SQL
> select sum(idade) from pessoas;
+------------+
| sum(idade) |
+------------+
|        390 |
+------------+
```
### COUNT
Podemos pegr a quantidade de linhas inseridas na tabela pessoas:
```SQL
> select count(*) from pessoas;
+----------+
| count(*) |
+----------+
|        7 |
+----------+
```

