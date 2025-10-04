# Curso de GIT
##### Objetivo Geral
- Introduzir ao versionamento de código com git e github
- Conhecer as ferramentas
- Instalar, Configurar e Autenticar
- Mrimeiros passos com git e github
- Dicas e Materiais de Apoio
---
# Instalação, Configuração e Autenticação
* [**Documentação Git**](https://git-scm.com/doc)
## Instalação
No git para llinux, podemos usar, na linha de comando, o gerenciador de pacotes oficial da distribuição
- No meu caso, usando o arch linux, é o pacman
	- `sudo pacman -S git`
---
## Configurações
Temos 3 lugares para configurar o sistema de git:
- --global - É o local que queremos gravar configurações que vai até para o repositório no geral. Para configurações como email e nome que queremos que seja listado em meus git push, e pull requests
- --local - É o local que gravamos configurações para repositórios locais, que não afeta outros nem o repositório online
- --system - É o local que configuramos coisas no git para o sistema (No meu caso, o linux)
---
### Configurações gerais importantes
- `git config --global user.name "nome"` - Configuração para nomear seus commits;
- `git config --global user.email "email"` - Configuração para configurar o email;
- `git config --global init.defaultBranch main` - Nomeia a branch principal default;
#### Configurações de credenciais para o github
A configuração de credenciais é crucial para conseguir clonar e dar push em repositórios que são apenas da nossa conta. Para isso, precisamos ter uma token que é gerado pelo github. 
O caminho para gerar token:
- Settings/Developer Settings/Personal access tokens/tokens(classic)/Generate new token
É Recomendado pelo github que esse token não seja eterno, para segurança 
#### Configuração de chave ssh
A configuração de chave ssh é muito importante principalmente para a segurança na web. Para gerar essa chave de ssh, temos na [documentação do git](https://docs.github.com/pt/authentication/connecting-to-github-with-ssh) como fazer. 

---
# Primeiros Passos com Git e Github
### Comandos principais do git
- `git init` - Iniciar o versionador do git;
- `git remote -v` - Mostra o link para o repositório remoto;
- `git remote add origin ${link_repositore}`- Adiciona um repositório de origem para subir;
	- o origin é um nome, e pode ser alterado. Mas é comumente usado pelos usuários
- `git clone ${link_repositore}` - Comando para clonar um repositório git existente de um servidor para um novo diretório local;
	- Posso clonar passando o caminho onde quero este repositório logo após ao link;
	- Posso também clonar direto uma branch especifica com `--branch &{nome-branch} --single-branch`;
- `git pull` - Puxa as alterações do repositório remoto para o local (busca e mescla);
- `git push` - Empurra as alterações que fiz localmente para o repositório online;
- `git restore &{nome-arquivo}` - comando para restaurar o arquivo modificado por engano;
    - ele restaura o arquivo para o ultimo log registrado;
- `git commit --amend -m "mensagem"` - Comando para reescrever a ultima mensagem do ultimo commit;
    - No caso, sempre será reescrito o commit do ultimo log registrado;
    - se não por o `-m` e a mensagem em "" ele abre uma tela no vim onde você pode editar diretamente a mensagem escrita no ultimo log;
    - `--amend` - Serve para corrigir uma mensagem do ultimo commit
- `git reset --/soft/mixed/hard ${hash}` - Vai para o commit anterior que foi declarado através do hash;
    - `--soft` - Ele volta no commit anterior mas mantem a alteração dos commits posteriores, mantendo os arquivos na area de preparação, a staging area;
    - `--mixed` - Comportamento padrão do comando `git reset`. Este comando mantem os arquivos no commit posterior na untracked area;
    - `--hard` - O comportamento dele é agrecivo. ele reseta o diretório para o commit anterior apagando qualquer arquivo ou linha de código adicionada posterior a esse log;
- `git reflog` - Um listador de logs mais detalhados. Mostra até os logs que foram apagados pelo --hard;
- `git reset &{nome-arquivo} / git restore --staged ${nome-arquivo}` - Retira nosso arquivo de stageding para untracked;
---
# Dicas e Materiais de Apoio