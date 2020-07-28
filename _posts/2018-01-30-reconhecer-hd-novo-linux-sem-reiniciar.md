---
id: 521
title: Reconhecer HD novo Linux sem reiniciar
date: 2018-01-30T20:53:54-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=521
permalink: /reconhecer-hd-novo-linux-sem-reiniciar/
wp_review_user_reviews:
  - "0"
wp_review_review_count:
  - "0"
img: /uploads/2018/01/vmware_client_failed.jpg
categories:
  - Linux
  - Virtualização
tags:
  - hd novo
  - reconhecer hd sem reiniciar
  - vmware hd novo
---
Hoje vamos a mais uma dica rápida. Pra que usa seus servidores virtualizados e precisa adicionar um novo HD seja por falta de espaço ou pelo motivo que for, não precisa reiniciar o servidor para ter o HD reconhecido. Basta apenas executar um simples comando que ordena um "scan" no barramento.

Vale lembrar também que essa dica é para virtualizações com Hot plug habilitado.

```shell
echo "- – -" > /sys/class/scsi_host/host0/scan
```

Obrigado e até a próxima.
