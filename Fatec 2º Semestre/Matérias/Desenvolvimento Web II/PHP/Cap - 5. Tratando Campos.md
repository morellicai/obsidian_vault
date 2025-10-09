---
tags:
  - PHP
  - Code
Titulo: Capitulo 5 Tratamento de diferentes campos de formulário
Data: 2025-10-09T08:00:00
---
> Antes de passar para a próxima etapa, é crucial que revisitemos o que já foi feito até aqui, para conseguir ter certeza se não precisamos melhorar algo de nosso código. Para que possamos facilitar as próximas etapas.

# 5.1 Modularizando os Códigos

- Vamos separar o código em 2. 
	- 1 fará a logica, processando as entradas e manipulando a sessão
	- o outro fará a exibição do formulário
### Tarefas.php

```php
<?php
session_start();

if (isset($_GET['nome'])){
	$_SESSION['lista_tarefas'][] = $_GET['nome'];
}

if(isset($_SESSION['lista_tarefas'])){
	$lista_tarefas = $_SESSION['lista_tarefas'];
} else {
	$lista_tarefas = array();
}

include "template.php";
?>
```
> Aqui temos um detalhe novo, que é o include. Ele quem chama os arquivos diferentes. E o interessante é que ele adiciona a possibilidade de todas as funções e variáveis criada no arquivo que chama, passa para o arquivo chamado, nesse caso o `template.php`.
> É como o `{python} import` do Python, que chama módulos ou arquivos inteiros como objeto. A diferença, é que em Python e em C, os `imports` são tratados apenas como instancia do código do outro arquivo. Ou seja, se eu quero usar o template como declarado no código acima em C ou Python, eu preciso também instanciar o que tem neles no arquivo que eu chamo.
> Para controlar o que é utilizado quando incluí um arquivo no php, precisamos declarar funções ou classes que necessitam ser instanciadas ou chamadas para rodar. Se não, assim que você inclui o arquivo, tudo que está nele roda.
> É necessário então ter atenção de onde é inserido o include, para ele não iniciar em um lugar que não é desejado!
### template.php
```php
<!DOCTYPE html>
<html lang="pt-BR">

<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<title>Gerenciador de Tarefas</title>
	<link href="style.css" rel="stylesheet" type="text/css">
</head>

<body>
	<h1>Gerenciador de Tarefas</h1>
	<form>
		<fieldset>
			<levend>Nova Tarefa</levend>
			<label>Tarefa:</label>
			<input type="text" name="nome" placeholder="Digite a Tarefa">
			<input type="submit" value="Cadastrar">
		</fieldset>
	</form>
	<table>
		<tr>
			<th>Tarefas</th>
		</tr>
		<?php foreach($lista_tarefas as $tarefas): ?>
		<tr>
			<td>
				<?php echo $tarefas; ?>
			</td>
		</tr>
		<?php endforeach; ?>
	</table>
</body>

</html>
```
> Agora temos apenas a lógica de apresentação em PHP aqui. Unica coisa de php que temos nesse código, é o loop de apresentação 

# 5.2 Adicionando mais informações às tarefas

- Vamos adicionar mais informações para descrever melhor as tarefas e poder organiza-las mais facilmente
- Adicionarei uma descrição também
- Prazo de conclusão
- Nível de propriedade
Pra isso vamos adicionar novos campos no arquivo `template.php`
```php
<!DOCTYPE html>
<html lang="pt-BR">

<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">
	<title>Gerenciador de Tarefas</title>
	<link href="style.css" rel="stylesheet" type="text/css">
</head>

<body>
	<h1>Gerenciador de Tarefas</h1>
	<form>
		<fieldset>
			<legend>Nova Tarefa</legend>
			<label>Tarefa:</label>
			<input type="text" name="nome" placeholder="">

			<label>Descrição (Opcional)</label>
			<textarea name="descrição"></textarea>

			<label>Prazo (Opcional)</label>
			<input type="text" name="prazo"></input>

			<fieldset>
				<legend>Prioridade:</legend>
				<label>
					<input type="radio" name="prioridade" value="baixa" checked>
					Baixa

					<input type="radio" name="prioridade" value="media" checked>
					Media

					<input type="radio" name="prioridade" value="alta" checked>
					Alta
				</label>
			</fieldset>
			<label>
				Tarefa concluida <input type="checkbox" name="concluida" value="sim">
				<input type="submit" value="Cadastrar">
			</label>
		</fieldset>
	</form>
	<table>
		<tr>
			<th>Tarefas</th>
		</tr>
		<?php foreach($lista_tarefas as $tarefas): ?>
		<tr>
			<td>
				<?php echo $tarefas; ?>
			</td>
		</tr>
		<?php endforeach; ?>
	</table>
</body>

</html>
```

- Agora alterar o `tarefas.php` para receber esses novos dados
```php
<?php
session_start();

if (isset($_GET['nome'] && $_GET['nome'] != '')){
	$tarefa = array();

	$tarefa['nome'] = $_GET['nome'];

	if(isset($_GET['descricao'])){
		$tarefa['descricao'] = $_GET['descricao'];
	}else{
		$tarefa['descricao'] = '';
	}

	if(isset($_GET['prazo'])){
		$tarefa['prazo'] = $_GET['prazo'];
	}else{
		$tarefa['prazo'] = '';
	}
	
	$tarefa['prioridade'] = $_GET['prioridade'];

	if(isset($_GET['concluida'])){
		$tarefa['concluida'] = $_GET['concluida'];
	}else{
		$tarefa['concluida'] = '';
	}

	$_SESSION['lista_tarefas'][] = $tarefa;
}

if(isset($_SESSION['lista_tarefas'])){
	$lista_tarefas = $_SESSION['lista_tarefas'];
} else {
	$lista_tarefas = array();
}

include "template.php";
?>
``` 
> Utiliza o `{php} isset()` pois o navegador não envia dado não inserido em branco. Então o php retorna um erro se não utilizamos essa função que valida se existe

Agora só alterar a tabela para que todos sejam exibidos. E alteramos isso no arquivo `template.php`
