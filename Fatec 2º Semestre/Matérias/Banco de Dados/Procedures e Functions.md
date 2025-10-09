---
Titulo: Apresentação de Stored Procedure e Function
Conteúdo Externo: https://www.tutorialspoint.com/sql/sql-stored-procedures.htm
tags:
  - Faculdade
  - Code
  - MySQL
  - BD
---
# Entendendo Stored Procedures e Functions (SPs e Functions)

> 	Primeiro, fixar que tanto as **Stored Procedures** quanto as **Functions** são **sub-programas** É um passo muito importante. O objetivo delas é executar uma **tarefa específica** e elas são ferramentas cruciais dentro de um SGBD, que busca fornecer um ambiente conveniente e eficiente para o gerenciamento e armazenamento de informações.
	Como outros blocos de código (por exemplo, em PL/SQL), elas podem receber **parâmetros** e têm uma área obrigatória para a lógica de execução, além de áreas opcionais para declarações e tratamento de exceções.
## Como Elas Funcionam e Onde São Armazenadas?

Elas não são executadas na hora; elas são **objetos compilados previamente**.

1. O **texto de origem** (o código-fonte que eu escrevo) e a **forma compilada** (**p-code**) são armazenados no dicionário de dados.
2. Quando eu chamo uma Procedure ou Function, o _p-code_ é lido do disco.
3. Uma vez lido, ele fica armazenado na **parte compartilhada do pool da SGA** (_System Global Area_), o que permite que vários usuários o acessem, otimizando a performance.

### A Diferença Fundamental: Retorno e Uso

A principal coisa que devo lembrar para diferenciar as duas é: o que elas devolvem e como eu as chamo.

|Característica|Stored Procedure|Function|
|:--|:--|:--|
|**Retorno de Valor**|**Não retornam valores**.|**Sempre retornam um valor**. O tipo de retorno é especificado, como `RETURN NUMBER`.|
|**Uso em SQL**|Não são usadas para atribuir valores a variáveis ou como argumento em um comando `SELECT`.|Podem ser invocadas por meio de um comando `SELECT` ou utilizadas em cálculos.|
|**Invocação**|Chamada pelo nome ou diretamente via comando `EXECUTE`, ou dentro de um bloco anônimo PL-SQL.|Podem ser chamadas em comandos DML (Data Manipulation Language).|
|**Parâmetros**|Podem ter parâmetros de **entrada (IN)** e **saída (OUT)**.|Normalmente só possuem parâmetro de **entrada (IN)**.|
|**Interoperabilidade**|Pode chamar uma Function.|**Não pode** invocar uma Stored Procedure.|

### Modos de Parâmetros em Stored Procedures

Este é um detalhe crucial: as Procedures (especialmente no PL/SQL) me permitem usar três modos de parâmetros.

|Modo|Objetivo|Efeito no Valor Inicial|
|:--|:--|:--|
|**IN** (Entrada)|Recebe o valor de fora. É o modo padrão (_default_).|O valor recebido **não pode ser modificado** dentro da procedure. Os valores são usados exatamente como foram enviados.|
|**OUT** (Saída)|Devolve um valor para o programa chamador.|A variável é inicializada como `NULL` dentro do sub-programa. Se a variável externa tinha um valor, ele **não faz nenhum efeito** no cálculo.|
|**IN OUT** (Entrada/Saída)|Junta IN com OUT. Recebe um valor inicial e devolve um valor modificado.|O valor inicial da variável externa **fará efeito** no cálculo, pois este modo tanto recebe quanto envia.|

### A Estrutura Básica

Eu preciso memorizar a estrutura básica (usando PL/SQL como exemplo):

**Stored Procedure**:

```sql
CREATE [OR REPLACE] PROCEDURE proc_name [lista de parâmetros] IS
 Declarações
BEGIN
 Lógica de Execução (obrigatória)
EXCEPTION
 Tratamento de Exceção (opcional)
END;
/
```

**Function**:

```sql
CREATE [OR REPLACE] FUNCTION function_name [(parâmetros)]
 RETURN tipo_de_retorno  -- Isso aqui é obrigatório!
 {IS | AS}
BEGIN
 Lógica (body)
END [function_name];
/
```

### Gerenciamento e Comandos DDL

Para manipular esses objetos compilados, eu uso comandos DDL (_Data Definition Language_). Para criar procedures, meu _schema_ precisa ter o privilégio `CREATE ANY PROCEDURE`, que é concedido pelo administrador.

Eu posso usar os seguintes comandos para controle:

- **Para ver o status ou listar:** Eu consulto as tabelas `user_objects` usando `object_type='PROCEDURE'` ou `object_type='FUNCTION'`.
- **Para ver o código-fonte (o texto):** Eu uso `select text from user_source where name= 'nome'`.
- **Para remover:** Uso `drop procedure nome_procedure/function`.
- **Para ver erros de compilação:** Uso `SHOW ERRORS NOME_PROCEDURE`.
- **Para dar permissão de uso:** Uso `GRANT EXECUTE ON b.procedure_name TO a`.

### Entendendo a Importância Prática

O exemplo do MySQL de "Vendas e Atualização de Estoque" me mostra exatamente por que eu usaria uma Stored Procedure.

A `atualizarEstoque` encapsula a **lógica de negócios** dentro do SGBD. Ela verifica o estoque atual e, se houver o suficiente (`IF varEstoqueAtual >= varQuantidadeVendida THEN`), ela executa as operações necessárias (`UPDATE` no estoque e `INSERT` na tabela `vendas`). Caso contrário, ela retorna uma mensagem de erro ("Estoque insuficiente").

Isso é fundamental porque garante a **integridade dos dados**. Essa _procedure_ garante que todas as etapas da transação (verificar, atualizar e registrar) sejam realizadas em conjunto, protegendo contra falhas, um conceito central do SGBD que deve garantir a acuracidade e recuperação das informações.