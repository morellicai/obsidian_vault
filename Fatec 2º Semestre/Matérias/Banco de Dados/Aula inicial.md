# Iniciar a criação de conta de um usuário do oracleDB

## Criação de usuário no Oracle
**Comando**: 
```sql
SQL> create user c##<nome> identified by c##<nome> default tablespaces user quota 30M on users;
```
- Cria usuário numa tablespace padrão que ja vem no oracle chamada user. 
- quota é a memória alocada para esse usuário, que no caso sera 30 megas
- O nome é preciso c## para identificar
- **Trocar `<nome>` para o meu nome ou outro nome que seja comum para o uso** 

Agora precisamos dar um direito ao usuário para que ele possa criar as tabelas, possa fazer as ações necessários e o direito de se conectar com o banco
O comando é:
```sql
grant connect, resource to c##<nome>
```

- para desconectar do banco é o comando disc
- Para conectar, comando conn
