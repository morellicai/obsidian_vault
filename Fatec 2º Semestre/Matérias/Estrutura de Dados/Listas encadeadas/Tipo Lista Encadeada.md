# Construindo lista encadeada em C
- [[Listas encadeadas - Base | Voltar]]
## O tipo Lista
```c
typedef int Item;
typedef struct no {
  Item item;
  struct no *prox;
} *Lista;
```
##### Lógica
- O tipo `{c} Item` indica o tipo dos itens armazenados na lista
	- Se `{c} int` a lista só armazenará inteiros por exemplo
- O tipo `{c} Lista` é usado para declarar um ponteiro de lista 
	- Que aponta o primeiro nó
- Se **I** é um ponteiro de lista, então `{c} I->item` é o primeiro item da lista
- Se **I** é um ponteiro de lista, então `{c} I->prox` é o endereço do segundo nó da lista (resto)


## Criação de Nó
```c
Lista no(Item x, Lista p) {
  Lista n = malloc(sizeof(struct no));
  n->item = x;
  n->prox = p;
  return n;
}
```
## Criação de Lista
```c
// Essa chamada vai dentro do main da aplicação
Lista I = no(3, no(1, no(5, NULL)));
```
- A execução da chamada é da parte mais interna para mais externa. Então ele começa da ultima chamada para a primeira, mas a sequência fica na forma que é lida.
## Exibindo a lista
```c
void exibe(Lista L) {
  while (L != NULL) {
    printf("%d\n", L->item);
    L = L->prox;
  }
}
```
##### Lógica
- Uma função que contém um `{c} while` onde se a lista for `{c} NULL` é onde o loop acaba.
- Ele printa o item L em questão `{c} L->item`
- Pula para o proximo item do array `{c} L = L->prox;
> Note que, no final do percurso, o ponteiro inicial continua apontando o primeiro nó da lista