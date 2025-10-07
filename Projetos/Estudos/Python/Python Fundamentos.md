- Material professor Rodrigo de Web
- Fundamentos sobre a linguagem python
- Variáveis e tipos de dados
- --
# Configuração de Variáveis de Ambiente
> Python foi criado para ser uma linguagem de propósito geral, popularizado em **automação, ciência de dados, machine learnin e desenvolvimento de software**.

###### Frameworks web populares
- Flask
- Django
- FastAPI
###### Servidores
- uvicorn
- uWSGI
- ASGI

## Um pouco sobre cada Framework
###### Django:
Django é um Framework web python completo que fornece um conjunto abrangente de ferramentas e recursos para construir aplicativos web complexos e escaláveis. Ele vem com tudo o que os desenvolvedores precisam para começar, incluindo autenticação, uma interface administrativa e um Framework leve para tipos de conteúdos bem como muitas outras ferramentas.
###### Flask:
Flask é um microframework Python leve e flexível que se concentra na simplicidade; é conhecido por seu design minimalista e sintaxe direta, o que o torna uma excelente escolha para projetos de pequeno e médio porte e uma ferramenta para iniciantes, graças à pouca quantidade de código clichê que possui.
O Framework permite que os desenvolvedores comecem a construir aplicativos da web rapidamente, sem uma curva de aprendizado ingrime, o que fornece muita liberdade em termos de personalização, permitindo que os desenvolvedores escolhem apenas os componentes de que precisam para seus requisitos específicos de projeto.
###### FastAPI:
FastAPI é um Framework web de alto desempenho que está rapidamente ganhando popularidade para construir APIs. Ele é construído sobre Starlette, um Framework web assíncrono, e usa dicas de tipo Python para validação automática de dados. Ao utilizar programação assíncrona, ele fornece desempenho excepcional e é uma ótima escolha para construir APIs e microsserviços. 
Sem soar muito previsível, uma das vantagens significativas do FastAPI é sua velocidade. Ao fazer uso de programação assíncrona, o FastAPI pode lidar com um grande número de solicitações simultâneas de forma eficiente. Isso o torna perfeito para aplicativos de alto tráfego que exigem processamento de dados em tempo real, e uma vantagem é que ele fornece documentação automática usando Swagger UI, economizando tempo e esforço na documentação

# Sobre Python
> Python é uma linguagem interpretada, tipagem dinâmica e alto nível.

Para rodar python no terminal os comandos são:
```bash
python app.py
```
**Características fundamentais**
- Sensível a indentação (uso obrigatório de espaços ou tabulações)
- Scripts podem ser executados diretamente no terminal

# Ambientes isolados com python basic
- `python -m venv venv` -> Para criar o ambiente virtual
- `source venv/bin/activate` -> Para ativar o ambiente virtual
- `pip freeze > requirements.txt` -> Para congelar dependências
- `pip install -r requirements.txt` -> Para instalar dependências congeladas no projeto
### Ambiente Virtual
- Ferramenta que ajuda a manter dependências de diferentes projetos python separadas, garantindo que bibliotecas específicas não conflitem umas com as outras.
### Packages python
- Pip é o principal instalador de pacotes para Python
- Python Package Index ([PyPI](https://pypi.org/)) é um repositório online que abriga milhares de pacotes Python prontos para uso
# Fundamentos Python
## Identificadores
- É o nome dado a uma variável, função, classe ou módulo 
- pode ter um ou mais caracteres e devem obedecer as seguintes regras:
	- começar com uma letra ou underscor
	- Pode conter letras minúsculas e maiúsculas, números ou underscor
	- Não pode ser utilizado qualquer uma das palavras-chaves reservadas da linguagem
	- Não pode caracteres especiais
## Variáveis e tipos de dados
- Python é considerada **Dinamicamente tipada**, isso signigica que o compilador irá manipular uma variável de acordo com o valor que está sendo definido para a mesma
- Python também é **fortemente tipada**, ou seja, as conversões necessárias em python, são feitas explicitamente.
##### Exemplo:
```python
idade_int = 25
idade_str = "25"
print(type(idade_int)) # printa "int"
print(type(idade_string)) # printa "str"

soma = idade_int + int(idade_string) # Sem a conversão, voltaria um erro ao tentar somar
print(soma)
```
### Principais tipos de dados
- **int**: números inteiros
- **float**: números decimais
- **str**: strings (conjuntos de caracteres)
- **bool**: valores booleanos (**True**, **False**)
```python
nome = "Alice"
idade = 25
altura = 1.65
ativo = True

print(type(nome)) # <class 'str'>
print(type(idade)) # <class 'int'>
print(type(altura)) # <class 'float'>
print(type(ativo)) # <class 'bool'>
``` 
### Principais tipos de Estruturas de Dados
- list
- tuple
- set
- dict
```python
lista = ["apple", "banana", "cherry"]
tupla = ("apple", "banana", "cherry")
set = {"apple", "banana", "cherry"}
dicionario = {
	"nome": "maria",
	"sexo": "feminino",
	"nascido": 1990
}
```
### Indentação
> Em python, os programas são estruturados através de indentação.
##### Exemplo
```python
valor = 12
if valor > 0:
	print("Valor positivo")
	if valor % 2 == 0:
		print("Valor par")
	else:
		print("Valor impar")
else:
	print("Valor negativo")
print("Fim do programa")
```
- No exemplo, temos uma verificação de que se o valor for maior que 0 ele verifica se é par ou impar e da o resultado, se o numero não for maior que 0, ele define como negativo e não testa se é par ou impar. 
- Em python, qualquer indentação quer dizer bloco de código 
### Comentarios
- \# -> comentário inline
- ''' -> Comentário em bloco
```python
'''
Assim que fica
um comentario em bloco
'''
```
### Comandos de saída
- Print é o comando que permite apresentar texto no terminal. 
	- Ele irá imprimir tudo como string e qualquer coisa que não seja string será convertido
- A varias formas de formatar strings dentro do comando print
	- str.format()
	- f-strings
	- concatenação
	- virgulas
#### Exemplos
> Exemplo apenas do str.format() e f-string pois são as unicas diferentes de outras linguagens de forma direta
```python
a = 4
b = 3
'''
Formatação str.format()
'''
print("Valor A: {0}, valor B: {1}".format(a,b))
'''
formatação f-string
'''
print(f"Valor A: {a}, valor B: {b}")
```
### Comandos de Entrada
> Utilizamos o comando `input()` para recever dados que o usuário digitar
```python
valorA = input("Digite o valor de A: ")
valorA = int(input("Digite o valor de A: "))
```
- Como podemos ver, podemos passar o input ja sendo convertido para inteiro para que não acontecer erros de tipos caso seja necessário em nosso programa
- Podemos também fazer o mesmo para `float()` e para `str()`
### Comandos de decisão
> A estrutura mais básica de decisão é formada apenas pelo comando if
```python
if valor > 0:
	print('positivo')
else:
	print('negativo')
```
- Para aninhar varios testes de decisão, podemos usar também o comando `elif`
```python
if idade >= 18:
	print("Maior de idade")
elif idade >= 60 anos
	print("Melhor idade")
else:
	print("Criança")
```
### Operadores Aritméticos
| **Operador** | **Significado** | **Tipos de operandos** | **Tipos de resultado** |
| ------------ | --------------- | ---------------------- | ---------------------- |
| ^, **        | Exponencial     | Inteiro ou real        | inteiro ou real        |
| +            | Soma            | Inteiro ou real        | inteiro ou real        |
| -            | Resto           | Inteiro ou real        | inteiro ou real        |
| *            | Multiplicação   | Inteiro ou real        | inteiro ou real        |
| /            | Divisão         | Real                   | Real                   |
### Operadores de Comparação
```python
print(5<3) # menor que | False
print(5>3) # maior que | True
print(5==3) # igual a | False
print(5!=3) # diferente de | True
print(5>=3) # Maior ou igual a | True
print(5<=3) # Menor ou igual a | False
```
### Laço de repetição FOR
- A sintaxe em python do for é 
	- `for variavel_iteravel in sequência:`
- O for em python iterage numa lista de valores dada na sequência e carrega cada um desses calores para a variável **Variavel_iteravel**m continuando esse processo enquanto houver valores na sequência
##### Exemplo
```python
for valor in [2, 3, 5, 8]:
	print(f"{valor}")
```
### Laço de repetição While
> O *while* irá rep[[0. Estudos PHP]]etir a lista de **Comandos** enquanto a **expressão** for verdadeira
##### Exemplo
```python
i = 0
while i < 10:
	print(f"Valor de i: {i}")
	i += 1
# Ou podemos fazer algo como:
i = True
x = 0
while i:
	print(f"Valor de x: {x}")
	if x >= 10:
		i = False
	x += 1
```
### Declarações Continue e Break
> As declarações *continue* e *break* podem alterar bastante o funcionamento do laço de repetição
- **Continue**: Faz o fluxo pular ao encontrar a condição
- **Break**: faz o fluxo do loop parar
##### Exemplo
```python
for valor in range(-3, 4)
	if valor == 0:
		continue
	print(f"{valor}")
print("--------------------")
for valor in range (-3, 4):
	if valor == 0:
		break
	print(f"{valor}")
'''
Saida:
-3
-2
-1
1
2
3
--------------------
-3
-2
-1
'''
```
# Backend
- **Entender o FastAPI**
- **Criar um servidor básico**
- **Definir endpoints**: Explicar o conceito de endpoint (método HTTP + rota)
---
## Instalando o Fast API e criando um servidor
- [FastAPI](https://fastapi.tiangolo.com/) -> Documentação
---
- `pip install "fastapi[standard]"` - Esse comando instala fastapi e todas suas dependências padrão. Para montar um servidor de ponta a ponta sem precisar instalar outras dependências
- Para criar um servidor com fastapi, temos o seguinte código criado no arquivo base (Meu caso, app.py):
```python
from fastaapi import FastAPI

app = FastAPI()

@app.get("/")
def read_root():
	return {"message": "Olá Mundo!"}
```
- Rodando esse código com o comando `fastapi dev app.py` inicializa com essa mensagem em terminal
```bash
fastapi dev app.py

   FastAPI   Starting development server 🚀

             Searching for package file structure from directories with __init__.py files
             Importing from /home/morelli/Documentos/contratos_project

    module   🐍 app.py

      code   Importing the FastAPI app object from the module with the following code:

             from app import app

       app   Using import string: app:app

    server   Server started at http://127.0.0.1:8000
    server   Documentation at http://127.0.0.1:8000/docs

       tip   Running in development mode, for production use: fastapi run

             Logs:

      INFO   Will watch for changes in these directories:
             ['/home/morelli/Documentos/contratos_project']
      INFO   Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
      INFO   Started reloader process [35853] using WatchFiles
      INFO   Started server process [35855]
      INFO   Waiting for application startup.
      INFO   Application startup complete.
```
- Se quiser mais controle, podemos chamar diretamente dentro do código do app.py o uvicorn, onde definimos o host e a porta também. adicionando a condicional ao final do código
```python
if __name__ == "__main__":
	import uvicorn
	uvicorn.run(app, host="127.0.0.1", port="8000")
```
## Conceito de Endpoint
> Um endpoint é a junção de um **Método** HTTP (GET, POST, PUT, DELETE) e uma **rota** (por exemplo, "/users"), onde o servidor resposnde a uma solicitação.
> Um local centralizado onde é recebido uma **requisição**
### Conceito de Rota
- Uma rota é uma URL associada a um método HTTP. 
- A rota / sempre sera com o método get que responde a uma requisição feita para a raiz da aplicação
- Uma função que define o que deve ser feito quando esse caminho é solicitado.
	- Função que pode processar dados, renderizar uma pagina, enviar respostas em JSON e até redirecionar o usuário para outra página
###### O que tem numa rota:
- **Método HTTP** -> Define o tipo de ação ou operação que será realizada
- **Caminho da URL** -> A parte da URL que identifica a rota (Semelhante a rotas de diretórios e arquivos)
- **Handler (Controlador)** -> A função ou o conjunto de funções que processam a requisição e determinam a resposta