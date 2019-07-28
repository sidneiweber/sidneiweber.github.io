---
id: 276
title: Reforçando segurança servidor ssh
date: 2016-11-23T10:07:22-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=276
permalink: /reforcando-seguranca-servidor-ssh/
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
wp_review_user_reviews:
  - "0"
wp_review_review_count:
  - "0"
image: /wp-content/uploads/2016/09/Artigo_07_002-220x162.jpg
categories:
  - Linux
  - Servidores
  - SSH
tags:
  - seguranca ssh
  - servidor ssh
---
<div id="toc_container" class="no_bullets">
  <p class="toc_title">
    P&aacute;gina de Posts
  </p>
  
  <ul class="toc_list">
    <li>
      <a href="#Introducao"><span class="toc_number toc_depth_1">1</span> Introdução</a>
    </li>
    <li>
      <a href="#Restricoes_de_acesso"><span class="toc_number toc_depth_1">2</span> Restrições de acesso</a>
    </li>
    <li>
      <a href="#Nao_permitir_acesso_direto_como_root"><span class="toc_number toc_depth_1">3</span> Não permitir acesso direto como root</a>
    </li>
    <li>
      <a href="#Modificar_porta_padrao"><span class="toc_number toc_depth_1">4</span> Modificar porta padrão</a>
    </li>
    <li>
      <a href="#Bloquear_ataques_de_forca_bruta_com_iptables"><span class="toc_number toc_depth_1">5</span> Bloquear ataques de força bruta com iptables</a>
    </li>
    <li>
      <a href="#Logando_com_chaves_de_criptografia"><span class="toc_number toc_depth_1">6</span> Logando com chaves de criptografia</a>
    </li>
    <li>
      <a href="#Desabilitar_autenticacao_por_senha"><span class="toc_number toc_depth_1">7</span> Desabilitar autenticação por senha</a>
    </li>
  </ul>
</div>

### <span id="Introducao">Introdução</span>

Nos dias de hoje é de suma importância proteger nossos servidores contra ataques e invasões. Nesse caso especifico do ssh é importante mantê-lo bem seguro pois é a nossa porta de entrada para o servidor, qualquer brecha pode causar uma catástrofe. Não devemos pensar que por ser um servidor de uma pequena empresa ou um <a href="https://www.melhorhospedagemdesites.com/servidor-vps/" target="_blank" rel="noopener">servidor VPS</a> que não devemos ter esse cuidado, hoje a informação disponível pode estar valendo muito. É uma questão de segurança básica que devemos estar atentos para não termos dores de cabeça e continuar com nossos servidores e serviços intactos.

### <span id="Restricoes_de_acesso">Restrições de acesso</span>

Caso queria restringir acesso somente a grupos ou usuários específicos, acrescentaremos ou editaremos as opções abaixo no arquivo de configuração do servidor ssh, o **/etc/ssh/sshd_config**. O mais correto ainda seria criar um grupo somente para acessos ssh.

<pre class="lang:default decode:true">AllowGroups sysadmin suporte

AllowUsers pedro juca</pre>

Podendo usar ou somente restrição por grupo ou somente restrição por usuário.

### <span id="Nao_permitir_acesso_direto_como_root">Não permitir acesso direto como root</span>

<pre class="lang:sh decode:true ">PermitRootLogin no</pre>

### <span id="Modificar_porta_padrao">Modificar porta padrão</span>

De preferência uma porta  com valor alto.

<pre class="lang:sh decode:true ">Port 2258</pre>

### <span id="Bloquear_ataques_de_forca_bruta_com_iptables">Bloquear ataques de força bruta com iptables</span>

<pre class="lang:sh decode:true ">iptables -I input -p tcp --dport 22 -i eth0 -m state --state NEW -m recent -set

iptables -I input -p tcp --dport 22 -i eth0 -m state --state NEW -m recent --update --seconds 60 --hitcount 4 -j DROP

iptables -A INPUT -P tcp --destination-port 22 -j ACCEPT</pre>

### <span id="Logando_com_chaves_de_criptografia">Logando com chaves de criptografia</span>

Gerar a chave

<pre class="lang:sh decode:true">ssh-keygen -b 1024 -t dsa</pre>

<img class="alignnone size-full wp-image-278" src="http://sidneiweber.com.br/wp-content/uploads/2016/09/Seleção_009.png" alt="selecao_009" width="595" height="386" srcset="https://sidneiweber.com.br/wp-content/uploads/2016/09/Seleção_009.png 595w, https://sidneiweber.com.br/wp-content/uploads/2016/09/Seleção_009-300x195.png 300w" sizes="(max-width: 595px) 100vw, 595px" /> 

Copiar para a outra máquina a chave pública

<pre class="lang:sh decode:true ">ssh-copy-id -i ~/.ssh/id_dsa.pub 192.168.1.100</pre>

<img class="alignnone size-full wp-image-279" src="http://sidneiweber.com.br/wp-content/uploads/2016/09/Seleção_010.png" alt="selecao_010" width="1052" height="188" srcset="https://sidneiweber.com.br/wp-content/uploads/2016/09/Seleção_010.png 1052w, https://sidneiweber.com.br/wp-content/uploads/2016/09/Seleção_010-300x54.png 300w, https://sidneiweber.com.br/wp-content/uploads/2016/09/Seleção_010-768x137.png 768w, https://sidneiweber.com.br/wp-content/uploads/2016/09/Seleção_010-1024x183.png 1024w" sizes="(max-width: 1052px) 100vw, 1052px" /> 

Verificar se o arquivo foi copiado para o destino em .ssh/authorized_keys e modificar a permissão para 600, por questões de segurança

### <span id="Desabilitar_autenticacao_por_senha">Desabilitar autenticação por senha</span>

<pre class="lang:sh decode:true ">PasswordAuthentication no</pre>

&nbsp;