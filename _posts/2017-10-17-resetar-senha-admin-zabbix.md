---
id: 491
title: Resetar senha Admin Zabbix
date: 2017-10-17T09:44:49-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=491
permalink: /resetar-senha-admin-zabbix/
img: /uploads/2017/10/zabbix.png
tag: [zabbix]
---
Hoje vamos a uma dica rápida para quem esqueceu ou não sabe a senha de Admin do painel de administração do Zabbix. Eu estava testando a ferramenta e depois de um tempo se mexer havia esquecido a senha, tive que resetá-la. Para isso a única coisa que precisamos é ter a senha de root do mysql, tendo ela podemos logar no terminal:

<pre class="lang:sh decode:true ">mysql -u root -p
Enter password:</pre>

Dentro do terminal a gente vai fazer o seguinte:

<pre class="lang:default decode:true ">mysql&gt; use zabbix;

mysql&gt; UPDATE users SET passwd=md5(‘novasenha’) WHERE alias=’Admin’;</pre>

Pronto, senha resetada.

[Fonte:](https://jorgepretel.com.br/2016/04/reset-na-senha-admin-do-zabbix/)