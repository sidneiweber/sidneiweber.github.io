# Pesquisar Em Um Intervalo De Datas Mysql


```sql
SELECT * FROM `contas_pagar` WHERE data BETWEEN (&#39;2014-09-01&#39;) AND (&#39;2014-09-31&#39;);
```

E para fazer uma soma em um intervalo de datas:

```sql
SELECT SUM(valor) as total FROM contas_pagar WHERE valor BETWEEN (&#39;2014-09-01&#39;) AND (&#39;2014-09-31&#39;);
```

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/pesquisar-em-um-intervalo-de-datas-mysql/  

