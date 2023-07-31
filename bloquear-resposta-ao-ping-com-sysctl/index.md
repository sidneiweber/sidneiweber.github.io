# Bloquear resposta ao ping com sysctl

A dica de hoje é super rápida e prática, para bloquear as respostas de ping podemos usar o comando sysctl:

Para bloquear:

```shell
sysctl -w net.ipv4.icmp_echo_ignore_all=1
```

Para desbloquear:

```shell
sysctl -w net.ipv4.icmp_echo_ignore_all=0
```


---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/bloquear-resposta-ao-ping-com-sysctl/  

