---
id: 166
title: Migração banco de dados Mysql
date: 2015-07-06T15:42:35-03:00
author: Sidnei Weber
layout: post
guid: https://sidiweber.wordpress.com/?p=166
permalink: /migracao-banco-de-dados-mysql/
geo_public:
  - "0"
wp_review_location:
  - bottom
wp_review_desc_title:
  - Resumo
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
count_items:
  - "0"
wp_review_type:
  - none
wp_review_custom_location:
  - "0"
wp_review_custom_colors:
  - "0"
wp_review_custom_author:
  - "0"
wp_review_hide_desc:
  - "0"
wp_review_total:
  - "0"
wp_review_schema:
  - null
wp_review_rating_schema:
  - author
wp_review_show_schema_data:
  - "0"
wp_review_box_template:
  - default
categories:
  - Mysql
---
Para fazer um backup de uma base de dados mysql e copiar para outra base basta fazer os seguintes passos

Os dados que deverão ser alterados são os seguintes:

  * base_origem
  * endereco\_base\_original
  * usuario\_base\_original
  * senha\_base\_original
  * base_destino
  * endereco\_base\_destino
  * usuario\_base\_destino
  * senha\_base\_destino

Sabendo os dados a alterar, substitua-os no comando abaixo e o execute:

<pre class="lang:sh decode:true ">mysqldump base_origem --opt -h endereco_base_original -uusuario_base_original -psenha_base_original --routines --triggers | mysql base_destino -hendereco_base_destino -uusuario_base_destino -psenha_base_destino</pre>

&nbsp;