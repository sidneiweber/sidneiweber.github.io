# netstat -putona - Um comando para monitorar as conexões de rede


```shell
netstat -putona
```

Onde os parâmetros significam:

p Mostra as conexões para o protocolo especificado pelo TCP ou UDP  
u Lista todas as portas UDP  
t Lista portas em TCP  
o Exibe temporizadores  
n Exibe o número da porta  
a Exibe todas as conexões do sistema ativo

Por exemplo, para saber que processo ocupa a porta 1521 pode utilizar: 

```shell
netstat -putona | grep :1521
```

[Fonte](http://ubuntulife.wordpress.com/2014/03/11/netstat-putona-un-comando-que-no-olvidaras-para-monitorizar-las-conexiones-en-linux/)


---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/netstat-putona-um-comando-para-monitorar-as-conexoes-de-rede/  

