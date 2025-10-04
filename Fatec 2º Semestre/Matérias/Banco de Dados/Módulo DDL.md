# Indice
- [[#Comandos DDL]]
- [[#Comandos úteis]]
- [[#Alguns tipos de dados]]
- [[#Constraints]]
- [[#Exemplo de criação com PK]]
- [[#Exemplo de criação com PK Composta]]
- [[#Integridade Referencial]]
- [[#Not Null]]
- [[#CHECK]]
- [[#UNIQUE]]
- [[#Desativando e removendo constraints]]
- [[#Excluindo tabelas]]
- [[#CLÁUSULA]]
- [[#Cláusula Where]]
- [[#Cláusula Default]]
- [[#Operações SQL]]

# Comandos DDL
- `CREATE TABLE` -> criar uma tabela
- `CREATE INDEX` -> cria um índice
- `ALTER TABLE`  -> Altera ou insere uma coluna em uma tabela
- `ALTER INDEX`  -> Altera um índice
- `DROP TABLE`   -> Elimina uma tabela
- `DROP INDEX`   -> Elimina um índice

## Comandos úteis
- Listar todos os usuários:
	- `SELECT * FROM ALL_USERS;`
- Lista todas as tabelas:
	- `SELECT TABLE_NAME FROM USER_TABLES;` 
- Mostra usuário atual:
	- `SHOW USER`
## Alguns tipos de dados
- **Char** -> Cadeira de caracteres de tamanho fixo n. O dfault é 1 e o máximo é 255.
- **varchar2(n)** -> Cadeia de caracteres de tamanho variável. Tamanho máximo 4000
- **varchar(n)** -> Idem ao tipo 2, porém usa todo espaço mesmo o não preenchido
	- Aloca memória mesmo sem uso
- **long** -> Cadeira de caracteres de tamanho variável. Tamanho máximo 2GB. Só pode existir um campo deste tipo por tabela.
- **raw e long raw** -> Equivalente o varchar2 w long, respectivamente. Utilizado para armazenar dados binários (sons, imagens, etc.) Limite: 2000 bytes.
- **number(p,e)** -> Valores numéricos. Ex: number(5,2) armazena -999,99 a 999,99
- **date** -> Armazena data e hora (inclusive minuto e segundo). Ocupam 7 bytes
[Tabela detalhada e outros tipos](https://docs.oracle.com/en/cloud/paas/nosql-cloud/rnpxl/index.html#GUID-833B2B2A-1A32-48AB-A19E-413EAFB964B8)
## Constraints
- As restrições (contraints) estabelecem as relações entre as várias tabelas em um banco de dados e realizam três tarefas fundamentais:
	- Mantém a integridade dos dados
	- Não permitem a inclusão de valores incorretos
	- Impedem a exclusão de dados se existirem dependências entre tabelas
**CHAVE PRIMÁRIA (PK - PRIMARY KEY)**
- Coluna ou grupo de colunas que permite identificar uma única linha da tabela
- Também é a referencia para relação com outras tabelas
#### Exemplo de criação com PK
```sql
CREATE TABLE tabela1(
	coluna1 NUMBER(5), 
	coluna2 VARCHAR2(30), 
	CONSTRAINT tabela1_pk PRIMARY KEY(coluna1)
);
```
#### Exemplo de criação com PK Composta
```sql
CREATE TABLE tabela1(
	coluna1 NUMBER(5), 
	coluna2 VARCHAR(30),
	CONSTRAINT tabela1_pk PRIMARY KEY(coluna1,coluna2)
)
```
## Integridade Referencial
> Coluna que estabelece o relacionamento entre duas tabelas, gerando a chamada integridade referencial entre elas. O que significa que para inserir uma linha na tabela "filha", deve necessariamente existir a linha de ligação na tabela "pai".

#### Exemplo
Supondo a criação das tabelas eng e projeto
```sql
create table eng(
	id_eng number(8) primary key,
	nome varchar2(20) not null
);

create table projeto(
	id_proj numnber(9) primary key,
	data_proj date,
	valor_proj number(12,2),
	id_eng number(8),
	contraint pk_eng foreign key(id_eng) references eng(id_eng)
)
```
**Explicação para essa contraint**:
- pk_eng -> nome da contraint
- foreign key(id_eng) -> Referencia de outra tabela, no caso, a chave primaria da tabela eng
- references eng(id_eng) -> Referencia da foreign key na tabela projeto é id_eng
## Not Null
> NOT NULL -> Indica que o conteúdo de uma coluna não poderá ser vazia (nulo)

```sql
create table tabela4(
	coluna1 NUMBER(5),
	coluna2 VARCHAR(30) NOT NULL
);
```
A declaração é que a coluna 2 não pode não ser inserida algum dado. Se inserir na linha, tem que inserir algum dado na coluna2, sempre respeitando seu tipo e sua necessidade
## CHECK
> Define um domínio de valores para o conteúdo da coluna.
#### Exemplos
```sql
create table tabela6(
coluna1 number(5),
	coluna2 char(1) contraint tabela6_ch check(coluna2='M'OR coluna2='F')
);

create table6(
	coluna1 number(5),
	coluna2 char(2) constraint tabela6_ch check(coluna2 IN('SP','RJ','MG'))
);

create table6(
	coluna1 number(5),
	coluna2 number(5) contraint tabela6_ch check(coluna2<1000)
);
```
## UNIQUE
> Indica que não poderá haver repetição no conteúdo da coluna. Funciona como a chave primária, mas permite nulos.
#### Exemplos
```sql
create table tabela5(
	coluna1 number(5),
	coluna2 varchar2(30) unique
);

create table tabela5(
	coluna1 number(5),
	coluna2 varchar2(30) contraint tabela5_un unique
);
```
# Desativando e removendo constraints
- Desativando constraints
```sql
ALTER TABLE tabela1 DISABLE CONSTRAINT tabela1_pk;
```
- Ativando constraints
```sql
ALTER TABLE tabela1 ENABLE CONSTRAINT tabela1_pk;
```

> **Alerta**: _Se uma constraint for desativada e forem inclusos dados que violariam a constraint, isso impedirá a reativação da constraint. Ou seja, ela só poderá ser reativada caso esses dados que violam, não tenham sido inseridos._

- Removendo constraints
```sql
ALTER TABLE tabela1 DROP CONSTRAINT tabela1_pk;
```
- Adicionando Constraints
```sql
ALTER TABLE tabela1 ADD CONSTRAINT tabela1_pk PRIMARY KEY(coluna1)
```
# Excluindo tabelas
Para excluir uma tabela utilizamos o comando `DROP TABLE`:
```sql
DROP TABLE tabela1;
DROP TABLE tabela2 CASCADE CONSTRAINTS;
```

# CLÁUSULA
- `ON DELETE SET NULL` -> Quando for removido um valor da tabela-pai, o Oracle define os valores correspondentes da tabela-filho como NULL.
- `ON DELETE CASCADE` -> Quando for removido um valor da tabela-pai o Oracle remove os valores correspondentes da tabela-filho.
- `DEFAULT` -> Atribui um conteúdo padrão a uma coluna da tabela.
### ON DELETE CASCADE, SET NULL E DEFAULT
```sql
CREATE TABLE tabela2(
	coluna1 NUMBER(5), 
	colunaX NUMBER(5),
	CONSTRAINT tabela2_pk PRIMATY KEY(coluna1),
	CONSTRAINT tabela2_fk FOREIGN KEY(colunaX) REFERENCES tabela1(coluna1)
);

CREATE TABLE tabela2(
	coluna1 NUMBER(5), 
	colunaX NUMBER(5),
	CONSTRAINT tabela2_pl PRIMARY KEY(coluna1),
	CONSTRAINT tabela2_fk FOREIGN KEY(colunaX) REFERENCES tabela1(colunaX) ON DELETE SET NULL
);

CREATE TABLE tabela2(
	coluna1 NUMBER(5),
	colunaX NUMBER(5),
	CONSTRAINT tabela2_pk PRIMARY KEY(coluna1),
	CONSTRAINT tabela2_fk FOREIGN KEY(colunaX) REFERENCES tabela1(coluna1) ON DELETE CASCADE
);

CREATE TABLE tabela3(
	coluna1 NUMBER(5),
	colunaX NUMBER(5) DEFAULT 1,
	coluna3 VARCHAR2(10) DEFAULT 'a',
	coluna4 DATE DEFAULT SYSDATE 
);

```
## Cláusula Default
- Caso o usuário não preenche o campo, definimos um valor que a tabela deve registrar como padrão
	- Exemplo um evento onde 99% dos participantes são brasileiros, podemos criar a tabela seguinte:  
```sql
CREATE TABLE participante(
	id int GENERATED BY 
		DEFAULT AS 
		IDENTITY primary key,
	nome varchar2(20) not null,
	nacionalidade varchar(20) default 'brasileira'
);
```
## Cláusula Where
> É utilizada sempre que se desejar estabelecer uma condição de pesquisa. É sempre seguida dos seguintes operadores:

- De comparação -> >, <, =, >=, <=, <>
- Lógicos -> 
	- AND, 
	- OR, 
	- NOT
- Da linguagem SQL -> 
	- IS NULL, 
	- IS NOT NULL, 
	- LIKE, 
	- NOT LIKE, 
	- IN, 
	- NOT IN, 
	- BETWEEN, 
	- NOT BETWEEN, 
	- EXISTS, 
	- NOT EXISTS
## Operações SQL:

### IS NULL
- Verifica se o conteúdo da coluna é NULL (vazio)
- IS NOT NULL Negação do operador IS NULL
```sql
SELECT * FROM PROJETO WHERE VALOR_PROJ IS NULL;
```

### LIKE
> Compara cadeia de caracteres utilizando padrões de comparação

- % substitui zero, um ou mais caracteres
- _ substitui um caractere
- LIKE 'A%' inicia com a **letra A**
- LIKE '%A' termina com a  **Letra A**
- LIKE '%A%' tem a letra A em **qualquer posição**
- LIKE 'A_' string de dois caracteres, inicia com a **letra A**
- LIKE '_ A' string de dois caracteres, termina com a **Letra A**
- LIKE '_ A _ ' string de três caracteres, **letra A** na segunda posição
- LIKE '%A_' tem a letra A na penúltima posição
- LIKE '_ A%' tem a letra A na segunda posição 
- NOT LIKE Negação do operador LIKE

### IN
> Testa se um valor pertence a um conjunto de valores
> NOT IN Negação do operador IN
### BETWEEN 
> Determina um intervalo de busca:
> `{sql} BETWEEN 'valor1' AND 'valor2'`
> `NOT BETWEEN` -> Negação do operador `BETWEEN`
### EXISTS
> Verifica se um valor existe em um conjunto, levando em conta os valores
> Nulos não são considerados pelo operador IN
> `NOT EXISTS`-> Negação do operador `EXISTS`.
