---
tags:
  - Curso
aliases:
  - CONCAT
---


- `{sql} CONCAT(str1,str2,...);` : retorna uma string que é o resultado da concatenação dos argumentos (que são strings)
	- Geralmente usado com [[Seleção - The Ultimate MySQL Bootcamp|SELECT]] : `{sql} SELECT CONCAT(CAST(int_col AS CHAR), char_col);`


```sql
MariaDB [book_shop]> SELECT CONCAT(author_fname, ' ', author_lname) FROM books;
+-----------------------------------------+
| CONCAT(author_fname, ' ', author_lname) |
+-----------------------------------------+
| Jhumpa Lahiri                           |
| Neil Gaiman                             |
| Neil Gaiman                             |
| Jhumpa Lahiri                           |
| Dave Eggers                             |
| Dave Eggers                             |
| Michael Chabon                          |
| Patti Smith                             |
| Dave Eggers                             |
| Neil Gaiman                             |
| Raymond Carver                          |
| Raymond Carver                          |
| Don DeLillo                             |
| John Steinbeck                          |
| David Foster Wallace                    |
| David Foster Wallace                    |
+-----------------------------------------+
```


É possível fazer uma concatenação sem ter que ficar passando o separador toda vez que formos juntar mais uma coluna ou string : [[CONCAT_WS - String Functions - The Ultimate MySQL Bootcamp]]