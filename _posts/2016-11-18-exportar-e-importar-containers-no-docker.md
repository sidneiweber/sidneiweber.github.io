---
id: 307
title: Exportar e importar containers no docker
date: 2016-11-18T14:56:26-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=307
permalink: /exportar-e-importar-containers-no-docker/
img: /uploads/2016/11/índice-220x159.png
tag: [docker]
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