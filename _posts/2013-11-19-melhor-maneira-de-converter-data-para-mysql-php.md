---
id: 100
title: 'Melhor maneira de converter data para mysql [PHP]'
date: 2013-11-19T14:08:08-03:00
author: Sidnei Weber
layout: post
guid: http://sidiweber.wordpress.com/?p=100
permalink: /melhor-maneira-de-converter-data-para-mysql-php/
categories:
  - Mysql
  - PHP
---
Se você quer converter uma data vinda do MYSQL para o formato PT-BR use o seguinte comando:

<pre>$data = implode("/",array_reverse(explode("-",$data)));</pre>

Assim vai converter a data do mysql para o formato brasileiro.

Ex: 2010-31-04 para 31/04/2010

Se você quer converter uma data em formato brasileiro para inserir no mysql use:

<pre>$data = implode("-",array_reverse(explode("/",$data))); </pre>

O resultado será: 31/04/2010 para 2010-31-04

Fonte: <http://www.l9web.com.br/blog/?p=68>