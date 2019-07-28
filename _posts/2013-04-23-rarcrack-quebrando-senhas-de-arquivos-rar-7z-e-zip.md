---
id: 82
title: 'Rarcrack &#8211; Quebrando senhas de arquivos rar, 7z e zip'
date: 2013-04-23T11:58:04-03:00
author: Sidnei Weber
layout: post
guid: http://sidiweber.wordpress.com/?p=82
permalink: /rarcrack-quebrando-senhas-de-arquivos-rar-7z-e-zip/
wp_review_user_reviews:
  - "0"
wp_review_review_count:
  - "0"
categories:
  - Linux
---
Ontem fiz download de um arquivo RAR e para minha surpresa o mesmo estava com senha. Antes de procurar outros links resolvi tentar quebrar a senha deste arquivo mesmo, e buscando uma solução no Google eis que acho o _rarcrack_, um brute force para arquivos .rar, .zip e 7-zip.

Faça download do arquivo em:

  * <http://sourceforge.net/projects/rarcrack/files/rarcrack-0.2/%5BUnnamed%20release%5D/>

Feito o download, como root, navegue até a pasta onde salvou o arquivo e faça:

**\# tar -xjf rarcrack-VERSAO.tar.bz2  
\# cd rarcrack-VERSAO**

Você precisará do gcc ou outro compilador C:

**\# make  
\# make install**

Pronto, instalado.

Para usar o rarcrack:

**\# rarcrack &#8211;type *rar nomedoarquivo.rar**

* o type fica a seu critério, dependendo do seu arquivo compactado.

Obs.: Infelizmente acabei não lembrando de cronometrar o processo. Mas após 30~45min o arquivo já estava extraído.

[Fonte](http://www.vivaolinux.com.br/dica/Rarcrack-Quebrando-senhas-de-arquivos-rar-7z-e-zip)