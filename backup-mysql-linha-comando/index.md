# Backup Mysql - Linha Comando


Backup de uma base específica

```shell
mysqldump --database -d NOME DA BASE DE DADOS -u USUARIO -p &gt; c:meu_db.sql
```

Backup de todas as bases

```shell
mysqldump --all-databases -u USUARIO -p &gt; meu_mysql.sql
```

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/backup-mysql-linha-comando/  

