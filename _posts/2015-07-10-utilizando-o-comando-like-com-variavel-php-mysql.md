---
id: 205
title: 'Utilizando o comando like com variável [PHP-MySQL]'
date: 2015-07-10T16:48:54-03:00
author: Sidnei Weber
layout: post
guid: https://sidiweber.wordpress.com/?p=205
permalink: /utilizando-o-comando-like-com-variavel-php-mysql/
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
  - Mysql
  - PHP
---
<pre class="lang:php decode:true ">include("conexao.php");
$busca = $_POST['busca'];
// comando like com variavel
// retorna todos os produtos que tenham o valor da variável busca em qualquer posição
$result = mysql_query("SELECT descricao FROM produtos WHERE descricao like '%".$busca."%' ");

// comando like normal
//retorna todos os nomes que tenham a palavra "pedro" em qualquer posição
$result = mysql_query(" SELECT nome FROM funcionarios WHERE nome like '%pedro%' ");</pre>

&nbsp;