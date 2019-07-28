---
id: 550
title: Instalando e gerenciando programas no Windows com Chocolatey
date: 2018-04-17T19:38:34-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=550
permalink: /instalando-e-gerenciando-programas-no-windows-com-chocolatey/
image: /wp-content/uploads/2018/04/Captura-de-tela-de-2018-04-17-20-38-48.png
categories:
  - Windows
tags:
  - chocolatey
---
Hoje lhes apresento uma ferramenta muito boa para gerenciar os programas no Windows, chamada <a href="https://chocolatey.org/" target="_blank" rel="noopener">Chocolatey</a>. Para quem está acostumando com gerenciadores de pacotes do Linux como apt, yum, etc, vai se sentir em casa. Ele consegue instalar e atualizar e remover diversos programas, facilitando muito o trabalho dos técnicos e até para gerenciar um grande parque de máquinas do seu trabalho.

O programa é suporte do Windows 7 em diante e Windows server 2003 em diante, tem como pré requisito o programa .NET Framework 4+.

A instalação é bem simples e pode ser feita via **cmd** ou **Powershell**

Instalando via CMD:

<script src="https://gist.github.com/sidneiweber/4ea0bebfaa810888cc2cdd8068c58105.js"></script>

Instalando via Powershell

<script src="https://gist.github.com/sidneiweber/2d1627b19433cb39244f06cbbb39d6aa.js"></script>

Após a instalação o comando choco já estará disponivel. Segue algumas opções do comando:

  * list &#8211; Lista os pacotes disponíveis, enquanto fazia testes haviam incríveis **5644 pacotes**
  * search &#8211; Realiza pesquisa de pacotes
  * info &#8211; Traz informações sobre um pacote
  * install &#8211; Obviamente, instala
  * upgrade &#8211; Atualiza
  * uninstall &#8211; Adivinhe, remove 🙂

Caso queiramos instalar o VLC por exemplo:

```shell
choco install vlc
```

<img src="http://sidneiweber.com.br/wp-content/uploads/2018/04/Captura-de-tela-de-2018-04-17-20-32-04.png" alt="" width="647" height="348" srcset="https://sidneiweber.com.br/wp-content/uploads/2018/04/Captura-de-tela-de-2018-04-17-20-32-04.png 647w, https://sidneiweber.com.br/wp-content/uploads/2018/04/Captura-de-tela-de-2018-04-17-20-32-04-300x161.png 300w" sizes="(max-width: 647px) 100vw, 647px" />

Há também uma página onde pode se verificar uma lista com os pacotes pelo link <a href="https://chocolatey.org/packages." target="_blank" rel="noopener">https://chocolatey.org/packages.</a>

Sem contar ainda em um gerenciador gráfico chamado Chocolatey GUI, que pode sem instalado com o comando _choco install chocolateygui._

<img class="alignnone size-full" src="https://chocolatey.org/content/images/ChocolateyGUI_main_screen.png" width="1013" height="699" />

&nbsp;
