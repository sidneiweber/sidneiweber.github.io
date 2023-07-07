# Migração banco de dados Mysql

Para fazer um backup de uma base de dados mysql e copiar para outra base basta fazer os seguintes passos

Os dados que deverão ser alterados são os seguintes:

  * base_origem
  * endereco\_base\_original
  * usuario\_base\_original
  * senha\_base\_original
  * base_destino
  * endereco\_base\_destino
  * usuario\_base\_destino
  * senha\_base\_destino

Sabendo os dados a alterar, substitua-os no comando abaixo e o execute:

```shell
mysqldump base_origem --opt -h endereco_base_original -uusuario_base_original -psenha_base_original --routines --triggers | mysql base_destino -hendereco_base_destino -uusuario_base_destino -psenha_base_destino
```

---

> Author: Sidnei Weber  
> URL: https://sidneiweber.com.br/migracao-banco-de-dados-mysql/  

