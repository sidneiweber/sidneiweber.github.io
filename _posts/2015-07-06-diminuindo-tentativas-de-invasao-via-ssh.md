---
id: 174
title: Diminuindo tentativas de invasão via SSH
date: 2015-07-06T15:45:47-03:00
author: Sidnei Weber
layout: post
guid: https://sidiweber.wordpress.com/?p=174
permalink: /diminuindo-tentativas-de-invasao-via-ssh/
geo_public:
  - "0"
categories:
  - Linux
  - Servidores
---
Dentro do arquivo `/etc/ssh/sshd_config` altere as seguintes linhas:

    
    LoginGraceTime 2m
    MaxStartups 3:50:6
    
    

Explicando:

O primeiro parâmetro informa que a conexão será cortada caso fique inativa por 2 minutos.

O segundo quer dizer que depois de 3 tentativas não autenticadas, 50% das conexões do IP são recusadas e quando o número de de tentavivas chegar a 6 todas as tentativas de conexões do IP serão recusadas.

Fonte: Dicas-l