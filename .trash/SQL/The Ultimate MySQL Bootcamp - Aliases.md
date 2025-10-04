---
tags:
  - Curso
---


Um apelido para facilitar a escrita de um tabela ou coluna. Ou para dar um nome que faça sentido no  contexto da query

Exemplo:
`{sql} SELECT cat_id AS id, name FROM cats;`

Nesse exemplo estou nomeando a coluna `cat_id` como `id`, então se eu for chamar (dentro da mesma query) por `id` estarei chamando a coluna `cat_id`


Bom para diminuir a quantidade de digitação para fazer uma tarefa simples ou complicada, que por seguinte evita erros quando a query por muito grande.