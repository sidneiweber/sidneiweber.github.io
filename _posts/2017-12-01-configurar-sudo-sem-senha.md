---
id: 508
title: Configurar sudo sem senha
date: 2017-12-01T21:29:13-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=508
permalink: /configurar-sudo-sem-senha/
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
wp_review_user_reviews:
  - "0"
wp_review_review_count:
  - "0"
image: /wp-content/uploads/2016/12/Sele��o_003.png
categories:
  - Linux
---
Para configurar o uso do uso sem senha, o que não é recomendado, somente em casos de algum programa precise de permissão para executar determinado comando. Podemos usar como exemplo o Zabbix que quer rodar algum programa com privilégio de root sem comprometer a segurança. O arquivo a ser editado será o /etc/sudoers:

Configurar sudo sem senha para tudo:

```shell
zabbix    ALL=NOPASSWD: ALL
```

Ou podemos configurar para executar somente algo em específico:

```shell
zabbix ALL=NOPASSWD: /usr/bin/nmap
# Mais de um comando
zabbix ALL=NOPASSWD: /usr/bin/nmap, /etc/init.d/apache2 restart
```

E por hoje era isso pessoal, aquele abraço
