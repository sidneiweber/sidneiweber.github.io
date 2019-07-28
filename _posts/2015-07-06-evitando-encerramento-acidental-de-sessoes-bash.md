---
id: 186
title: Evitando encerramento acidental de sessões bash
date: 2015-07-06T15:50:35-03:00
author: Sidnei Weber
layout: post
guid: https://sidiweber.wordpress.com/?p=186
permalink: /evitando-encerramento-acidental-de-sessoes-bash/
geo_public:
  - "0"
wp_review_user_reviews:
  - "0"
wp_review_review_count:
  - "0"
categories:
  - Linux
  - Servidores
  - Shell Script
---
A sequência de teclas &#8220;`CTRL+D`&#8221; encerra uma sessão bash. Às vezes digitamos estas teclas por acidente e encerramos uma sessão acidentalmente.

Para evitar que isto ocorra, definimos a variável de ambiente `IGNOREEOF`:

<pre>export IGNOREEOF=1</pre>

Desta forma, para encerrar uma sessão bash, precisamos digitar a sequência &#8220;`CTRL+D`&#8221; duas vezes ou então digitar &#8220;`exit`&#8220;.

Esta variável de ambiente deve ser definida no arquivo `.bashrc`.

Fonte: <a href="http://www.dicas-l.com.br/arquivo/encerramento_acidental_de_sessoes_bash.php#.VDVCZdRdW2w" target="_blank">Dicas-L</a>