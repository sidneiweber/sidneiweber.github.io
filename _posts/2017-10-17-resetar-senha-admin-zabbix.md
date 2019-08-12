---
id: 491
title: Resetar senha Admin Zabbix
date: 2017-10-17T09:44:49-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=491
permalink: /resetar-senha-admin-zabbix/
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
image: /wp-content/uploads/2017/10/zabbix.png
categories:
  - Zabbix
---
Hoje vamos a uma dica rápida para quem esqueceu ou não sabe a senha de Admin do painel de administração do Zabbix. Eu estava testando a ferramenta e depois de um tempo se mexer havia esquecido a senha, tive que resetá-la. Para isso a única coisa que precisamos é ter a senha de root do mysql, tendo ela podemos logar no terminal:

<pre class="lang:sh decode:true ">mysql -u root -p
Enter password:</pre>

Dentro do terminal a gente vai fazer o seguinte:

<pre class="lang:default decode:true ">mysql&gt; use zabbix;

mysql&gt; UPDATE users SET passwd=md5(‘novasenha’) WHERE alias=’Admin’;</pre>

Pronto, senha resetada.

[Fonte:](https://jorgepretel.com.br/2016/04/reset-na-senha-admin-do-zabbix/)