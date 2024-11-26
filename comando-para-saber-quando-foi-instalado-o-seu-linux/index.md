# Comando Para Saber Quando Foi Instalado O Seu Linux


```shell
ls -lct /etc | tail -1 | awk &#39;{print $6, $7, $8}&#39;
```

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/comando-para-saber-quando-foi-instalado-o-seu-linux/  

