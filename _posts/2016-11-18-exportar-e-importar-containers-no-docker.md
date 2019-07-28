---
id: 307
title: Exportar e importar containers no docker
date: 2016-11-18T14:56:26-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=307
permalink: /exportar-e-importar-containers-no-docker/
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
image: /wp-content/uploads/2016/11/índice-220x159.png
categories:
  - Docker
---
### Exportando imagem

Temos aqui novamente um processo bem simples no docker, para exportar uma imagem uitlizamos o comando

<pre class="lang:default decode:true">root@black:/media/documentos# docker save debian-apache &gt; /tmp/imagem.tar
root@black:/media/documentos/Programação/Shell Script# ls -lh /tmp/
-rw-r--r-- 1 root   root  225M nov 18 14:50 imagem.tar</pre>

### Importando imagem

<pre class="lang:default decode:true">root@black:/media/documentos# docker load &lt; imagem.tar</pre>

Fala a verdade é simples ou não é, mais fácil que isso não tem como.

<a href="http://devopslab.com.br/docker-como-criar-uma-imagem-docker-a-partir-de-um-container-utilizando-o-docker-commit/" target="_blank">Fonte</a>