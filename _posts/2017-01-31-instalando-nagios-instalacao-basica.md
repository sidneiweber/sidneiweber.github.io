---
id: 359
title: 'Instalando Nagios &#8211; Instalação básica'
date: 2017-01-31T13:11:40-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=359
permalink: /instalando-nagios-instalacao-basica/
wp_review_location:
  - bottom
wp_review_desc_title:
  - Resumo
wp_review_total:
  - "0"
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
wp_review_user_reviews:
  - "0"
wp_review_review_count:
  - "0"
count_items:
  - "0"
wp_review_type:
  - none
wp_review_custom_location:
  - "0"
wp_review_custom_colors:
  - "0"
wp_review_custom_author:
  - "0"
wp_review_hide_desc:
  - "0"
wp_review_schema:
  - null
wp_review_rating_schema:
  - author
wp_review_show_schema_data:
  - "0"
wp_review_box_template:
  - default
image: /wp-content/uploads/2017/01/nagios_logo_black.png
categories:
  - Nagios
---
Vamos fazer a instação básica do Nagios. Pra quem não conhece o Nagios, segue um <a href="https://pt.wikipedia.org/wiki/Nagios" target="_blank" rel="noopener">link para conhecer melhor</a>.

> **Nagios** é uma popular aplicação de monitoramento de rede de [código aberto](https://pt.wikipedia.org/wiki/C%C3%B3digo_aberto "Código aberto") distribuída sob a licença [GPL](https://pt.wikipedia.org/wiki/GNU_General_Public_License "GNU General Public License"). Ele pode monitorar tanto hosts quanto serviços, alertando quando ocorrerem problemas e também quando os problemas são resolvidos.

Faremos a instalação no Debian, que é uma distribuição de minha preferência. O Nagios pode ser instalado em qualquer sistema Linux, a única diferença que pode ocorrer é a instalação de dependências e/ou alguma localização de pastas

<div id="toc_container" class="no_bullets">
  <p class="toc_title">
    P&aacute;gina de Posts
  </p>
  
  <ul class="toc_list">
    <li>
      <a href="#Instalacao_das_dependencias"><span class="toc_number toc_depth_1">1</span> Instalação das dependências</a>
    </li>
    <li>
      <a href="#Baixando_Nagios"><span class="toc_number toc_depth_1">2</span> Baixando Nagios</a>
    </li>
    <li>
      <a href="#Extraindo_Pacotes"><span class="toc_number toc_depth_1">3</span> Extraindo Pacotes</a>
    </li>
    <li>
      <a href="#Adicionar_usuario_Nagios"><span class="toc_number toc_depth_1">4</span> Adicionar usuário Nagios</a>
    </li>
    <li>
      <a href="#Instalacao"><span class="toc_number toc_depth_1">5</span> Instalação</a><ul>
        <li>
          <a href="#Compilando_Nagios"><span class="toc_number toc_depth_2">5.1</span> Compilando Nagios</a>
        </li>
        <li>
          <a href="#Criando_usuario_e_senha_do_Nagios"><span class="toc_number toc_depth_2">5.2</span> Criando usuário e senha do Nagios</a>
        </li>
        <li>
          <a href="#Compilando_os_plugins"><span class="toc_number toc_depth_2">5.3</span> Compilando os plugins</a>
        </li>
      </ul>
    </li>
  </ul>
</div>

### <span id="Instalacao_das_dependencias">Instalação das dependências</span>

<pre class="lang:sh decode:true ">sudo apt-get install wget build-essential apache2 php-gd libgdchart-gd2-xpm libgdchart-gd2-xpm-dev libapache2-mod-php</pre>

### <span id="Baixando_Nagios">Baixando Nagios</span>

Baixaremos a última versão dos pacotes Nagios Core e Nagios Core Plugins pelo site https://www.nagios.org/downloads/. Ou diretamente pelos links abaixo:

<a href="https://assets.nagios.com/downloads/nagioscore/releases/nagios-4.2.4.tar.gz#_ga=1.92809877.98229964.1480095349" target="_blank" rel="noopener">Nagios Core</a>

<a href="https://nagios-plugins.org/download/nagios-plugins-2.1.4.tar.gz#_ga=1.114959247.98229964.1480095349" target="_blank" rel="noopener">Nagios Plugins</a>

### <span id="Extraindo_Pacotes">Extraindo Pacotes</span>

<pre class="lang:default decode:true ">tar -xzvf nagios-4.2.4.tar.gz
tar -xzvf nagios-plugins-2.1.4.tar.gz</pre>

### <span id="Adicionar_usuario_Nagios">Adicionar usuário Nagios</span>

<pre class="lang:sh decode:true ">useradd nagios
groupadd nagios
usermod -a -G nagios nagios
usermod -a -G nagios www-data</pre>

### <span id="Instalacao">Instalação</span>

#### <span id="Compilando_Nagios">Compilando Nagios</span>

<pre class="lang:default decode:true">cd nagios-4.2.4
./configure --with-command-group=nagios

make all
make install
make install-init
make install-config
make install-commandmode
make install-webconf</pre>

Reiniciando o apache

<pre class="lang:default decode:true ">service apache2 restart</pre>

#### <span id="Criando_usuario_e_senha_do_Nagios">Criando usuário e senha do Nagios</span>

<pre class="lang:sh decode:true">htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin</pre>

#### <span id="Compilando_os_plugins">Compilando os plugins</span>

<pre class="lang:sh decode:true ">cd ..
cd nagios-plugins-2.1.4
./configure --with-nagios-user=nagios --with-nagios-group=nagios
make
make install</pre>

Habilitar CGI no apache

<pre class="lang:sh decode:true ">cp /etc/apache2/mods-available/cgi.load /etc/apache2/mods-enabled/
service apache2 reload</pre>

Antes de fazer qualquer alteração nas configurações, teste se está tudo ok :

<pre class="lang:sh decode:true">/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg</pre><figure id="attachment_366" aria-describedby="caption-attachment-366" style="width: 717px" class="wp-caption alignnone">

<img class="size-full wp-image-366" src="http://sidneiweber.com.br/wp-content/uploads/2017/01/Sele��o_006.png" alt="" width="717" height="350" srcset="https://sidneiweber.com.br/wp-content/uploads/2017/01/Sele��o_006.png 717w, https://sidneiweber.com.br/wp-content/uploads/2017/01/Sele��o_006-300x146.png 300w" sizes="(max-width: 717px) 100vw, 717px" /> <figcaption id="caption-attachment-366" class="wp-caption-text">0 erros</figcaption></figure> 

Caso não ocorra nenhum erro, podemos iniciar o serviço:

<pre class="lang:sh decode:true ">/usr/local/nagios/bin/nagios -d /usr/local/nagios/etc/nagios.cfg</pre>

Basta acessar pelo endereço IP/nagios (ip da máquina na qual foi instalado ou localhost se for local), com usuário nagiosadmin e a senha criada anteriormente. Segue um print do meu nagios com alguns hosts sendo monitorados e com uma interface diferente. Falaremos desses detalhes em outros posts.

<a href="https://sidneiweber.com.br/wp-content/uploads/2017/01/Sele��o_005.png" target="_blank" rel="noopener"><img class="alignnone wp-image-363 size-large" src="https://sidneiweber.com.br/wp-content/uploads/2017/01/Sele��o_005-1024x517.png" alt="" width="648" height="327" srcset="https://sidneiweber.com.br/wp-content/uploads/2017/01/Sele��o_005-1024x517.png 1024w, https://sidneiweber.com.br/wp-content/uploads/2017/01/Sele��o_005-300x151.png 300w, https://sidneiweber.com.br/wp-content/uploads/2017/01/Sele��o_005-768x388.png 768w, https://sidneiweber.com.br/wp-content/uploads/2017/01/Sele��o_005.png 1579w" sizes="(max-width: 648px) 100vw, 648px" /></a>