> Fazer o exemplo de Overload de área dado em aula. Entregar o testes de caixa preta e o código `.java`

### Código
```java
public class exemplo0506{
	public static void main(String[] args) {
		System.out.println("A área de um quadrado..." + area(3));
		System.out.println("A área de um retângulo.." + area(3, 2));
		System.out.println("A área de um cubo......." + area(3, 2, 5));
	}

	public static double area(int x){
		return(x * x);
	}
	public static double area(int x, int y) {
		return(x * y);
	}
	public static double area(int x, int y, int z){
		return(x * y * z);
	}
}
```
### Saída
![[screenshot-2025-10-11_18-13-44.png]]