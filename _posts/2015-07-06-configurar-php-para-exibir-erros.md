---
id: 160
title: Configurar PHP para exibir erros
date: 2015-07-06T15:40:25-03:00
author: Sidnei Weber
layout: post
guid: https://sidiweber.wordpress.com/?p=160
permalink: /configurar-php-para-exibir-erros/
geo_public:
  - "0"
categories:
  - Apache
  - PHP
---
Essa configuração útil quando estamos desenvolvendo e precisamos ver alguns erros gerados pelo nosso código. Basta editar o arquivo **php.ini** que no Linux geralmente fica em **/etc/php5/apache2/php.ini** e trocar a configuração da chave:

_display_errors = Off_

Para On