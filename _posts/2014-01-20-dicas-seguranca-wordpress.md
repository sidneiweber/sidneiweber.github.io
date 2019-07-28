---
id: 109
title: Dicas segurança WordPress
date: 2014-01-20T22:38:07-03:00
author: Sidnei Weber
layout: post
guid: http://sidiweber.wordpress.com/?p=109
permalink: /dicas-seguranca-wordpress/
wp_review_user_reviews:
  - "0"
wp_review_review_count:
  - "0"
categories:
  - Wordpress
---
<div id="toc_container" class="no_bullets">
  <p class="toc_title">
    P&aacute;gina de Posts
  </p>
  
  <ul class="toc_list">
    <li>
      <a href="#Nao_divulgue_a_versao_do_seu_WordPress"><span class="toc_number toc_depth_1">1</span> Não divulgue a versão do seu WordPress</a>
    </li>
    <li>
      <a href="#Remocao_dos_arquivos_readmehtml_e_installphp"><span class="toc_number toc_depth_1">2</span> Remoção dos arquivos readme.html e install.php</a>
    </li>
    <li>
      <a href="#Remova_os_plugins_e_temas_que_nao_estao_sendo_utilizados"><span class="toc_number toc_depth_1">3</span> Remova os plugins e temas que não estão sendo utilizados</a>
    </li>
    <li>
      <a href="#Nao_use_o_login_padrao_do_Admin_do_WordPress"><span class="toc_number toc_depth_1">4</span> Não use o login padrão do Admin do WordPress</a>
    </li>
    <li>
      <a href="#Bloqueie_a_listagem_de_arquivos_em_suas_pastas"><span class="toc_number toc_depth_1">5</span> Bloqueie a listagem de arquivos em suas pastas</a>
    </li>
    <li>
      <a href="#Desabilite_o_WP_DEBUG"><span class="toc_number toc_depth_1">6</span> Desabilite o WP_DEBUG.</a>
    </li>
    <li>
      <a href="#Desabilite_o_registro_de_novos_usuarios"><span class="toc_number toc_depth_1">7</span> Desabilite o registro de novos usuários</a>
    </li>
  </ul>
</div>

### <span id="Nao_divulgue_a_versao_do_seu_WordPress">Não divulgue a versão do seu WordPress</span>

Esta informação fica localizadas no arquivo header.php de seu tema. Para desabilitar, remova a linha a seguir:

<pre>&lt;meta name="generator" content="WordPress &lt;?php bloginfo('version'); ?&gt;" /&gt;</pre>

Outra maneira de remover esta informação é adicionar o código abaixo ao seu arquivos functions.php:

<pre>&lt;?php remove_action(‘wp_head’, ‘wp_generator’); ?&gt;</pre>

### <span id="Remocao_dos_arquivos_readmehtml_e_installphp">Remoção dos arquivos readme.html e install.php</span>

### <span id="Remova_os_plugins_e_temas_que_nao_estao_sendo_utilizados">Remova os plugins e temas que não estão sendo utilizados</span>

### <span id="Nao_use_o_login_padrao_do_Admin_do_WordPress">Não use o login padrão do Admin do WordPress</span>

### <span id="Bloqueie_a_listagem_de_arquivos_em_suas_pastas">Bloqueie a listagem de arquivos em suas pastas</span>

Para impedir que os arquivos de suas pastas sejam listados, crie ou modifique o arquivo .htaccess (se seu site rodar em Linux) e inclua a seguinte linha:

<pre>Options All -Indexes</pre>

O arquivo deve estar na pasta principal (“/”) da instalação do WordPress juntamente com o arquivo wp-config.php.

### <span id="Desabilite_o_WP_DEBUG"><b>Desabilite o WP_DEBUG.</b></span>

A variável global WP\_DEBUG permite ao desenvolvedor, depurar a aplicação. Deixar estas informações visíveis também pode fornecer informações valiosas aos atacantes. Para desabilitar a variável WP\_DEBUG, edite o arquivo wp-config.php e altere de true para false.

<pre>define(‘WP_DEBUG’, false);</pre>

### <span id="Desabilite_o_registro_de_novos_usuarios">Desabilite o registro de novos usuários</span>

Ao fazer isso você impede que qualquer um tenha acesso ao painel de administração do site. Vá até a seção Geral e desmarque a opção Qualquer pessoa pode se registrar, ou simplesmente delete o arquivo wp-register.php

Este post, de maneira nenhuma tem o objetivo de ser um guia definitivo mas sim apenas um ponto de partida para aqueles que conhecem pouco de segurança no WordPress ou para complementar os conhecimentos daqueles que já aplicam técnicas para proteção de sites e blogs.

<a href="http://www.pcredesecia.com.br/2013/11/32-dicas-de-seguranca-para-wordpress.html" target="_blank">Fonte</a>