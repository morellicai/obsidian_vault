> Fazer o exemplo de encapsulamento do Veiculo dado em aula e criar um outro exemplo utilizando encapsulamento. Entregar os códigos `.java` e os teste de caixa preta.

## Exemplo da aula
```java
//class Carro
class Veiculo{
	public String nome;
	private float velocidade;

	public void setVelocidade(float velocidade){
		this.velocidade = velocidade;
	}
	public float getVelocidade(){
		return (velocidade);
	}

	public void acelera(){
		if(velocidade < 100){
			velocidade++;
		}
	}
	public void frea(){
		if(velocidade > 0){
			velocidade--;
		}
	}
}
```
```java
// Main archive
public class Main {
	public static void main(String[] args){
		Veiculo v1 = new Veiculo();
		v1.nome = "Gol";
		v1.setVelocidade(80);
		for(int i = 1; i <= 25; i++){
			v1.acelera();
		}
		System.out.println("Velocidade = " + v1.getVelocidade());
		v1.setVelocidade(10);
		for(int i = 1; i <= 25; i++){
			v1.frea();
		}
		System.out.println("Velocidade = " + v1.getVelocidade());
	}
}
```
### Saída
![[screenshot-2025-10-13_05-23-51.png]]

## Exemplo meu
```java
// class Pessoa
import java.lang.Math;
public class Pessoa {
	protected String nome;
	private int idade;
	private float altura;
	private float peso;

	public void setNome(String nome) {
		this.nome = nome;
	}

	public String getNome() {
		return nome;
	}

	public void setIdade(int idade) {
		this.idade = idade;
	}

	public int getIdade() {
		return idade;
	}

	public void setAltura(float altura) {
		this.altura = altura;
	}

	public float getAltura() {
		return altura;
	}

	public void setPeso(float peso) {
		this.peso = peso;
	}

	public float getPeso() {
		return peso;
	}

	public float imc(float peso, float altura){
		return (float) (peso / Math.pow(altura, 2));
	}
}
```
```java
// Classe que testa as variaveis e funções
public class testPessoa{
	public static void main(String[] args) {
		Pessoa p1 = new Pessoa();
		p1.setNome("Caio");
		p1.setIdade(24);
		p1.setAltura(1.82f);
		p1.setPeso(113.0f);

		String nome = p1.getNome();
		int idade = p1.getIdade();
		float altura = p1.getAltura();
		float peso = p1.getPeso();

		System.out.println("Olá " + nome + ", Vi que sua idade é " + idade);
		System.out.println("Vamos ver seu IMC?");
		System.out.println("Seu peso é " + peso + " e sua altura " + altura);

		float imcResult = p1.imc(peso, altura);

		System.out.println("Seu imc é " + imcResult);
		if(imcResult < 18.5){
			System.out.println("Você esta abaixo do peso ideal");
		} else if (imcResult > 30.0){
			System.out.println("Você esta acima do peso ideal");
		} else {
			System.out.println("Você esta em forma!");
		}
	}
}
```
### Saída
![[screenshot-2025-10-13_06-37-54.png]]