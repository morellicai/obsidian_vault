---
tags:
  - PHP
---
# O primeiro programa em PHP - CAP 2

Um resumo sobre este capitulo:
- Neste capitulo do livro aprendi como instalar o PHP e utilizar o xampp (mesmo não usando em minha máquina, Sempre muito bom aprender para poder utilizar se necessário em algum dia)
- Também fiz meu primeiro código:
	- O código nada mais do que é uma função que retorna o dia e a hora
- Aprendi também como e onde estão minhas configurações do PHP
	- Que se encontram em `/etc/php/`
- Aprendi que a instrução `echo` é utilizada para imprimir algo (seja no navegador quando no terminal)
- toda linha de instrução termina com `;`
## Desafio do capitulo

1. Na função `date()`, experimente mudar o Y para y. O que acontece?
	- R: Em ver de 2025 ele está abreviando por 25
2. Consigo exibir a hora no formato de 12 horas, am e pm?
	- R: Na função date, adiciona um A no final e muda de H para h na hora
3. E se você tivesse que exibir o dia da semana? como seria?
	- R: Adiciono outra chamada a função date com o parâmetro "l"
	- Problema é que ele vem em inglês na resposta. Então teria que traduzir de alguma forma se fosse utilizar a função nativa do php
4. Exiba quantos dias faltam para o próximo sábado:
	- R: Para isso, precisava usar o parâmetro "w" para conseguir o valor em numero do dia atual dinamicamente, e diminuir até o dia desejado, que no caso é 6
5. Exiba também o nome do mês atual
	- R: Parâmetro usado para essa é o "F"