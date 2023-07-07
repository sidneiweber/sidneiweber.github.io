# Backup Mysql - Linha comando


Backup de uma base específica

```shell
mysqldump --database -d NOME DA BASE DE DADOS -u USUARIO -p > c:meu_db.sql
```

Backup de todas as bases

```shell
mysqldump --all-databases -u USUARIO -p > meu_mysql.sql
```

---

> Author: Sidnei Weber  
> URL: https://sidneiweber.com.br/backup-mysql-linha-comando/  

