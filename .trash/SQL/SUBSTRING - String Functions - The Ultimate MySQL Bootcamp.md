---
tags:
  - Curso
aliases:
  - SUBSTR
  - SUBSTRING
---
Faz uma nova string a partir de uma string passada, ou seja, um recorte da original.
Utilizado com [[Seleção - The Ultimate MySQL Bootcamp |SELECT]]


`{sql} SUBSTRING(str FROM pos FOR len)`
- `str` : string desejada, pode ser uma coluna
	- `str` = String, coluna
- `FROM pos` : a posição que é a nova string começa ( não é index!!! )
	- `pos` = Número
	- Pode ser um número negativo
- `FOR len` : o tamanho da sub-string
	- `len` = Número
- Essa forma é a padrão da sintaxe do SQL


Também pode ser escrito dessa forma: 
- `{sql} SUBSTRING(str, pos, len);` 
	- Note que cada item é separado por vírgula!
- `{sql} SUBSTR(str FROM pos FOR len)`
- `{sql} SUBSTR(str, pos, len)`


# Exemplo

```sql

MariaDB [book_shop]> SELECT SUBSTRING(title FROM 1 FOR 15) FROM books;
+--------------------------------+
| SUBSTRING(title FROM 1 FOR 15) |
+--------------------------------+
| The Namesake                   |
| Norse Mythology                |
| American Gods                  |
| Interpreter of                 |
| A Hologram for                 |
| The Circle                     |
| The Amazing Adv                |
| Just Kids                      |
| A Heartbreaking                |
| Coraline                       |
| What We Talk Ab                |
| Where I'm Calli                |
| White Noise                    |
| Cannery Row                    |
| Oblivion: Stori                |
| Consider the Lo                |
+--------------------------------+
```
