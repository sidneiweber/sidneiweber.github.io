# Pesquisar em um intervalo de datas Mysql


```sql
SELECT * FROM `contas_pagar` WHERE data BETWEEN ('2014-09-01') AND ('2014-09-31');
```

E para fazer uma soma em um intervalo de datas:

```sql
SELECT SUM(valor) as total FROM contas_pagar WHERE valor BETWEEN ('2014-09-01') AND ('2014-09-31');
```

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/pesquisar-em-um-intervalo-de-datas-mysql/  

