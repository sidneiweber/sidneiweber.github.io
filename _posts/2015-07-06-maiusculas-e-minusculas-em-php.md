---
id: 178
title: Maiúsculas e Minúsculas em PHP
description: Maiúsculas e Minúsculas em PHP
date: 2015-07-06T15:47:02-03:00
author: Sidnei Weber
layout: post
guid: https://sidiweber.wordpress.com/?p=178
permalink: /maiusculas-e-minusculas-em-php/
geo_public:
  - "0"
categories:
  - PHP
---
$texto =&#8221;warquia pereira santos&#8221;;  
vamos transforma a variavel $texto

**=> Converte a string para letras minúsculas**  
strtolower();  
ex: srttolower($texto);  
vai sair assim = warquia pereira santos

**=> Converte a string para letras maiúsculas**  
strtoupper();  
ex: srttoupper($texto);  
vai sair assim = WARQUIA PEREIRA SANTOS

**=> Converte o primeiro caractere de uma string em maiúsculo**  
ucfirst();  
ex: ucfirst($texto);  
vai sair assim = Warquia pereira santos

**=> Converte em maiúsculo o primeiro caractere de cada palavra contida em uma string**  
ucwords();  
ex: ucwords($texto);  
vai sair assim = Warquia Pereira Santos

<a href="http://phpbrasil.com/artigo/bG73TMFSCr3H/maiusculas-e-minusculas-em-php" target="_blank">Fonte</a>