---
id: 499
title: Bloquear resposta ao ping com sysctl
date: 2017-10-20T22:21:16-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=499
permalink: /bloquear-resposta-ao-ping-com-sysctl/
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
categories:
  - Linux
  - Rede
---
A dica de hoje é super rápida e prática, para bloquear as respostas de ping podemos usar o comando sysctl:

Para bloquear:

```shell
sysctl -w net.ipv4.icmp_echo_ignore_all=1
```

Para desbloquear:

```shell
sysctl -w net.ipv4.icmp_echo_ignore_all=0
```
