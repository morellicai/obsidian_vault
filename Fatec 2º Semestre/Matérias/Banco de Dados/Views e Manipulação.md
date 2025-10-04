# Definição de View
- Pode ser definida como uma tabela virtual composta por linhas e colunas de dados vindo de tabelas relacionadas em uma query (um agrupamento de SELECT's, por exemplo).
- Se por exemplo precisamos fazer um software em um banco de dados que tem informações sigilosas, as views são criadas para que o desenvolvedor não consiga acessar essas determinadas informações sigilosas
- Tem views comuns, que só servem para visualizar
	- Mas se construir uma view de uma tabela só, podemos fazer CRUD's
	- Mas se construído com joins, não é possível fazer alterações
- São consultas pré-preparaddas
- As linhas e colunas da view simples, são geradas dinamicamente no momento em que é feita uma referência a ela.
## Para que servem?
- Reduzir o tempo de acesso ao sistema gerenciador
- Restringir o acesso a determinados dados
- Filtrar dados especificados de determinadas tabelas
## Vantagens
- **Reuso**: As views são objetos de caráter permanente. E por isso podem ser lidas por vários usuários simultaneamente.
- **Segurança**:
	- Permitem que ocultemos determinadas colunas de uma tabela
	- Facilita o estabelecimento de direitos de acesso a usuários específicos
- Permite que as consultas na própria view sejam mais simples, pois grande parte da complexidade já foi tratada na sua criação
- Também é bom para a velocidade de resposta das consultas. 
	- Por conta disso, é bom utilizar em produção, principalmente em coisas que já não irão mudar
# Criando a View
```sql
CREATE VIEW produto_console 
as select Id, Nome, Fabricante, Quantidade, tipo
from produtos
where Tipo='Console';
```
- No exemplo acima, os vendedores só acessarão somente seus produtos
# Criando View materializada
