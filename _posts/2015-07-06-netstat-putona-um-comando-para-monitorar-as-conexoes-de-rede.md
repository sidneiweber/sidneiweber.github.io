---
layout: post
title: netstat -putona - Um comando para monitorar as conexões de rede
description: netstat -putona - Um comando para monitorar as conexões de rede
id: 153
date: '2015-07-06 15:37:42 -0300'
author: Sidnei Weber
guid: https://sidiweber.wordpress.com/?p=153
permalink: "/netstat-putona-um-comando-para-monitorar-as-conexoes-de-rede/"
tags: linux
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
