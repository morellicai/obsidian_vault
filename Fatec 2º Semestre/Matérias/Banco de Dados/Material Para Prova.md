# O SQL
> Linguagem desenvolvida para "conversarmos" com o banco de dados.

## Todos:
- [[WHERE]]
- [[FUNÇÕES]]
- [[Juntando tabelas]]
- [[SELECT]]
- [[Módulo DDL]]
- [[JOIN]]

 
Podemos com o SQL:

- Criar e modificar Banco de dados
- Criar e modificar tabelas
- Criar e modificar permissões de acesso
- Criar e modificar Registro de Dados
- Gerenciar transações

> A SQL é organizada em subconjuntos com propósitos muito bem definidos.

São eles:

## **DDL - Data Definition Language**:
---
> Define os comandos para criação, exclusão e manutenção das tabelas e outras estruturas
---
- **CREATE**: Cria uma Tabela;
```SQL
CREATER TABLE PESSOAS(
  ID INT PRIMARY KEY AUTO_INCREMENT,
  CPF VARCHAR(20),
  NOME VARCHAR(20) NOT NULL,
  IDADE INT
);
```
- **ALTER**: Altera a Tabela;
- **DROP**: Exclui a Tabela;
```SQL
DROP TABLE PESSOAS;
```
## **DLC - Data Control Language**:
---
> Define os comandos utilizados para controlar o acesso aos dados do Banco de Dados
---
- **GRANT**: Concede acesso;
- **REVOKE**: Revoga (remove) o acesso;
## **DTL - Data Transaction Langueg**:
---
> Define os comando utilizados para gerenciar as transações executadas no Banco de dados;
---
- **BEGIN**: Inicia uma TRANSACTION
- **COMMIT**: Confirma uma TRANSACTION
- **ROLLBACK**: Desfaz uma TRANSACTION 
## DML - Data Manipulation Language:
---
> Define os comandos utilizados para manipulação dos dados;
---
- **INSERT**: Insere dados na Tabela;
 ```SQL
 INSERT INTO PESSOAS(CPF, NOME, IDADE)
 VALUES
  ('011.801.211-01', 'Maria Oliveira', 30),
  ('011.801.211-02', 'João da Silva', 40);
 ```
 
- **UPDATE**: Atualiza dados da Tabela;
```SQL
UPDATE PESSOAS
SET IDADE = 45
WHERE ID = 2; 
```
> Senão usarmos a claúsula `where`, toda a tabela `PESSOAS` será atualizada.

- **DELETE**: Exclui dados da tabela;
```SQL
DELETE FROM PESSOAS
WHERE ID = 2;
```
## **DQL - Data Query Language**:
---
> Define o comando utilizado para a realização das consultas dos dados; 
---
- **SELECT**: Consulta os dados em uma tabela
