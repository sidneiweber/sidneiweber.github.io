---
id: 248
title: Tutorial básico e rápido de Mysql
date: 2016-07-12T13:10:54-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=248
permalink: /tutorial-basico-e-rapido-de-mysql/
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
img: /uploads/2016/07/mysql_hosting-220x162.png
categories:
  - Mysql
tags:
  - mysql
---
<div id="toc_container" class="no_bullets">
  <p class="toc_title">
    P&aacute;gina de Posts
  </p>
  
  <ul class="toc_list">
    <li>
      <a href="#Instalacao"><span class="toc_number toc_depth_1">1</span> Instalação</a>
    </li>
    <li>
      <a href="#Administrando_via_linha_de_comando"><span class="toc_number toc_depth_1">2</span> Administrando via linha de comando</a>
    </li>
    <li>
      <a href="#Comandos_de_uso_basico"><span class="toc_number toc_depth_1">3</span> Comandos de uso básico</a>
    </li>
    <li>
      <a href="#Exportar_e_importar_via_linha_de_comando"><span class="toc_number toc_depth_1">4</span> Exportar e importar via linha de comando</a>
    </li>
  </ul>
</div>

## <span id="Instalacao">Instalação</span>

Começamos pela instalação, que nas distribuições Debian like seria:

<pre class="lang:sh decode:true">sudo apt-get install mysql-server phpmyadmin</pre>

Esse comando instalará a última versão do Mysql e do administrador visual que mais gosto o PHPmyadmin. A instalação irá pedir uma senha para o usuário padrão (root):

<img class="alignnone size-full wp-image-257" src="/assets/img/uploads/2016/07/Seleção_003.png" alt="Seleção_003" width="719" height="401" srcset="https://sidneiweber.com.br/assets/img/uploads/2016/07/Seleção_003.png 719w, https://sidneiweber.com.br/assets/img/uploads/2016/07/Seleção_003-300x167.png 300w" sizes="(max-width: 719px) 100vw, 719px" /> 

A confirmação da senha:

<img class="alignnone size-full wp-image-259" src="/assets/img/uploads/2016/07/Seleção_004.png" alt="Seleção_004" width="713" height="386" srcset="https://sidneiweber.com.br/assets/img/uploads/2016/07/Seleção_004.png 713w, https://sidneiweber.com.br/assets/img/uploads/2016/07/Seleção_004-300x162.png 300w" sizes="(max-width: 713px) 100vw, 713px" /> 

Em qual servidor web o Phpmyadmin irá rodar, no meu caso apache:

<img class="alignnone size-full wp-image-260" src="/assets/img/uploads/2016/07/Seleção_005.png" alt="Seleção_005" width="711" height="392" srcset="https://sidneiweber.com.br/assets/img/uploads/2016/07/Seleção_005.png 711w, https://sidneiweber.com.br/assets/img/uploads/2016/07/Seleção_005-300x165.png 300w" sizes="(max-width: 711px) 100vw, 711px" /> 

E diga não a próxima opção:

<img class="alignnone size-full wp-image-261" src="/assets/img/uploads/2016/07/Seleção_006.png" alt="Seleção_006" width="717" height="392" srcset="https://sidneiweber.com.br/assets/img/uploads/2016/07/Seleção_006.png 717w, https://sidneiweber.com.br/assets/img/uploads/2016/07/Seleção_006-300x164.png 300w" sizes="(max-width: 717px) 100vw, 717px" /> 

## <span id="Administrando_via_linha_de_comando">Administrando via linha de comando</span>

<pre class="lang:default decode:true">mysql -h host -u root -p (o super usuário default é root)</pre>

Assim terá acesso ao terminal do mysql.

## <span id="Comandos_de_uso_basico">Comandos de uso básico</span>

Para ter acesso a linha de comando mysql localhost, após o comando será solicitado a senha de admin do mysql

<pre class="lang:default decode:true">mysql -u root -p</pre>

Criar base de dados:

<pre class="lang:mysql decode:true">create database nomebanco;</pre>

Para editar o banco de dados:

<pre class="lang:mysql decode:true ">use nomebanco;</pre>

Criar tabela:

<pre class="lang:mysql decode:true ">create table nometabela(campos tipos...);

//Exemplo

CREATE TABLE usuario
(
id int,
nome varchar(255),
sobrenome varchar(255),
endereco varchar(255),
cidade varchar(255)
);</pre>

Mostrar conteudo da tabela:

<pre class="lang:mysql decode:true ">select * from nometabela;</pre>

Exibir bancos de dados:

<pre class="lang:mysql decode:true ">show databases;</pre>

Exibir tabelas:

<pre class="lang:mysql decode:true ">show tables;</pre>

Exibir informações das tabelas, a formação das informações:

<pre class="lang:mysql decode:true ">describe nometabela;</pre>

##<img class="alignnone size-full wp-image-269" src="/assets/img/uploads/2016/07/Seleção_007.png" alt="Seleção_007" width="555" height="202" srcset="https://sidneiweber.com.br/assets/img/uploads/2016/07/Seleção_007.png 555w, https://sidneiweber.com.br/assets/img/uploads/2016/07/Seleção_007-300x109.png 300w" sizes="(max-width: 555px) 100vw, 555px" /> 

## <span id="Exportar_e_importar_via_linha_de_comando">Exportar e importar via linha de comando</span>

Exportar

<pre class="lang:mysql decode:true ">mysqldump -u user -p passwd banco &gt; banco.sql</pre>

Importando:

<pre class="lang:mysql decode:true ">mysql -u user -p password banco &lt; banco.sql</pre>

Esse é o tutorial bem básico sobre o uso do mysql.