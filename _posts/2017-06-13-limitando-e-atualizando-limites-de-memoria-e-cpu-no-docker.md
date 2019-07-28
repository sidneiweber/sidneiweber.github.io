---
id: 451
title: Limitando e atualizando limites de memória e CPU no docker
date: 2017-06-13T13:55:20-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=451
permalink: /limitando-e-atualizando-limites-de-memoria-e-cpu-no-docker/
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
  - Docker
---
Bom hoje vamos seguir com nosso aprendizado em docker, já vimos sobre <a href="http://sidneiweber.com.br/2016/11/17/comandos-basicos-docker/" target="_blank" rel="noopener noreferrer">comandos básicos</a>, <a href="http://sidneiweber.com.br/2016/11/17/iniciando-servidor-apache-no-docker/" target="_blank" rel="noopener noreferrer">iniciar servidor apache</a>, <a href="http://sidneiweber.com.br/2016/11/18/exportar-e-importar-containers-no-docker/" target="_blank" rel="noopener noreferrer">exportar e importar containers</a> e agora a dica é bem simples porém muito útil. Toda vez que subimos um container sem colocar limites nos recursos, o container pode usar todo o recurso da máquina fisica, isso nem sempre é bom, seja por onerar o host ou mesmo para testes da sua aplicação. Então vamos as dicas.

Antes da dica, vamos a outra dica :), com o comando _**docker stats**_ podemos ver o consumo de nossos containers:

<img class="alignnone size-large wp-image-452" src="http://sidneiweber.com.br/wp-content/uploads/2017/06/Captura-de-tela_2017-06-13_13-47-34-1024x79.png" alt="" width="648" height="50" srcset="https://sidneiweber.com.br/wp-content/uploads/2017/06/Captura-de-tela_2017-06-13_13-47-34-1024x79.png 1024w, https://sidneiweber.com.br/wp-content/uploads/2017/06/Captura-de-tela_2017-06-13_13-47-34-300x23.png 300w, https://sidneiweber.com.br/wp-content/uploads/2017/06/Captura-de-tela_2017-06-13_13-47-34-768x59.png 768w, https://sidneiweber.com.br/wp-content/uploads/2017/06/Captura-de-tela_2017-06-13_13-47-34.png 1033w" sizes="(max-width: 648px) 100vw, 648px" /> 

Agora vamos as nossas dicas de hoje.

<div id="toc_container" class="no_bullets">
  <p class="toc_title">
    P&aacute;gina de Posts
  </p>
  
  <ul class="toc_list">
    <ul>
      <li>
        <a href="#Limitar_memoria_do_container"><span class="toc_number toc_depth_2">0.1</span> Limitar memória do container</a>
      </li>
      <li>
        <a href="#Limitar_CPU_do_container"><span class="toc_number toc_depth_2">0.2</span> Limitar CPU do container</a>
      </li>
    </ul></li>
    
    <li>
      <a href="#Atualizar_limites_de_container_em_execucao"><span class="toc_number toc_depth_1">1</span> Atualizar limites de container em execução</a><ul>
        <li>
          <a href="#Alterando_limite_de_memoria"><span class="toc_number toc_depth_2">1.1</span> Alterando limite de memória</a>
        </li>
        <li>
          <a href="#Atualizar_limite_CPU"><span class="toc_number toc_depth_2">1.2</span> Atualizar limite CPU</a>
        </li>
      </ul>
    </li>
  </ul>
</div>

#### <span id="Limitar_memoria_do_container">Limitar memória do container</span>

<pre class="lang:sh decode:true"># Para limitar a 512 MEGAS
docker run -it -m 512M ubuntu /bin/bash
#Para limitar a 1 GIGA
docker run -it -m 1G ubuntu /bin/bash
# Verificando a quantidade de memória
docker inspect [container id] |grep -i mem</pre>

#### <span id="Limitar_CPU_do_container">Limitar CPU do container</span>

<pre class="lang:sh decode:true ">docker run -it --cpu-shares 1024 ubuntu /bin/bash
docker inspect [container id] |grep -i cpu</pre>

### <span id="Atualizar_limites_de_container_em_execucao">Atualizar limites de container em execução</span>

#### <span id="Alterando_limite_de_memoria">Alterando limite de memória</span>

<pre class="lang:default decode:true">docker update -m 256M [container id]</pre>

#### <span id="Atualizar_limite_CPU">Atualizar limite CPU</span>

<pre class="lang:default decode:true ">docker update --cpu-shares 512 [container id]</pre>

Sempre lembrando que para pegar o id do container basta executar _**docker ps**_.