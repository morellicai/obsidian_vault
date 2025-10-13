Expressões e Pilhas para Conversão e Avaliação
### 1. Definição e Tipos de Notações de Expressões

Uma expressão aritmética é uma composição de **operandos** (aqui, constantes numéricas, geralmente inteiras de um único dígito, para simplificar), **operadores** (operações aritméticas binárias como adição, subtração, multiplicação e divisão) e **delimitadores** (os parênteses de abertura e fechamento).

O cerne deste estudo reside nas três formas de notação para representar uma expressão:

1. **Infixa:** A forma que usamos naturalmente (Exemplo: A + B). É **fácil de escrever**, mas **difícil de avaliar** por um computador sem regras complexas de precedência e uso de parênteses.
2. **Prefixa (ou Polonesa):** O operador precede os operandos (Exemplo: + A B).
3. **Posfixa (ou Polonesa Reversa):** O operador segue os operandos (Exemplo: A B +). Esta forma é o **objetivo** de conversão, pois é **difícil de escrever**, mas **extremamente fácil de avaliar** por um algoritmo.

### 2. A Vantagem Estratégica da Posfixa

O grande benefício da notação posfixa é que **ela elimina a necessidade de parênteses** e organiza as operações exatamente na sequência em que devem ser realizadas. Isso permite que seu valor seja calculado de maneira eficiente e direta, **utilizando exclusivamente uma pilha**.

O objetivo central é, portanto, **converter uma expressão infixa para sua forma posfixa** e, em seguida, **avaliar o valor** dessa forma posfixa.

#### Estratégia Manual de Conversão (Infixa para Posfixa)

Um método visual de conversão infixa para posfixa é o seguinte:

1. **Parentesiar:** Garantir que a expressão esteja completamente parentesiada, respeitando a prioridade dos operadores.
2. **Transcrever:** Reescrever a expressão, **descartando os parênteses** e **movendo cada operador** para a posição que era ocupada pelo seu respectivo parêntese de fechamento.

### 3. Automatizando a Conversão Infixa para Posfixa

Para que um computador possa realizar a conversão, são necessários algoritmos que utilizam uma pilha $P$ e uma _string_ resultante $s$.

#### Algoritmo Simplificado (1ª Versão – Apenas para Infixa Parentesiada)

Esta versão funciona quando a expressão de entrada já possui todos os parênteses necessários.

- **Parêntese de Abertura:** É simplesmente descartado.
- **Operando:** É anexado imediatamente à expressão posfixa $s$.
- **Operador:** É empilhado em $P$.
- **Parêntese de Fechamento:** Sinaliza o fim de uma subexpressão. O item do topo de $P$ (que deve ser o operador) é desempilhado e anexado a $s$.
- Ao final, $s$ é o resultado.

#### Algoritmo Completo (2ª Versão – Lidando com Prioridades)

Quando a expressão infixa **não está completamente parentesiada**, a prioridade dos operadores deve ser respeitada, exigindo uma lógica mais sofisticada de empilhamento e desempilhamento.

Para isso, é definida uma função de **prioridade** (`prio`): `*` e `/` têm prioridade 2; `+` e `-` têm prioridade 1; `(` tem prioridade 0.

O ponto crucial do Algoritmo da 2ª Versão é o tratamento do parêntese e das prioridades:

1. **Parêntese de Abertura `(`:** É **empilhado** imediatamente em $P$. É importante lembrar que `(` tem **prioridade máxima** quando aparece na expressão de entrada, mas tem **prioridade mínima** quando já está na pilha.
2. **Operando:** É anexado diretamente a $s$.
3. **Operador:** Antes de empilhar o operador atual, verifica-se a pilha. **Enquanto o operador no topo de $P$ tiver prioridade maior ou igual** à do operador que está sendo lido, o operador do topo é **desempilhado e anexado a $s$**. Somente após esse processo, o novo operador é empilhado.
4. **Parêntese de Fechamento `)`:** Isso aciona o desempilhamento. **Enquanto o topo de $P$ não for um parêntese de abertura** `(`, os itens são desempilhados e anexados a $s$. Depois de encontrar `(`, ele é desempilhado e descartado (não vai para $s$).
5. **Finalização:** Se, após percorrer toda a expressão infixa, a pilha $P$ não estiver vazia, todos os operadores restantes devem ser desempilhados e anexados a $s$.

### 4. Avaliação da Forma Posfixa

Uma vez que a expressão esteja na forma posfixa, sua avaliação é simples e segue o "Algoritmo de Avaliação".

O cálculo do valor é feito com uma pilha $P$ vazia, seguindo estas etapas da esquerda para a direita:

- **Operando:** Se o elemento for um operando (seu valor numérico), ele é **empilhado**.
- **Operador:** Se o elemento for um operador, a ação é inversa: **dois valores são desempilhados** de $P$. O valor que foi desempilhado primeiro ($y$) é o segundo operando, e o segundo valor desempilhado ($x$) é o primeiro operando. O operador é aplicado ($x$ [operador] $y$), e o **resultado dessa operação é empilhado de volta** em $P$.
- **Resultado Final:** Ao término da varredura, **o número que permanece no topo de $P$ é o valor final** da expressão.

### 5. Extensões e Outras Notações

Os mesmos princípios de pilha e prioridade podem ser aplicados a outros tipos de expressões.

- **Expressões Booleanas:** Estas expressões usam operandos lógicos (F/0 e V/1) e operadores como `!` (não), `&` (e) e `|` (ou), com prioridades bem definidas. O algoritmo de conversão e avaliação é análogo ao aritmético.
- **Conversão Infixa para Prefixa:** A conversão para a notação prefixa exige uma abordagem modificada: deve-se percorrer a expressão infixa **da direita para a esquerda**. Ferramentas como `strlen()` para tamanho e `_strrev()` para inversão da cadeia podem ser úteis nesse processo. A avaliação da forma prefixa também utiliza pilhas, adaptando a ordem de leitura dos operadores e operandos.