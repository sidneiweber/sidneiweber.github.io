---
id: 182
title: Colocando uma firula no terminal
date: 2015-07-06T15:48:53-03:00
author: Sidnei Weber
layout: post
guid: https://sidiweber.wordpress.com/?p=182
permalink: /colocando-uma-firula-no-terminal/
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
wp_review_user_reviews:
  - "0"
wp_review_review_count:
  - "0"
categories:
  - Linux
  - Shell Script
---
Editar o arquivo .bashrc e adicionar a linha a seguir

<pre>#PS1='[u@h W]$ '
PS1='┌─[u@h W][e[0;32m][${cwd}t][&lt;wbr /&gt;033[0m] ${fill}n[&#092;&#048;33[0m]└─■ '
</pre>