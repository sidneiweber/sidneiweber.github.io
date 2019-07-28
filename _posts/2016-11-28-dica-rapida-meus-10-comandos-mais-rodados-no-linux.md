---
id: 330
title: '[Dica rápida] Meus 10 comandos mais rodados no linux'
date: 2016-11-28T15:39:52-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=330
permalink: /dica-rapida-meus-10-comandos-mais-rodados-no-linux/
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
image: /wp-content/uploads/2015/07/cropped-captura_de_tela-220x162.jpg
categories:
  - Linux
---
Com este comando podemos conferir quais os 10 comandos mais rodados em nossa máquina:

<pre class="lang:default decode:true ">history|awk '{print $2}'|awk 'BEGIN {FS="|"} {print $1}'|sort|uniq -c|sort -rn|head -10</pre>

Meu resultado foi:

<pre class="lang:sh decode:true ">sidnei@black:~$ history|awk '{print $2}'|awk 'BEGIN {FS="|"} {print $1}'|sort|uniq -c|sort -rn|head -10
    248 sudo
    148 vi
    101 sh
     49 ping
     49 ls
     40 systemctl
     38 ifconfig
     38 htop
     31 ps
     26 du
sidnei@black:~$</pre>

&nbsp;