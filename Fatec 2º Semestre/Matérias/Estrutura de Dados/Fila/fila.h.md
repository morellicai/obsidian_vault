# Sobre o arquivo `fila.h`
> É uma implementação de **fila (queue)** usando **vetor circular** (“ring buffer”) alocado dinamicamente. Em vez de mover elementos quando enfileira/desenfileira, ele mantém dois índices (`inicio` e `final`) e um contador (`total`). Ao chegar no fim do vetor, os índices “dão a volta” para o começo usando aritmética modular.
### Includes
`<stdlib.h>` é um **cabeçalho da biblioteca padrão de C** que declara funções e macros de utilidade geral, incluindo:
- **Gerência de memória**: `malloc`, `calloc`, `realloc`, `free`.
- **Controle de processo/terminação**: `exit`, `abort`, macros `EXIT_SUCCESS` e `EXIT_FAILURE`.
- **Conversões numéricas**: `atoi`, `strtol`, etc.
- **Utilidades diversas**: `qsort`, `bsearch`, `abs`, `rand`/`srand`.
- **Constantes**: `NULL`, `size_t`, entre outras (algumas via outros headers).
No código, dele vêm **`malloc`**, **`free`**, **`abort`** e **`NULL`**.
### Vetor circular
Para entender bem o vetor circular, preciso entender exatamente como a fila nessa estrutura funciona. 
- **Inicio** -> Esse aponta para o indice de saída (inicio da fila, quem sai primeiro)
- **Final** -> Esse aponta para o indice de entrada (Final da fila, quem chega depois)
Entendendo isso, da para conseguir compreender bem o que acontece nesse tipo de file que conta com uma simulação de vetor circular
Por que ao invés de retirar um item no indice inicio, e andar toda fila, eu apenas "movo o array". 
Como isso funciona?
- tenho uma fila de 5 itens vazios. A cada item que eu coloco, o inicio permanece em indice 0, e final vai acompanhando os indices.
- Então, quando temos uma fila cheia, o final deve apontar para o indice 4, e o inicio para o indice 0.
- Retirando um item da fila, que será o item de indice Inicio, Eu ando o indice inicio de indice 0 para indice 1. 
- Com isso, tenho meu indice final apontando para o indice 4, e inidice inicio pontando para indice 1
- Me deixando livre para sobrescrever o que esta em indice. O que faz com que final aponte para 0, pois é com ele que entendemos onde podemos inserir um dado novo
### Typedof
`typedef` cria um **apelido de tipo**.
## Em geral
- `typedef int inteiro;` → agora `inteiro` é sinônimo de `int`.
- `typedef struct X* PX;` → `PX` é **ponteiro para** `struct X`.
## No seu código
1. `typedef int Itemf;`
    - Só cria um nome semântico para o tipo dos elementos da fila. Se você depois quiser trocar para `typedef float Itemf;` ou para um `struct`, o resto do código não muda.
2. 
   ```c
   typedef struct fila {
	   int   max;     // capacidade do vetor
	   int   total;   // nº de elementos atualmente na fila
	   int   inicio;  // índice do primeiro elemento
	   int   final;   // índice da próxima posição livre para inserir
	   Itemf *item;   // vetor de itens
	} *Fila
	``` 
- Define uma **struct anônima** com tag `fila` e, **ao mesmo tempo**, cria um typedef **para ponteiro** dessa struct:
    - `Fila` passa a significar **`struct fila*`**.
- Então quando você escreve `Fila F;`, isso é **um ponteiro**.  
    Por isso você acessa campos com **`->`** (ver mais abaixo).
### Função Fila
```c
Fila fila(int m) {
   Fila F = malloc(sizeof(struct fila));
   F->max    = m;
   F->total  = 0;
   F->inicio = 0;
   F->final  = 0;
   F->item   = malloc(m*sizeof(Itemf));
   return F;
}
```
Passo a passo:
1. **Aloca a estrutura**:
    - `malloc(sizeof(struct fila))` reserva memória para os campos (`max`, `total`, …, `item`).
    - Retorna um ponteiro; como `Fila` é `struct fila*`, a atribuição fecha certinho.
2. **Inicializa os metadados**:
	- `max = m`: capacidade (tamanho do vetor).
	- `total = 0`: fila começa vazia.
	- `inicio = 0`, `final = 0`: ambos no índice 0.
	    - **Invariante**: com `total == 0`, os valores de `inicio` e `final` são convencionados; o código usa `total` para distinguir vazio/cheio
3. **Aloca o vetor de itens**:
    - `F->item = malloc(m * sizeof(Itemf));`
    - Reserva espaço para `m` elementos.
    - (Boas práticas: verificar `if (!F->item) { free(F); /* erro */ }`.)
4. **Retorna a fila pronta**.
#### As setas das funçõe
Quando você tem um **ponteiro para struct**, acessa campos com `->`.  
`F->total` é açúcar sintático para `(*F).total`
### Funções vaziaf e cheiaf
- `int vaziaf(Fila F) { return (F->total == 0); }`
    - Retorna 1 (verdadeiro) ou 0 (falso). Em C, `int` faz o papel de booleano (ou use `<stdbool.h>` e `bool`).
- `int cheiaf(Fila F) { return (F->total == F->max); }`
    - Cheia quando o número de elementos atingiu a capacidade.
Por que usar `total` em vez de checar `inicio == final`?  
Porque num buffer circular, **`inicio == final` é ambíguo**: pode significar **vazia** ou **cheia**. Existem duas estratégias comuns:
- **Guardar `total`** (como aqui): elimina a ambiguidade; custo: manter e atualizar um contador.
- **Reservar um slot**: considerar “cheia” quando `(final + 1) % max == inicio`, e “vazia” quando `inicio == final`. Custo: capacidade efetiva cai para `max - 1`.
### Função desenfileira(Fila F)
```c
if (vaziaf(F)) { puts("fila vazia!"); abort(); }
Itemf x = F->item[F->inicio];
avanca(F->inicio);
F->total--;
return x;
```
- **Checagem de _underflow_**: não pode remover de fila vazia.
- **Lê o item** na posição `inicio`.
- **Avança `inicio`** circularmente para o próximo elemento.
- **Decrementa `total`** e **retorna** o valor.
Também **O(1)**.

### Função destroif(Fila \*G)
```c
free((*G)->item);
free(*G);
*G = NULL;
```
- Recebe **`Fila *G`**, ou seja, **ponteiro para o ponteiro da fila**.
- Libera primeiro o **vetor de itens**, depois a **estrutura**.
- Em seguida define o **ponteiro do chamador como `NULL`**.  
    Isso evita _dangling pointer_ no escopo do chamador.