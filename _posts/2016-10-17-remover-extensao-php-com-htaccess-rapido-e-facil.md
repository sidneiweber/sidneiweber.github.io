---
id: 290
title: Remover extensão .php com .htaccess (Rápido e fácil)
date: 2016-10-17T14:34:10-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=290
permalink: /remover-extensao-php-com-htaccess-rapido-e-facil/
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
image: /wp-content/uploads/2016/10/Seleção_012-220x162.png
categories:
  - PHP
tags:
  - extensao .htaccess
  - remover extensao .php
---
Já havia tentado de várias maneiras remover a extensão .php dos meus arquivos, mas todas sem sucesso. Porém consegui fazer de uma maneira muito simples, editando o arquivo .htaccess. Lembrando que para funcionar a modulo &#8220;mod_rewrite&#8221; deve estar habilitado no seu servidor web.

Criaremos o arquivo .htaccess na raiz do nosso projeto com o seguinte conteúdo

<pre class="lang:default decode:true" title="remover extensão .php">&lt;IfModule mod_rewrite.c&gt;
RewriteEngine on
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME}.php -f
RewriteRule ^(.*)$ $1.php

&lt;/IfModule&gt;</pre>

E quando formos criarmos nosso link no php, aqui no caso estamos com o exemplo signup.php, basta digitar assim:

<pre class="lang:default decode:true ">&lt;a href="signup"&gt;signup here&lt;/a&gt;</pre>

Sem a extensão .php. O servidor irá fazer todo o resto do trabalho.

[Fonte](http://www.codingcage.com/2015/11/how-to-remove-php-html-extensions-with.html)