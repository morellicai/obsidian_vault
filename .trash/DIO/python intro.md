---
sticker: emoji//1f40d
---
# Introdução ao Python
Prof: Guilherme Carvalho | @guicarvalho (Linkedin e Github)
   - 9anos de carreira em backend

## Objetivo Geral
> Conhecer um pouco sobre a histótia da linguagem e conhecer onde podemos usar python

### A origem
- Nasceu em 1989 como um hobby do programador Guido Van Rossum
- Influenciado pela linguagem ABC
    - Uma linguagem para facilitar o aprendizado
    - Passado para iniciantes, como o python em teoria passa hoje em dia

### Os objetivos
- Uma linguagem fácil e intuitiva.
- Código aberto, para que todos possam contribuir
- Código tão inteligível quanto o Inglês.
- Adequada para tarefas diáriasm, e produtiva!

## Onde devo usar o Python
Python é uma linguagem muito versáril
- Tipagem dinâmica e forte
    - Não deixa fazer operações como (a - 1)
- Multiplataforma e Multiparadigma
    - Roda em qualquer SO
    - Linux, MacOS, Windows...
- Comunidade gigante e ativa
- Curva de aprendizado baixa
> Só não é boa para APP Mobile!

# Configuração do ambiente de Desenvolvimento
> Instalar e configurar nossa máquina para desenvolver em python
Aqui Foi instalado extenções ideais e o interpretador da linguagem python
Como eu ja tinha tudo isso instalado e ja sabia como funiona, não tera nada anotado

# Primeiro Programa
> Como criar nosso primeiro programa em python

## A Receita
- Para desenvolver um software, basicamente estamos criando uma receita para que o computador faça cada tarefa que instruimos
> Consiste informar ao computador uma sequência de rotinas que devem ser processadas

# O que são tipos?
> Os tipos servem para definir as caracteristicas de um valor a ser alocado pela memória. para que ele possa alocar mais espaço, ou qual tipo de valor sera armazenado para ficar mais facil procurar

## Tipos em Python
> Os tipos built-in são:
| Texto | str |
| Numérico | int, float, complex |
| Sequência | list, tuple, range |
| Mapa | dict |
| Coleção | set, frozenset |
| Booleano | bool |
| Binário | bytes, bytearray, memoryview |

# Tipos numéricos
### Números inteiros
- representados pela classe _int_.
- possuem precisão ilimitada.
    - Exemplos numeros inteiros:
    - 1, 10, 100, -1, -10, -100... 99001823
### Números de ponto flutuante
- Representação por classe float
- Representação para numeros racionais
    - Exemplos:
    - 1.5, -10.543...

# Tipos boleano e string
### Booleano
- É usado para verdadeiro ou falso
- Implementado pela classe _bool_
- True ou False
- Geralmente 0 é False e em python, qualquer numero acima de 0 é True
### Strings
- Cadeia de Caracteres
- Usado para representar valores alfanuméricos
- Em python são utilizado a classe _str_
    - Exemplos:
    - "Python", 'Python', """Python""", '''Python''', "p"

        ```python
        # Tipos de dados
        print(10 + 11) # Saida tem que ser 21
        print(1.5 + 1.5) # Saida tem que ser 3.0
        print(True) # Saida True
        print(False) # Saida False
        print("Python") Saida Python
        ```

# Modo interativo
> Como usar o modo interativo do interpretador python

## O modo interativo
- Podemos executar python em um modo que o resultado saia na hora
### Iniciando o modo
- Podemos no terminal apenas chamar _'python'_ e ja entramos no modo interativo
    - Podemos inicializar ele dentro de um arquivo de um programa escrito. ele Executa o código, e deixa disponivel para que possamos rodar comandos dentro do interpretador naquele arquvio
    - O que é interessante, pois ele me permite rodar comandos como dir e help
#### dir
- Sem arquimentos, retorna a lista de nomes no escopo atual
- dir()
- dir(100) - Tipo inteiro
#### help
- É um sistema que invoca uma ajuda para ver como executar determinadas funções ou coisas assim
- help()
    - Ele esta mostrando tudo como funciona dentro de cada método possivel no python dentro de determinado escopo
- helo(100)
- Basicamente uma documentação integrada dentro do python

## Links Úteis
- [wiki python](https://wiki.python.org.br/ModoInterativo)

# Variáveis e constantes
- **Variaveis:** São locais em minha memoria onde eu posso armazenar um valor.
    - É chamado de variavel, pois ele pode ser alterado no meio do código.
    - Em python, não precisamos declarar o tipo da minha variavel
    - O interpretador faz esse trabalho por mim desde que eu atribuo um valor
    - Se eu não quero atribuir valor de inicio no meu código, eu preciso definir o tipo
    - Para alterar um valor de uma variavel em python, eu só preciso atribuir novamente o valor. e eles se alteram automaticamente
- **Constantes:** São locais em memoria igualmente a variavel, porem, uma vez definida, não posso modificar ela ao longo do meu programa
    - Muito utilizado para armazenar numeros de documentos em programas, ou objetos matematicos como o PI que é uma constante
    - **em Python não temos constantes**
        - Para isso, usamos uma convenção.
        - Usamos o nome todo em maiusculo para que podemos reconhecer que é uma constante

## Boas práticas
- O padrão de nomes deve ser *snake case*
   - Substituindo todo espaço que haveria no nome da variavel por underscor
   - "valor_total" -> Um exemplo de snake case
- Escolher nomes sugestivos
- Nome de constante todo em maiúsculos

# Conversão de Tipos
> Aprender a converter os tipos das variáveis

## Convertendo tipos
- as vezes precisamos alterar o tipo para que possamos fazer algumas operações

#### Inteiro para float
```python
preco = 10
print(preco)
>>> 10

preco = float(preco)
print(preco)
>>> 10.0 # Adicionamos um ponto flutuante ao numero usando
# um construtor do python

preco = 10 / 2
print(preco)
>>> 5.0 # Convertemos para float por que todo resultado de
# divisão em python vai ser float
```
- Se eu utilizar "//" na hora de fazer uma divisão em python, ele preserva o valor em inteiro

#### Numérico para string
- Utilizo o construtor *"str"*
```python
>>> print(str(preco))
10

>>> texto = f"preço {preco}"
>>> print(texto)
preço 10
```
- Fazemos isso justamente para poder concatenar resultados numéricos em uma string
    - O que não é obrigatório. Podemos concatenar numeros inteiros e float numa string. Porém, provavelmente é uma boa pratica transformar em texto