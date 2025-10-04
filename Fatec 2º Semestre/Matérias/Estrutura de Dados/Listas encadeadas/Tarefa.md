`listaEncadeada.h`
```c
#include <stdio.h>
#include <stdlib.h>

typedef int Item;
typedef struct no {
  Item item;
  struct no *prox;
} *Lista;

Lista no(Item x, Lista p) {
  Lista n = malloc(sizeof(struct no));
  n->item = x;
  n->prox = p;
  return n;
}

void exibe(Lista L) {
  printf("[");

  if (L == NULL) {
    printf("]");
  }

  while (L != NULL) {
    printf("%d", L->item);
    if (L->prox != NULL) {
      printf(",");
    }
    L = L->prox;
  }

  printf("]");
}
int tamanho(Lista L) {
  int t = 0;
  while (L) {
    t++;
    L = L->prox;
  }
  return t;
}
```

# Exercício 1
Completar e executar o programa exibido no material:
```c
#include "listaEncadeada.h"
// Fiz um arquivo para conter todo o arquivo de construção de listas
int main(void) {
  Lista I = no(3, no(1, no(5, NULL)));
  exibe(I);
  return 0;
}
```
Saída:
![[screenshot-2025-10-03_21-25-34.png]]
# Exercício 2
Alterar a função `{c} exibe()` para que a saída seja [3,1,5]
```c
#include "listaEncadeada.h"
#include <stdio.h>

void exibe2(Lista L) {
  printf("[");

  while (L != NULL) {
    printf("%d", L->item);
    if (L->prox != NULL) {
      printf(",");
    }
    L = L->prox;
  }

  printf("]");
}

int main(void) {
  Lista I = no(3, no(1, no(5, NULL)));
  exibe2(I);
  return 0;
}
```
Saída:
![[screenshot-2025-10-03_21-25-34 1.png]]
# Exercício 3
completar o programa a seguir
```c
#include "listaEncadeada.h"

int main(void) {
  Lista I = no(3, no(1, no(5, NULL)));
  exibe(I);
  printf("\nTamanho = %d\n", tamanho(I));
  return 0;
}
```
Saída!
![[screenshot-2025-10-03_21-43-04.png]]
# Exercício 4
Adicionar uma função que some os itens da lista
```c
#include "listaEncadeada.h"
#include <stdio.h>

int soma(Lista L) {
  int result = 0;

  while (L != NULL) {
    result = result + L->item;
    L = L->prox;
  }
  return result;
}

int main(void) {
  Lista I = no(3, no(1, no(5, NULL)));
  exibe(I);
  if (soma(I) == 0) {
    printf("lista vazia");
    return 0;
  }
  printf("\nResultado da soma dos itens da lista é: %d\n", soma(I));
}
```
Saída:
![[screenshot-2025-10-03_22-01-23.png]]