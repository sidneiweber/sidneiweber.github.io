---
id: 10
title: Codecs ubuntu 9.04
date: 2009-09-23T19:27:02-03:00
author: Sidnei Weber
layout: post
guid: http://clancpd.com.br/sidneiweber/?p=10
permalink: /codecs-ubuntu-904/
categories:
  - Ubuntu
---
Paso #1: Agregar el Repositorio de Medibuntu  
Abre el terminal ubicado en Aplicaciones/Accesorios/Terminal, y ejecuta el siguiente comando:

> sudo wget http://www.medibuntu.org/sources.list.d/jaunty.list –output-document=/etc/apt/sources.list.d/medibuntu.list

Paso #2: Agregar la llave GPG  
Ahora ejecuta este otro comando:

> sudo apt-get update && sudo apt-get install medibuntu-keyring && sudo apt-get update

Paso #3: Instalar Codec’s  
Ahora podemos instalar los codec’s que necesitemos. Ejecuta cada linea en el Terminal para instalar el codec nombrado:

> sudo apt-get install libdvdcss2  
> sudo apt-get install w32codecs  
> sudo apt-get install non-free-codecs  
> sudo apt-get install ffmpeg

Si deseas instalar todo de una sola vez solo ejecuta esto:

> sudo apt-get install libdvdcss2 w32codecs non-free-codecs ffmpeg