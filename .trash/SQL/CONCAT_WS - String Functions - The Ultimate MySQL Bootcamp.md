---
tags:
  - Curso
aliases:
  - CONCAT_WS
---
CONCAT_WithSeparator 


`{sql} CONCAT_WS(separator,str1,str2,...);`


```sql
SELECT CONCAT_WS(', ', 'First name', 'Second name', 'Last Name');
+-----------------------------------------------------------+
| CONCAT_WS(', ', 'First name', 'Second name', 'Last Name') |
+-----------------------------------------------------------+
| First name, Second name, Last Name                        |
+-----------------------------------------------------------+

SELECT CONCAT_WS('-','Floor',NULL,'Room');
+------------------------------------+
| CONCAT_WS('-','Floor',NULL,'Room') |
+------------------------------------+
| Floor-Room                         |
+------------------------------------+
```
