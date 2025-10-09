# Entrada de dados com formulário - Cap 4

> Neste capitulo, o livro me levará a criar uma lista de tarefas

## 4.2 Formulário
Para a criação deste projeto, apenas criei um diretório na raiz `php` e vou adicionar meus arquivos, da mesma forma que no calendário. A rota está assim: "`http://localhost/tarefas/tarefas.php`"
- O código html do formulário:
```php
<html>
<head>
	<title>Gerenciador de Tarefas</title>
</head>
<body>
	<h1>Gerenciador de Tarefas</h1>
	<form>
		<fieldset>
			<legend>Nova Tarefa</legend>
			<label>Tarefa:</label>
			<input type="text" name="nome"/>
			<input type="submit" value="Cadastrar"/>
		</fieldset>
 </form>
```
## 4.3 Entrada de Dados
Quando apertamos em "Cadastrar" O html passa para a URL as informações passadas no nome da tarefa. Deixando o URL assim: 
"`http://localhost/tarefas/tarefas.php?nome=Estudar+PHP`"
Com isso, já podemos pegar da url a informação e construir algo. 

Para pegar da url esse nome, é fácil. Como php nasceu pra web, ele ja vem com alguns kits de para fazer coisas essenciais da web, facilitando nossa vida.
Temos algumas variáveis chamadas de **Super Globais**.
- Variáveis disponíveis em qualquer código php
Neste caso, temos a super global **`$_GET`**
- o Proprio php pega a url e passa as informações depois do '?' para essa variavel que é um array
- Podemos deixar o código assim:
```php
<html>
<head>
	<title>Gerenciador de Tarefas</title>
</head>
<body>
	<h1>Gerenciador de Tarefas</h1>
	<form>
		<fieldset>
			<legend>Nova Tarefa</legend>
			<label>Tarefa:</label>
			<input type="text" name="nome"/>
			<input type="submit" value="Cadastrar"/>
		</fieldset>
 </form>

<?php
    if (isset($_GET['nome'])) { // Verifica se indice 'nome' existe
        echo "Nome informado: " . $_GET['nome'];
    }
?>
</body>
</html>
```

Agora que sei como pegar as informações da url, posso construir um array que recebe e guarda as informações cadastradas. A modificação ficou assim:
```php
<?php
$lista_tarefas = array();
if (isset($_GET['nome'])){
	$lista_tarefas[] = $_GET['nome'];
}
?>
```
- Criamos um array chamado `$lista_tarefas`
- Verifica se existe o indice 'nome' dentro de `$_GET`
- Se existe, criamos um indice usando a sintaxe de lista vazia
	- Diferente na utilizada no calendário. Que se usassemos da mesma forma, seria assim `array_push($lista_tarefas, $_GET)` 

Para listarmos a lista de tarefas agora, podemos usar um loop. 
```php
<table>
	<tr>
		<th>Tafefas</th>
	</tr>
</table>
<?php foreach($lista_tarefas as $tarefas) : ?>
	<tr>
		<td><?php echo $tarefas; ?></td>
	</tr>
<?php endforeach; ?>
```
- Está sendo usado agora um novo loop que é feito para iterar encima de um array
- O `foreach` facilita a escrita para iterar um código. 
- Também não utilizamos as chaves '{}', podemos utilizar ':' e finalizar o loop com '`{php} endforach`'. Deixando mais legível o código
- É possivel utilizar a mesma lógica em todos os blocos de loop ou condicional `if e endif`, `while e endwhile` e `for e endfor`
> Preferível usar essa sintaxe apenas quando for acrescentar lógica no meio do html. Se o bloco ja for majoritariamente php, ai usa o bloco comum com abertura e fechamento de colchetes '{}'
## 4.5 Sessões no PHP

Cada requisição feita no navegador, o php reenvia a pagina HTML. Então se atualizarmos a pagina, ou se enviarmos um novo cadastro de tarefa, o PHP não guarda a informação passada antes. Ai entra as sessões.
As sessões são quem vai nos ajudar a manter as variáveis. Para usar sessão, no php utilizamos uma outra super global chamada `{php} $_SESSION` 
- A diferença dela para o `{php} $_GET` é que usaremos tanto para ler, quanto para escrever informações.
Vamos alterar o código para atribuir o session:
```php
<?php session_start();?> // Inicia a session
<html>
<head>
	<title>Gerenciador de Tarefas</title>
</head>
<body>
	<h1>Gerenciador de Tarefas</h1>
	<form>
		<fieldset>
			<legend>Nova Tarefa</legend>
			<label>Tarefa:</label>
			<input type="text" name="nome"/>
			<input type="submit" value="Cadastrar"/>
		</fieldset>
 </form>

<?php
if (isset($_GET['nome'])){
	// Passa o array para dentro da session
	$_SESSION['$lista_tarefas'][] = $_GET['nome']; 
}

$lista_tarefas = array(); // cria o array com o mesmo nome citado na session

if(isset($_SESSION['lista_tarefas'])){
	// Se a session existir, atribui o que tem listado na session, no array
	$lista_tarefas = $_SESSION['lista_tarefas'];
}
?>
	<table>
		<tr>
			<th>Tafefas</th>
		</tr>
	</table>
<?php foreach($lista_tarefas as $tarefas) : ?>
	<tr>
		<td><?php echo $tarefas; ?></td>
	</tr>
<?php endforeach; ?>
</body>
</html>
```
### Como funcionam as Sessões?

- Para o php saber qual é o usuário dono da sessão, ele guarda algumas informações nos `coockies` chamado **PHPSESSID**. Ele guarda um ID do usuário que está acessando a determinada session
- Também podemos usar os Cookies para guardar informações que serão mantidas nas requisições. 
	- Para isso usamos o `{php} $_COOKIE` uma super global array, assim como as outras que usamos até agora
## Desafios
1. Construir uma lista de contatos que devem ser cadastrados o nome, telefone e o e-mail.
```php
<?php session_start();?>
<html>

<head>
	<title>Gerenciador de Tarefas</title>
	<link href="style.css" rel="stylesheet">
</head>

<body>
	<h1>Gerenciador de Tarefas</h1>
	<form>
		<fieldset>
			<legend>Novo Contato</legend>
			<label>Contato</label>
			<div class="inputs">
				<input type="text" name="nome" placeholder="Nome" />
				<input type="tel" name="telefone" placeholder="Telefone" />
				<input type="email" name="email" placeholder="E-mail" />
			</div>
			<input type="submit" value="Cadastrar" />
		</fieldset>
	</form>

<?php
if (isset($_GET['nome'], $_GET['telefone'], $_GET['email'])){
	$_SESSION['lista_tarefas'][] = $_GET['nome'];
	$_SESSION['lista_tarefas'][] = $_GET['telefone'];
	$_SESSION['lista_tarefas'][] = $_GET['email'];
}

$lista_tarefas = array();

if(isset($_SESSION['lista_tarefas'])){
	$lista_tarefas = $_SESSION['lista_tarefas'];
}
?>
	<table>
		<tr>
			<th>Tafefas</th>
		</tr>
<?php foreach($lista_tarefas as $tarefas) : ?>
	<tr>
		<td><?php echo $tarefas; ?> <br></td>
	</tr>
<?php endforeach; ?>
	</table>
</body>
</html>
```
