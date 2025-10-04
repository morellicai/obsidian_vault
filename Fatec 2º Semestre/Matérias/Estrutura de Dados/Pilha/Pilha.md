- [[0. Estrutura de Dados - Base | Base]]
> É uma lista em que todas as operações de inserção, remoção e acesso são feitas num mesmo extremo, denominado de **topo**

### Funcionamento
- Quando um item é inserido numa pilha, ele é colocado em seu topo.
- Apenas o item no ropo da pilha pode ser acessado ou removido
- Essa política de acesso é denominada **LIFO** (Last-In/First-Out).
#### Exemplos de aplicação
- Controle de acesso às páginas visitadas num navegador web
- Controle de chamadas e retornos das funções num programa.
---
> Pilha é útil em qualquer situação em que precisamos **inverter** a ordem de uma sequência
---
## Operações em pilhas
**pilha(m)**
- Cria e devolve uma pilha vazia **P**, com tamanho **m**.
**vaziap(P)
- Devolve verdade se, e só se, a pilha P estiver vazia.
**cheiap(P)
- Devolve verdade se, e só se, a pilha P estiver cheia
**empilha(x,P)**
- Insere o item **x** no topo da pilha P
**desempilha(P)**
- Remove e devolve o item que estiver no topo de P.
**topo(p)**
- Acessa e devolve o item que estiver no topo de P.
**destroip(&p)**
- Destrói a pilha P
#### Exemplo:
```c
#include <stdio.h>
#include "pilha.h"

int main(void){
	int n;
	Pilha P = pilha(8*sizeof(int))
	printf("Decimal? ");
	scanf("%d", &n);
	do {
		empilha(n % 2, P);
		n /= 2;
	} while(n > 0);
	printf("Binario: ");
	while(!vaziap(P)){
		printf("%d", desempilha(P));
	}
	destroip(&P);
	return 0;
}
```

```c
// Inversão de cadeia
#include "pilha.h"
#include <stdio.h>

int main(void) {
  char c[513];
  Pilha P = pilha(513);
  printf("Cadeia? ");
  scanf("%512s", c);
  for (int i = 0; c[i]; i++) {
    empilha(c[i], P);
  }
  printf("Inverso: ");
  while (!vaziap(P)) {
    printf("%c", desempilha(P));
  }
  printf("\n");
  destroip(&P);
  return 0;
}
```

# Como o tipo *Pilha* e suas operações são definidos no arquivo `pilha.h`
- `typedef int Itemp;`: Define um tipo `Itemp` como um `int`. Isso é útil para flexibilidade, pois permite que o tipo de dado armazenado na pilha seja facilmente alterado (por exemplo, para `float` ou `char`) apenas mudando esta linha.     
- `typedef struct pilha { ... } *Pilha;`: Define a estrutura `pilha` e, ao mesmo tempo, cria um `typedef` para um ponteiro para essa estrutura, chamado `Pilha`. Isso simplifica a sintaxe, permitindo que você declare uma pilha como `Pilha P;` em vez de `struct pilha *P;`.
- **`pilha(int m)`**:
    - Esta função constrói e inicializa a pilha.
    - `Pilha P = malloc(sizeof(struct pilha));`: Aloca memória para a estrutura da pilha em si.        
    - `P->max = m;`: Armazena o tamanho máximo da pilha.
    - `P->topo = -1;`: O `topo` é um índice que aponta para o último item da pilha. O valor `-1` significa que a pilha está vazia.
    - `P->item = malloc(m * sizeof(Itemp));`: Aloca memória para os itens que serão armazenados na pilha. A quantidade de memória é `m` vezes o tamanho de um `Itemp` (`int`).
    - A função retorna o ponteiro `P` para a pilha recém-criada.
- **`vaziap(Pilha P)` e `cheiap(Pilha P)`**:
    - `vaziap`: Retorna `1` (verdadeiro) se a pilha estiver vazia (`topo == -1`), e `0` (falso) caso contrário.
    - `cheiap`: Retorna `1` se a pilha estiver cheia (`topo == max - 1`), e `0` caso contrário. A lógica `max - 1` é usada porque o índice do array começa em `0`.
- **`empilha(Itemp x, Pilha P)`**:
    - Coloca um item `x` no topo da pilha.
    - Primeiro, verifica se a pilha está cheia. Se estiver, imprime uma mensagem e encerra o programa com `abort()`.
    - Se houver espaço, incrementa o `topo` e armazena o item `x` na nova posição do topo.
- **`desempilha(Pilha P)`**:
    - Remove e retorna o item que está no topo da pilha.
    - Primeiro, verifica se a pilha está vazia e, se estiver, encerra o programa.
    - Se não estiver vazia, armazena o item do topo em uma variável temporária `x`, decrementa o `topo` para "remover" o item, e então retorna `x`.
- **`topo(Pilha P)`**:
    - Retorna o item no topo da pilha sem removê-lo.
    - Similar a `desempilha`, ele verifica se a pilha está vazia. Se não estiver, retorna o item na posição do `topo`.
- **`destroip(Pilha *Q)`**:
    - Libera a memória alocada para a pilha, evitando "vazamentos de memória".
    - `free((*Q)->item);`: Libera a memória alocada para o array de itens.
    - `free(*Q);`: Libera a memória alocada para a estrutura da pilha.
    - `*Q = NULL;`: Atribui `NULL` ao ponteiro da pilha, o que é uma boa prática para garantir que o ponteiro não aponte para uma memória que já foi liberada. O ponteiro `Q` é passado por referência (como `Pilha *Q`) para que a função possa modificar o ponteiro original `P` na função `main` que a chamou.