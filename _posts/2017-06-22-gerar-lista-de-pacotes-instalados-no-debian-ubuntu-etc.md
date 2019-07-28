---
id: 455
title: Gerar lista de pacotes instalados no Debian, Ubuntu, etc
date: 2017-06-22T13:22:53-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=455
permalink: /gerar-lista-de-pacotes-instalados-no-debian-ubuntu-etc/
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
categories:
  - Debian
  - Linux
tags:
  - dpkg
  - lista de pacotes
---
Para gerar uma lista dos pacotes instalados no sistema, poderemos usar o **dpkg** para isso. Pode ser muito útil na hora de criar sistemas com a mesma base

#### Gerando lista de pacotes

<pre class="lang:sh decode:true ">sudo dpkg --get-selections &gt; install.list</pre>

#### Instalando pacotes a partir da lista

<pre class="lang:sh decode:true ">sudo dpkg --set-selections &lt; install.list
sudo apt-get -y update
sudo apt-get dselect-upgrade</pre>

<a href="http://www.dicas-l.com.br/dicas-l/20161025.php" target="_blank" rel="noopener noreferrer">Fonte</a>