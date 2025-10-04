- [[0. Estrutura de Dados - Base | Base]]
#### Busca linear
não precisa de ordenação
#### Busca binária
reconhecida como uma busca log(n), mas precisa estar ordenado

# Ordenação
> É a operação que **reorganiza** os itens de um vetor par que eles fiquem em ordem **crescente**
> Dado um vetor v[n], sendo n >= 1, a **

## Algoritmo de Troca
> É a operação que troca os valores de duas posições quaisquer de um vetor.

### Estratégia:
- Copie o valor da posição _i_ para _x_
- Armazene na posição _i_ o valor da posição _j_
- Armazene na posição _j_ o valor de _x_ 
```c
void troca(int v[], int i, int j){{
	int x = v[i];
	v[i] = v[j];
	v[j] = x;
}
```
## Ordenação por trocas (*bubble sort*)
> É um algoritmo de ordenação cuja operação básica é a **troca**.
### Estratégia:
Para ordenar um vetor v[n], usando ordenação por trocas:
- Encontre em *v* um par de itens consecutivos $v_i$ e $v_{j+i}$ tal que $v_{j}> v_{j+i}$
- Troque esses itens de posição, de modo que cada um passe a ocupar a posição do outro.
- Repita o procedimento enquanto for possível
- O mais importante de entender, é que sempre vamos estar trocando as posições até que seja ordenado;

```c
void bsort(int v[], int n){
	for(int i = 1; i < n; i++){
		for(int j = 0; j < n - i; j++){
			if(v[j] > v[j+1]){
				troca(v, j, j + 1);
			}
		}
	}
}
```
- Bubble sort é um algoritmo de $n^2$, não é um algoritmo rápido
- Quando olhamos para a qualidade do algoritmo, olhamos para a velocidade que ele faz a ordenação. Se a quantidade de comparação para a ordenação acontecer, é maior do que o tamanho do array, ele é considerado $n^2$ 
# Intercalação (merge)
> É a operação que **Combina** duas sequências ordenadas numa única sequência ordenada
## Estratégia
- Enquanto nenhuma sequência estiver vazia:
	- Compare o 1º item de uma ao 1º item da outra
	- Copie o menor deles para a sequência final
- Copie os itens restantes para a sequência vinal
> A operação é consome tempo proporcional a *n*. Por que ele passa por todos os itens do array
```c 
void intercala(int v[], int p, int m, int u) {
  int *w = malloc((u - p + 1) * sizeof(int));
  int i = p, j = m + 1, k = 0;
  while (i <= m && j <= u) {
    w[k++] = v[i] , v[j]) ? v[i++] : v[j++];
  }
  while (i <= m)
    w[k++] = v[i++];
  while (j <= u)
    w[k++] = v[j++];
  for (k = 0; k <= u - p; k++) {
    v[p + k] = w[k];
  }
}
```

# Merge sort
> É um algoritmo de ordenação cuja operação básica é a **intercalação**.

- Esse algoritmo é um divide para conquistar
- É considerado um algoritmo $n\ log\ n$
- Um algoritmo mais rápido
- É necessário ser uma função recursiva
- wrapper é facilitar a entrada par o programador. para que ele passe 2 parametros e não precise pedir 3 parametros
## Exemplo

# Busca
> É a operação que verifica se um item **Pertence** a um vetor
- É o algoritmo que vamos usar para buscar o dado
- Se o vetor estiver ordenado, a busca será log n 
- Não é um algoritmo que se preocupa com a ordenação do vetor
# Busca binária
> Supõe que o vetor onde é feita a busca está **ordenada**
- A ideia é buscar a partir do meio e ir retirando blocos que com certeza não vai estar
- Ele faz comparação com:
	- Se o numero que eu estou procurando é maior que o item do meio, descarta todo o bloco da esquerda, e busca um novo meio com apenas metade do vetor
- 