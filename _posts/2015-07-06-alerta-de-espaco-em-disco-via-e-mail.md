---
id: 158
title: Alerta de espaço em disco via e-mail
description: Alerta de espaço em disco via e-mail
date: 2015-07-06T15:39:40-03:00
author: Sidnei Weber
layout: post
permalink: /alerta-de-espaco-em-disco-via-e-mail/
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
  - Shell Script
---
Script para enviar e-mail quando o uso de disco chegar a 90% de uso

<pre class="lang:sh decode:true  ">df -k | grep -e 'lv' | awk '{ print $4 " " $7 }' | while read output;
do
echo $output
usep=$(echo $output | awk '{ print $1}' | cut -d'%' -f1 )
partition=$(echo $output | awk '{ print $2 }' )
if [ $usep -ge 90 ]; then
echo "Verifique o diretorio "$partition" com ($usep%) de uso no servidor $(hostname)" | mail -s "Alerta! Disco excedido em $usep%" seu_email@provedor.com
fi
done
</pre>