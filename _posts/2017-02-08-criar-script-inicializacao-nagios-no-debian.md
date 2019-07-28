---
id: 377
title: Criar script inicialização Nagios no Debian
date: 2017-02-08T14:17:09-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=377
permalink: /criar-script-inicializacao-nagios-no-debian/
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
image: /wp-content/uploads/2017/01/nagios_logo_black.png
categories:
  - Nagios
---
Após a instalação e inicialização do Nagios no nosso servidor Debian, temos que configurar um script de inicialização, para que cada vez que a gente precisa reiniciar o serviço ou a própria máquina não precisaremos subir tudo na mão.

A primeira coisa é deletar o script já existente, lembrando que esse tutorial é válido para o Debian.

<pre class="lang:default decode:true ">rm -rf /etc/init.d/nagios</pre>

Copiar um esqueleto do sistema:

<pre class="lang:default decode:true">cp /etc/init.d/skeleton /etc/init.d/nagios</pre>

Vamos editar o arquivo /etc/init.d/nagios e colocar o seguinte conteúdo. Lembrando de remover ou comentar as duas linhas existentes no final do arquivo.

<pre class="lang:sh decode:true"># DESC="Description of the service"
# DAEMON=/usr/sbin/daemonexecutablename

DESC="Nagios"
NAME=nagios
DAEMON=/usr/local/nagios/bin/$NAME
DAEMON_ARGS="-d /usr/local/nagios/etc/nagios.cfg"
PROFILE=/usr/local/nagios/var/$NAME.lock</pre>

Dar as permissões para execução:

<pre class="lang:default decode:true ">chmod 755 nagios</pre>

E inicializar o serviço para subir junto com o sistema, quando o servidor for ligado:

<pre class="lang:sh decode:true ">update-rc.d nagios defaults</pre>

Agora temos todas as opções disponíveis:

<pre class="lang:sh decode:true ">root@nagios-server:/usr/local/nagios/etc/network# /etc/init.d/nagios
Usage: /etc/init.d/nagios {start|stop|status|restart|try-restart|force-reload}
root@nagios-server:/usr/local/nagios/etc/network# 
</pre>

Forte abraço e até a próxima.