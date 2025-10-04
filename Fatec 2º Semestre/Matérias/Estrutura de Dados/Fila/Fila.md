- [[0. Estrutura de Dados - Base | Base]]
> É uma lista de itens em que as inserções são feitas num extremo, denominado **final**, e as remoções são feitas no extremo oposto, denominado **início**

### Funcionamento:
- Quando um item é inserido numa fila, ele é colocado no seu final.
- Apenas o item no início da fila pode ser removido.
- Essa política de acesso é denominada **FIFO** (Fist-In/First-Out).
#### Exemplos de aplicação
- Fila de impressão de arquivos num sistema operacional.
- Fila de escalonamento de processos num sistema operacional
---
> Fila é útil em qualquer situação em que precisamos **manter** a ordem de uma sequência!
---
## Operações em filas
- **Fila**(m)
	- Cria e devolve uma fila vazia **F**, com tamanho **m**.
- **vaziaf**(F)
	- Devolve verdaded se, e só se, a fila **F** estiver vazia.
- **cheiaf**(F)
	- Devolve verdade se, e só se, a fila **F** estiver cheia.
- **enfileira**(x,F)
	- Insere o item **x** no final da fila **F**.
- **desenfileira**(F)
	- Remove e devolve o item que estiver no inicio de **F**
- **destroif**(&F)
	- Destrói a fila **F**
---
- [[fila.h | Sobre o Arquivo fila.h]]