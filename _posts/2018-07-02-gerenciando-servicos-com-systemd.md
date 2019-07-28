---
id: 592
title: Gerenciando serviços com SystemD
date: 2018-07-02T21:31:31-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=592
permalink: /gerenciando-servicos-com-systemd/
wp_review_location:
  - bottom
wp_review_desc_title:
  - Resumo
wp_review_color:
  - '#1e73be'
wp_review_fontcolor:
  - '#555555'
wp_review_bgcolor1:
  - '#e7e7e7'
wp_review_bgcolor2:
  - '#ffffff'
wp_review_bordercolor:
  - '#e7e7e7'
wp_review_user_review_type:
  - star
image: /wp-content/uploads/2018/07/Captura-de-tela-de-2018-07-13-20-55-02.png
categories:
  - Linux
tags:
  - systemctl
  - systemd
---
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
