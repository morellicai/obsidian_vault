# Construindo um calendário com PHP - CAP 3

> Neste capitulo construirei um calendário completo.

## 3.1 Definindo nosso calendário
- Usaremos tables do HTML montadas pelo PHP
- No final é esperado algo como:

| Dom | Seg | Ter | Qua | Qui | Sex | Sáb |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: |
|  1  |  2  |  3  |  4  |  5  |  6  |  7  |
|  8  |  9  | 10  | 11  | 12  | 13  | 14  |
| 15  | 16  | 17  | 18  | 19  | 20  | 21  |
| 22  | 23  | 24  | 25  | 26  | 27  | 28  |
| 29  | 30  | 31  |     |     |     |     |
## 3.2 Começando o calendário
- Já começamos introduzindo um código HTML para ter o cabeçalho do nosso calendário.
	- O que é mais destacado aqui pra mim, é que estamos escrevendo html direto num arquivo `.php` e ele já renderiza, sem muita dificuldade, sem precisar de muita regra de linguagem. Apenas o HTML.
###### O código:
```php
<h1><?php echo "Calendário em PHP"; ?></h1>
<table border="1">
	<tr>
		<th>Dom</th>
		<th>Seg</th>
		<th>Ter</th>
		<th>Qua</th>
		<th>Qui</th>
		<th>Sex</th>
		<th>Sáb</th>
	</tr>
</table>
```
> Isso é um poder exclusivo do arquivo `.php`. Não conseguimos fazer isso em um arquivo `.html` que não funcionará da mesma forma.

## 3.3 Usando funções
- Aqui é a primeira vez que trabalhamos com variáveis
	- Posso notar que cada variável deve começar com um cifrão ($) Na frente do nome de cada variável
	- Nomes de variáveis:

| Pode      | Não Pode |
| --------- | -------- |
| $dia      | $-nome   |
| $nome     | $1       |
| $semana   | $!nome   |
| $\_pessoa | $4nome   |
- Também usei um array, e ele é um pouco diferende de sintaxes como de C. A sintaxe dele, em vez de "\[]" ele usa "()" como se fosse uma função (O que provavelmente, em php seja uma função. Lembrar de revisar isso depois)
- Usei um while, e ele funciona exatamente como em qualquer linguagem. Abertura e fechamento de chaves para podermos delimitar a sua atuação.
- Assim como o if.
- Temos também uma chamada de função `count()` 
	- O que deve ser uma função nativa da linguagem para que possamos contabilizar algo iterável.   
> Abaixo o código desenvolvido até aqui:
```php
<?php
function linha($semana){
	echo"
		<tr>
			<td>{$semana[0]}/td>
			<td>{$semana[1]}/td>
			<td>{$semana[2]}/td>
			<td>{$semana[3]}/td>
			<td>{$semana[4]}/td>
			<td>{$semana[5]}/td>
			<td>{$semana[6]}/td>
		</tr>
	";
}; 

function calendario(){
	$dia = 1;
	$semana = array();
	while($dia <= 31){
		array_push($semana, $dia);
		if(count($semana) == 7){
			linha($semana);
			$semana = array();
		}
		$dia++;
	}
}
?>
<h1><?php echo "Calendário em PHP"; ?></h1>
<table border="1">
	<tr>
		<th>Dom</th>
		<th>Seg</th>
		<th>Ter</th>
		<th>Qua</th>
		<th>Qui</th>
		<th>Sex</th>
		<th>Sáb</th>
	</tr>
<?php
	calendario();
?>
</table>
```

### Observação da lógica

- A função linha é responsável por receber a variável `$semana`, que é um array que é iterado no while na função calendário
- A função calendário, ela está sendo a responsável pela logica robusta até aqui. 
	- Aqui criamos uma variável, que será os dias iterados até 31, que é a condição de parada do while da função.
	- A cada iteração, é feito um push no array (Ato de adicionar valor no final do array)
		- O que é interessante é que o array está me parecendo uma função. Para o push, eu preciso passar 2 parâmetros: 
		- 1º parâmetro é o array que quero dar push
		- 2º parâmetro é a variável que quero inserir no array
- O calendário só chegou até o dia 28 por um erro de lógica proposto no livro. Pois colocamos um if que, se o `count($semana) != 7` ele não entrá no if, e não faz as adições.
	- O que da pra entender com isso é que o while fica acumulando até que se passe 7 dias, passou os 7 dias, ele faz a chamada da função linha
	- O que estará errado, pois tendo 31 dias, é impossível que todos os meses sejam idênticos. O que eu pensando aqui, poderia fazer é incrementar a lógica e continuar criando até 12 meses. mas vamos ver até onde o livro vai para resolver. Até por que, a ideia é criar um calendário de algum determinado mês, e não do ano todo
## 3.4 Entendendo e se entendendo com os erros
- A solução é chamar a função linha depois que terminar o while, passando o array com menos dias. O código ficará assim:

```php
<?php
function linha($semana){
	echo"
		<tr>
			<td>{$semana[0]}/td>
			<td>{$semana[1]}/td>
			<td>{$semana[2]}/td>
			<td>{$semana[3]}/td>
			<td>{$semana[4]}/td>
			<td>{$semana[5]}/td>
			<td>{$semana[6]}/td>
		</tr>
	";
}; 

function calendario(){
	$dia = 1;
	$semana = array();
	while($dia <= 31){
		array_push($semana, $dia);
		if(count($semana) == 7){
			linha($semana);
			$semana = array();
		}
		$dia++;
	}
	linha($semana$);
}
?>
<h1><?php echo "Calendário em PHP"; ?></h1>
<table border="1">
	<tr>
		<th>Dom</th>
		<th>Seg</th>
		<th>Ter</th>
		<th>Qua</th>
		<th>Qui</th>
		<th>Sex</th>
		<th>Sáb</th>
	</tr>
<?php
	calendario();
?>
</table>
```
- Com isso vieram alguns erros, pois não é acessado os outros dias da semana.
- O erro é o `Undefined offset: 3` Isso quer dizer que está tentando acessar o incide 3 no array `$semana` e não está encontrando.
## 3.5 Meu PHP não mostrou os erros!
- Para que esses erros fiquem aparente, é preciso configurar o php para que ele mostre os erros no navegador, já que não estamos rodando no terminal.
	- Para essa configuração, editamos o php.ini
	- variavel que é necessário mudar é a `display_errors` que estará como off. precisa mudar para On, para visualizarmos os erros
## 3.6 Finalizando o Calendário
- Para corrigirmos o bug, precisamos utilizar um laço for, para testar se o índice do array está sendo acessado ou não
- A função fica assim agora:
```php
function linha($semana){
	echo"<tr>";
	for($i = 0; &i <= 6; $i++){
		if(isset($semana[$i])){ # Vê se a variável ou array foi iniciado
			echo"<td>{$semana[$i]}</td>";
		} else {
			echo"<td></td>";
		}
	}
	echo"</tr>";
}
```
> Executando novamente, os erros sumiram

- Foi usado a função do php `isset()` que verifica se uma variável existe ou se um índice em um array foi definido. 
## Desafio do capitulo

- Faça uma página que exiba a hora e a frase "Bom dia", "Boa tarde" ou "Boa noite", de acordo com a hora. Use a conficional **if** e a função `{php} date()` 
	- R: Criei uma função que pega a hora atual, e compara para ver se é de manha e declara bom dia se for. Para exibir a hora, peguei a hora atual com a formatação de hora e minuto e imprimi
```php
function cumprimento(){
	$hora = date("H");
	if($hora < 12){
		echo "Bom dia";
	}else if($hora >= 12 && $hora < 19){
		echo "Boa tarde";
	}else{
		echo "Boa noite";
	}
}
?>

<h1><?php echo "Calendário em PHP"; ?></h1>
<h3><?php cumprimento() ?></h3>
<p>
	<?php
		$horaAtual = date('h:i A');
		
		echo "Agora são $horaAtual";
	?>
</p>

```
- Faça com que o calendário exiba o dia atual em negrito, usando a função `{php} date()`
- Exiba os domingos em vermelho e os sábados em negrito.
	- R: 
- Faça o calendário começar em um dia que não seja um domingo.
	- R: Antes do while começar, adicionei um for que itera em quantos dias da semana não terão dia, enviando um null para o array `$semana` 
```php
function calendario(){
	$dia = 1;
	$semana = array();
	global $diaAtual;
	for($i = 0; $i < 3; $i++){
		array_push($semana, null);
	}

	while($dia <= 31){
    array_push($semana, $dia);
    if(count($semana) == 7){
      linha($semana);
      $semana = array();
    }
    $dia++;
	}
  linha($semana);
}
```
