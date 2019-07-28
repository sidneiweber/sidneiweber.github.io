---
id: 464
title: 'Dica rápida &#8211; Verificar pastas que ocupam mais espaço'
date: 2017-08-17T13:15:51-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=464
permalink: /dica-rapida-verificar-pastas-que-ocupam-mais-espaco/
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
image: /wp-content/uploads/2016/12/Sele��o_003.png
categories:
  - Linux
  - Shell Script
---
Bom essa dica é bem simples mas muito útil, vamos usar uma combinação de comandos para listar as 5 pastas que mais utilizam espaço no diretório corrente. O bom comando seria esse:

<pre class="lang:sh decode:true ">du -Sh | sort -rh | head -5</pre>

#### Saida:

<pre class="lang:default decode:true ">2,1G	./log/journal/457f9ec73a36473ab3a70f2a1ebce863
196M	./lib/mysql
189M	./lib/docker/aufs/diff/105ad3b8329fb9264b17543f7d70746b1c330f18523f27cdee5ad3fdff966697/usr/bin
116M	./lib/nvidia
111M	./lib/docker/aufs/diff/105ad3b8329fb9264b17543f7d70746b1c330f18523f27cdee5ad3fdff966697/usr/share/cattle/0e44936b6b56ae4372799b0f48e6e934/WEB-INF/lib
</pre>

#### Explicando:

O comando **du** faz a verificação do uso das pastas em si;  
O comando **sort** faz a ordenação do maior pro menor;  
E o comando **head** mostra os 5 primeiros, pode ser usado qualquer quantidade.

Se alguém tiver dúvidas quanto as opções usadas, basta digitar o nome do comando &#8211;help, que terá todas as informações.