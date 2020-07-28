---
id: 373
title: Alterando hostname sem reiniciar computador
date: 2017-02-03T14:15:55-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=373
permalink: /alterando-hostname-sem-reiniciar-computador/
img: /uploads/2016/05/cropped-captura_de_tela-300x167.jpg
categories:
  - Linux
---
Para podermos alterar o nome da máquina sem precisar reiniciar é muito simples. Primeiramente precisamos alterar o arquivo /etc/hostname. Mas após a alteração notamos que o nome não muda, mesmo dando o comando hostname, o nome continua o antigo. Para essa alteração valer sem precisar reiniciar, pois as vezes pode se tratar de um servidor que não pode parar no momento, basta digitar o comando abaixo:

<pre class="lang:sh decode:true ">echo "novo-hostname" &gt; /proc/sys/kernel/hostname</pre>

Pronto, problema resolvido.

[Fonte](https://www.vivaolinux.com.br/dica/Debian-Wheezy-Alterando-hostname-sem-reiniciar)