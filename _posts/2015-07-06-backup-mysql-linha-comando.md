---
id: 180
title: 'Backup Mysql &#8211; Linha comando'
date: 2015-07-06T15:48:02-03:00
author: Sidnei Weber
layout: post
guid: https://sidiweber.wordpress.com/?p=180
permalink: /backup-mysql-linha-comando/
geo_public:
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
  - Mysql
---
Backup de uma base específica

<pre>mysqldump --database &lt;NOME DA BASE DE DADOS&gt; -u&lt;USUARIO&gt; -p &gt; c:meu_db.sql</pre>

Backup de todas as bases

<pre>mysqldump --all-databases -u&lt;USUARIO&gt; -p &gt; meu_mysql.sql</pre>