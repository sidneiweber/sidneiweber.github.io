# Gerenciando Serviços Com SystemD

Com SystemD é possível gerenciar o sistema e serviços no seu Linux. Ele usa o **Control Groups (CGroups)**, cada serviço iniciado pelo systemd roda dentro de um cgroup separado, fazendo com que se tenha garantia que cada processo iniciado por serviço seja encerrado corretamente.

Para listar todos os serviços em execução:

```shell
systemctl -t service
```

Para ver o status de um serviço:

```shell
systemctl status cups.service
```

Para ativar um serviço na inicialização:

```shell
systemctl enable cups.service
```

Para retirar um serviço da inicialização:

```shell
systemctl disable cups.service
```

Para listar units sendo executadas:

```shell
systemctl

systemctl list-units
```

Para listar units que falharam:

```shell
systemctl --failed
```

Listar os serviços instalados:

```shell
systemctl list-unit-files
```

Reiniciar o sistema:

```shell
systemctl reboot
```

Desliga e encerra o sistema:

```shell
systemctl poweroff
```

Suspender o sistema:

```shell
systemctl suspend
```

Colocar o sistema em modo de hibernação:

```shell
systemctl hibernate
```

Colocar o sistema em modo de suspensão:

```shell
systemctl hybrid-sleep
```


---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/gerenciando-servicos-com-systemd/  

