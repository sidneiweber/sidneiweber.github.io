---
id: 103
title: Comando para saber quando foi instalado o seu Linux
date: 2013-11-20T19:29:00-03:00
author: Sidnei Weber
layout: post
guid: http://sidiweber.wordpress.com/?p=103
permalink: /comando-para-saber-quando-foi-instalado-o-seu-linux/
categories:
  - Linux
---
<pre>ls -lct /etc | tail -1 | awk '{print $6, $7, $8}'</pre>