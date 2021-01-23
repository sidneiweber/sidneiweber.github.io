---
id: 446
title: Iniciando servidor web PHP e Mysql com Docker
date: 2017-05-31T13:41:27-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=446
permalink: /iniciando-servidor-web-php-e-mysql-com-docker/
img: /uploads/2017/05/Captura-de-tela_2017-05-31_13-34-26.png
tag: [docker, mysql, php, apache]
---
De uma maneira muito rápida podemos iniciar um servidor web para testarmos aplicações, páginas, sistemas, etc. Para isso precisaremos de duas ferramentas:

  * Docker
  * Docker Compose

Vou levar em consideração de já tenha os mesmos instalados, pois cada sistema tem seu próprio gerenciador de pacotes e não vou especificar isso no momento.

<div id="toc_container" class="no_bullets">
  <p class="toc_title">
    P&aacute;gina de Posts
  </p>
  
  <ul class="toc_list">
    <li>
      <a href="#Iniciando"><span class="toc_number toc_depth_1">1</span> Iniciando</a><ul>
        <li>
          <a href="#DockerFile"><span class="toc_number toc_depth_2">1.1</span> DockerFile</a>
        </li>
        <li>
          <a href="#Docker_Compose"><span class="toc_number toc_depth_2">1.2</span> Docker Compose</a>
        </li>
        <li>
          <a href="#Subindo_a_aplicacao"><span class="toc_number toc_depth_2">1.3</span> Subindo a aplicação</a>
        </li>
      </ul>
    </li>
  </ul>
</div>

### <span id="Iniciando">Iniciando</span>

#### <span id="DockerFile">DockerFile</span>

Para iniciar criaremos um Dockerfile, para quem não está muito familiarizado pode ver um <a href="http://sidneiweber.com.br/2016/11/17/comandos-basicos-docker/" target="_blank" rel="noopener noreferrer">post com comandos básico do docker aqui</a>. Usaremos uma imagem base do Docker Hub, a [tutum/lamp](https://hub.docker.com/r/tutum/lamp/).

<pre class="lang:default decode:true ">FROM tutum/lamp
MAINTAINER PAAS EMAIL &lt;email@site.com&gt;</pre>

#### <span id="Docker_Compose">Docker Compose</span>

Agora na mesma pasta iremos criar o arquivo **docker-compose.yml**. Com o conteúdo abaixo:

_Ps: Lembre de verificar se os caminhos dos arquivos estão corretos em seu sistema, pode variar de linux para linux._

<pre class="lang:default decode:true ">dev:
 
  dockerfile: Dockerfile
  volumes:
    - .:/var/www/html
    - /etc/timezone:/etc/timezone
    - /etc/localtime:/etc/localtime
 
  build: .
  expose:
    - "80"
 
  ports:
    - "80:80"</pre>

#### <span id="Subindo_a_aplicacao">Subindo a aplicação</span>

Subiremos a aplicação com o seguinte comando:

<pre class="lang:default decode:true ">docker-compose up</pre>

Basta acessar seu localhost, ou ip de sua máquina que o servidor estará UP. A pasta onde foi criado os arquivos anteriores será a pasta raíz do servidor web. Ao iniciar será gerado uma saída parecido com a abaixo:

<img class="alignnone size-large wp-image-447" src="/assets/img/uploads/2017/05/Captura-de-tela_2017-05-31_13-34-26-1024x233.png" alt="" width="648" height="147" /> 

<a href="http://blog.locaweb.com.br/artigos/desenvolvimento-artigos/docker-php-em-5-minutos/" target="_blank" rel="noopener noreferrer">Fonte</a>