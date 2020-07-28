---
id: 215
title: Instalar Java 8 no Manjaro/Archlinux
date: 2015-11-12T00:10:33-03:00
author: Sidnei Weber
layout: post
guid: https://sidiweber.wordpress.com/?p=215
permalink: /instalar-java-8-no-manjaroarchlinux/
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
img: /uploads/2015/11/Java_620X0-220x162.jpg
categories:
  - Arch
  - Java
  - Linux
tags:
  - java arch
  - java manjaro
---
Primeiro atualize o sistema

<pre># pacman -Sy</pre>

Após isso baixamos a última versão (Na data da postagem essa era última versão)

<pre>$ wget http://javadl.sun.com/webapps/download/AutoDL?BundleId=111679 -O Java-latest</pre>

Descompactamos

<pre>$ tar -zxvf   Java-latest</pre>

Copiamos para a pasta correta

<pre>cp -pr jre1.8.0_60 /opt</pre>

Criamos o link para o programa

<pre>ln -s /opt/jre1.8.0_60/bin/java /usr/bin/java</pre>

E o link para os plugins:

<pre>ln  -s /opt/jre1.8.0_65/lib/amd64/libnpjp2.so  ~/.mozilla/plugins/libnpjp2.so</pre>

<a href="http://www.unixmen.com/install-java-8-manjaroarchlinux/" target="_blank">Fonte</a>