# Listas encadeadas
- Arquivo `ed-08v2.pptx`
- Professor Fretz
- [[0. Estrutura de Dados - Base | Base]]
---
# Estudos por fora

---
# Listas
> É uma sequência de nós compostos por um item e um ponteiro para o próximo nó
### Observações:
- Cada nó ocupa uma posição arbitrária de memória (a ordem é lógica, não física)
	- Não é um endereço sequencial. Cada ponto da memória ele pode tirar um numero tolamente aleatório
- Operações de inserção, remoção e acesso podem ser feitas em qualquer ponto
- O endereço do primeiro nó é mantido num ponteiro especial
- O último nó da sequência não tem sucessor (seu campo **prox** é **NULL**)
- Um ponteiro inicial com valor igual a **NULL** representa lista vazia
---
> Listas encadeadas é bom para quando preciso alocar uma quantidade de memórias variáveis durante a execução. 
---
- Um vetor é criado com uma quantidade de memórias fixas, Se eu precisar de mais, ou se eu precisar de menos, eu não posso fazer essa alteração. Preciso excluir o vetor e começar de novo com a quantidade de memória diferente
- O que a lista encadeada resolve esse problema. Pois como ele aponta para um endereço especifico de memória que pode estar em qualquer lugar, eu posso trabalhar com ela de forma muito mais simples.


- [[Tipo Lista Encadeada | Construção de uma Lista encadeada]]