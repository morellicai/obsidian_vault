---
tags:
  - Curso
---
> Selecione primeiro o que você pretende atualizar antes de fazer uma atualização
- Caso seja desejado atualizar somente uma linha tente usar o valor ==único== dela

[[The Ultimate MySQL Bootcamp - Clausula Where]]

```sql {1}
UPDATE cats SET breed='Shorthair'
WHERE breed = 'Tabby';
```

Essa query serve para atualizar uma tabela inteira, caso seja amplo, ou específico, caso esteja usando um id.



```sql
UPDATE table_name SET column1 = data_
WHERE column1 = condition
```
- SET : usado para trocar os valores de uma coluna 


- Para atualizar múltiplas colunas é só separar com virgular:
`{sql} UPDATE employees SET current_status = 'Laid-off', last_name= 'who cares';`


