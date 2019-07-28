---
id: 153
title: 'netstat -putona &#8211; Um comando para monitorar as conexões de rede'
date: 2015-07-06T15:37:42-03:00
author: Sidnei Weber
layout: post
guid: https://sidiweber.wordpress.com/?p=153
permalink: /netstat-putona-um-comando-para-monitorar-as-conexoes-de-rede/
geo_public:
  - "0"
wp_review_user_reviews:
  - "0"
wp_review_review_count:
  - "0"
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
---
<pre class="lang:sh decode:true ">netstat -putona</pre>

Onde os parâmetros significam:

p Mostra as conexões para o protocolo especificado pelo TCP ou UDP  
u Lista todas as portas UDP  
t Lista portas em TCP  
o Exibe temporizadores  
n Exibe o número da porta  
a Exibe todas as conexões do sistema ativo

Por exemplo, para saber que processo ocupa a porta 1521 pode utilizar: [shell]netstat -putona | grep :1521[/shell] 

<a href="http://ubuntulife.wordpress.com/2014/03/11/netstat-putona-un-comando-que-no-olvidaras-para-monitorizar-las-conexiones-en-linux/" target="_blank" rel="noopener noreferrer">Fonte</a>: