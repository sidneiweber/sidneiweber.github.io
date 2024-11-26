# Tutorial Básico E Rápido De Mysql


## Instalação

Começamos pela instalação, que nas distribuições Debian like seria:

```shell
sudo apt-get install mysql-server phpmyadmin
```

Esse comando instalará a última versão do Mysql e do administrador visual que mais gosto o PHPmyadmin. A instalação irá pedir uma senha para o usuário padrão (root):

![mysql &gt;&lt;](/img/uploads/2016/07/Seleção_003.png)

A confirmação da senha:

![mysql &gt;&lt;](/img/uploads/2016/07/Seleção_004.png)

Em qual servidor web o Phpmyadmin irá rodar, no meu caso apache:

![mysql &gt;&lt;](/img/uploads/2016/07/Seleção_005.png)

E diga não a próxima opção:

![mysql &gt;&lt;](/img/uploads/2016/07/Seleção_006.png)

## Administrando via linha de comando

```shell
mysql -h host -u root -p (o super usuário default é root)
```

Assim terá acesso ao terminal do mysql.

## Comandos de uso básico

Para ter acesso a linha de comando mysql localhost, após o comando será solicitado a senha de admin do mysql

```shell
mysql -u root -p
```

Criar base de dados:

```sql
create database nomebanco;
```

Para editar o banco de dados:

```sql
use nomebanco;
```

Criar tabela:

```sql
create table nometabela(campos tipos...);
```

Exemplo

```sql
CREATE TABLE usuario
(
id int,
nome varchar(255),
sobrenome varchar(255),
endereco varchar(255),
cidade varchar(255)
);
```

Mostrar conteudo da tabela:

```sql
select * from nometabela;
```

Exibir bancos de dados:

```sql
show databases;
```

Exibir tabelas:

```sql
show tables;
```

Exibir informações das tabelas, a formação das informações:

```sql
describe nometabela;
```

![mysql &gt;&lt;](/img/uploads/2016/07/Seleção_007.png) 

## Exportar e importar via linha de comando

Exportar

```shell
mysqldump -u user -p passwd banco &gt; banco.sql
```

Importando:

```shell
mysql -u user -p password banco &lt; banco.sql
```

Esse é o tutorial bem básico sobre o uso do mysql.

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/tutorial-basico-e-rapido-de-mysql/  

