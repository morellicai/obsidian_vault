```c
#include "pilha.h"
#include <stdio.h>

int main(void) {
  int num;
  Pilha A = pilha(10);
  Pilha B = pilha(10);

  printf("Digite 10 numeros aleatorios:\n");
  for (int i = 0; i < 10; i++) {
    scanf("%d", &num);
    empilha(num, A);
  }
  printf("Vamos ordenar...\n");

  while (!vaziap(A)) {
    int item_de_A = desempilha(A);

    while (!vaziap(B) && topo(B) > item_de_A) {
      empilha(desempilha(B), A);
    }
    empilha(item_de_A, B);
  }
  while (!vaziap(B)) {
    empilha(desempilha(B), A);
  }

  printf("Pilha ordenada: ");
  while (!vaziap(A)) {
    printf("%d ", desempilha(A));
  }
  printf("\n");

  destroip(&A);
  destroip(&B);
  return 0;
}
```
### Saída
![[screenshot-2025-10-10_17-50-46.png]]

# Tarefa 2
```c
#include "pilha.h"
#include <stdio.h>
int main(void) {
  int num;
  Pilha A = pilha(10);
  Pilha B = pilha(10);
  printf("Digite 10 numeros aleatorios:\n");
  for (int i = 0; i < 10; i++) {
    if (scanf("%d", &num) != 1) {
      printf("Erro de leitura.\n");
      break;
    }
    empilha(num, A);
  }
  printf("Vamos ordenar inversamente e garantir a unicidade...\n");
  while (!vaziap(A)) {
    int item_de_A = desempilha(A);

    while (!vaziap(B) && topo(B) < item_de_A) {
      empilha(desempilha(B), A);
    }
    empilha(item_de_A, B);
  }
  printf("Pilha ordenada inversamente (decrescente) e sem repetidos: \n");
  while (!vaziap(B)) {
    int elemento_final = desempilha(B);
    empilha(elemento_final, A);
  }
  printf("\n");
  while (!vaziap(A)) {
    int eEquals = desempilha(A);
    if (!vaziap(A) && eEquals == topo(A)) {
      continue;
    }
    printf("%d ", eEquals);
  }
  destroip(&A);
  destroip(&B);
  return 0;
}
```
### Saída
![[screenshot-2025-10-10_17-53-06.png]]
# Tarefa 3
```c
#include "pilha.h"
#include <stdio.h>
#include <string.h>

int main(void) {
  char frase[256];
  printf("Digite uma frase \n");
  fgets(frase, sizeof(frase), stdin);
  frase[strcspn(frase, "\n")] = '\0';

  Pilha P = pilha(strlen(frase));

  for (int i = 0; frase[i] != '\0'; i++) {
    if (frase[i] != ' ') {
      empilha((void *)(long)frase[i], P);
    } else {
      while (!vaziap(P))
        printf("%c", (char)(long)desempilha(P));
      printf(" ");
    }
  }
  while (!vaziap(P))
    printf("%c", (char)(long)desempilha(P));

  printf("\n");
  destroip(&P);
  return 0;
}
```
### Saída
![[screenshot-2025-10-10_17-54-57.png]]
# Tarefa 5
```c
#include "pilha.h"
#include <stdio.h>

int main(void) {
  Pilha P = pilha(5);
  char s[11];

  for (int i = 1; i <= 3; i++) {
    printf("? ");
    fgets(s, 11, stdin);
    empilha(s, P);
  }

  while (!vaziap(P)) {
    puts(desempilha(P));
  }
  return 0;
}
```
### Saída
![[screenshot-2025-10-10_17-57-04.png]]
- Isso ocorre por que a pilha armazena o endereço de memória, e não a cadeia de caracteres em si, por isso, quando inserimos um dois três, em vez de retornar de forma invertida cada um, o retorno é o ultimo valor que o endereço de memoria armazena
# Tarefa 6
```c
#include "pilha.h"
#include <stdio.h>
#include <string.h>

int main(void) {
  Pilha P = pilha(5);
  char s[11];

  for (int i = 1; i <= 3; i++) {
    printf("? ");
    fgets(s, 11, stdin);
    empilha(strdup(s), P);
  }

  while (!vaziap(P)) {
    puts(desempilha(P));
  }
  return 0;
}
```
### Saída
![[screenshot-2025-10-10_17-57-57.png]]

Você é um estudante engajado com a matéria de estrutura de dados, e nesse momento, você irá pegar esse material que está anexado e fazer um resumo detalhado.
**SUA MISSÃO**: pegar o material anexado, e resumir ele como se fosse uma pessoa escrevendo pensando em que fique claro para a próxima vez que ler lembrar de todos os detalhes envolvidos no assunto abordado pelo material, sem repetir as palavras e melhorando as formas de falar para que fique mais claro e memorizável.