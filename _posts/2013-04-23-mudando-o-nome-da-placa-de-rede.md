---
id: 84
title: Mudando o nome da placa de rede
date: 2013-04-23T12:00:50-03:00
author: Sidnei Weber
layout: post
guid: http://sidiweber.wordpress.com/?p=84
permalink: /mudando-o-nome-da-placa-de-rede/
tagazine-media:
  - 'a:7:{s:7:"primary";s:0:"";s:6:"images";a:1:{s:72:"http://ediomaico.files.wordpress.com/2011/03/70-persistent-net-rules.jpg";a:6:{s:8:"file_url";s:72:"http://ediomaico.files.wordpress.com/2011/03/70-persistent-net-rules.jpg";s:5:"width";i:782;s:6:"height";i:195;s:4:"type";s:5:"image";s:4:"area";i:152490;s:9:"file_path";b:0;}}s:6:"videos";a:0:{}s:11:"image_count";i:1;s:6:"author";s:6:"469294";s:7:"blog_id";s:8:"13481587";s:9:"mod_stamp";s:19:"2013-04-23 12:00:50";}'
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
  - Hardware
  - Linux
---
Semana passada me deparei com a seguinte situação, tinha um servidor com  duas placas de rede , eth0 e eth1 , só que a placa de rede eth0 deu pau e foi trocada, porem, quando foi instalada a nova placa o servidor reconheceu como eth2 .

Para resolver essa situação faça o seguinte:

Com o usuário root edite o arquivo:  
**#vi /etc/udev/rules.d/70-persistent-net.rules**

Apague as linhas:  
<a href="http://ediomaico.files.wordpress.com/2011/03/70-persistent-net-rules.jpg" target="_blank"><img class="" title="70-persistent-net.rules" src="http://ediomaico.files.wordpress.com/2011/03/70-persistent-net-rules.jpg?w=300&h=74" alt="" width="580" height="145" /></a>

Salva, saia e reinicie !

Suas placas voltarão novamente _eth0_ e _eth1. [E.M.B]_

[Fonte](http://ediomaico.wordpress.com/2011/03/21/mudando-o-nome-da-placa-de-rede/)