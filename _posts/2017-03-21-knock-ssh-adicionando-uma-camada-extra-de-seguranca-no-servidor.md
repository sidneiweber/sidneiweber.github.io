---
layout: post
title: Knock SSH - Adicionando uma camada extra de segurança no servidor
id: 411
date: '2017-03-21 16:03:09 -0300'
author: Sidnei Weber
guid: http://sidneiweber.com.br/?p=411
permalink: "/knock-ssh-adicionando-uma-camada-extra-de-seguranca-no-servidor/"
wp_review_location:
- bottom
wp_review_desc_title:
- Resumo
wp_review_color:
- "#1e73be"
wp_review_fontcolor:
- "#555555"
wp_review_bgcolor1:
- "#e7e7e7"
wp_review_bgcolor2:
- "#ffffff"
wp_review_bordercolor:
- "#e7e7e7"
wp_review_user_review_type:
- star
wp_review_user_reviews:
- 0
wp_review_review_count:
- 0
image: "/wp-content/uploads/2017/03/Sele��o_008.png"
categories:
- Servidores
- SSH
tags:
- knock ssh
- port ssh
- ssh knock
---

Hoje vamos falar do **Knock,** uma ferramenta muito interessante para quem precisar acessar seus servidores remotamente. Bom o que o Knock faz, ele adiciona essa camada a mais da seguinte forma, por exemplo se acessamos nosso servidor pela porta 22 do ssh ela deveria estar liberada. Porém com Knock ela pode estar bloqueada, você acertando uma sequência específica de portas ele irá liberar a porta 22, e somente se acertar a sequencia definida.

### No servidor

Precisamos instalar somente um pacote em nosso servidor:

<pre class="lang:default decode:true ">apt-get install knockd</pre>

O arquivo de configuração fica no **_/etc/knockd.conf._** Eis a configuração padrão que veio no Debian.

<img class="alignnone size-full wp-image-412" src="http://sidneiweber.com.br/wp-content/uploads/2017/03/Sele��o_007.png" alt="" width="722" height="402" srcset="https://sidneiweber.com.br/wp-content/uploads/2017/03/Sele��o_007.png 722w, https://sidneiweber.com.br/wp-content/uploads/2017/03/Sele��o_007-300x167.png 300w" sizes="(max-width: 722px) 100vw, 722px" /> 

Eu alterei para a configuração ficar como no exemplo abaixo, sempre colocando a regra de ACCEPT na primeira linha, pois caso tenha sido bloqueada e seja adiciona no final do arquivo a regra não funcionará.

<pre class="lang:default decode:true">[options]
        UseSyslog

[openSSH]
        sequence    = 7000,8000,9000
        seq_timeout = 5
        command     = /sbin/iptables -I INPUT 1 -s %IP% -p tcp --dport 22 -j ACCEPT
        tcpflags    = syn

[closeSSH]
        sequence    = 9000,8000,7000
        seq_timeout = 5
        command     = /sbin/iptables -D INPUT -s %IP% -p tcp --dport 22 -j ACCEPT
        tcpflags    = syn</pre>

&nbsp;

Após editaremos o arquivo **_/etc/default/knockd_** para especificar nossa placa de rede:

<pre class="lang:default decode:true ">START_KNOCKD=1
KNOCKD_OPTS="-i enp0s3"</pre>

Feito a configuração reiniciaremos o serviço:

<pre class="lang:default decode:true ">/etc/init.d/knockd restart</pre>

Caso não tenha a porta 22 fechada, vamos fecha-lá. Lembrando que isso deve estar no script firewall do seu servidor.

<pre class="lang:default decode:true ">iptables -A INPUT -p tcp --dport 22 -j DROP</pre>

### No cliente

No cliente instalaremos o mesmo utilitário, porém sem precisar fazer as configurações feitas anteriormente.

<pre class="lang:default decode:true ">aptitude install knockd</pre>

Agora vamos bater nas portas em sequência conforme configurado no nosso servidor (7000, 8000, 9000)

<pre class="lang:default decode:true ">knock 10.0.0.106 7000:tcp 8000:tcp 9000:tcp</pre>

Com as batidas corretamente executadas, podemos verificar o log do nosso servidor e veremos que o foi passado por 3 estágios e após os mesmos estarem corretos, nosso porta 22 foi liberada pelo firewall

<pre class="lang:default decode:true ">Mar 21 15:49:21 server knockd: starting up, listening on enp0s3
Mar 21 15:49:26 server knockd: 10.0.0.103: openSSH: Stage 1
Mar 21 15:49:26 server knockd: 10.0.0.103: openSSH: Stage 2
Mar 21 15:49:26 server knockd: 10.0.0.103: openSSH: Stage 3
Mar 21 15:49:26 server knockd: 10.0.0.103: openSSH: OPEN SESAME
Mar 21 15:49:26 server knockd: openSSH: running command: /sbin/iptables -I INPUT 1 -s 10.0.0.103 -p tcp --dport 22 -j ACCEPT</pre>

E assim podemos conectar normalmente sem bloqueio nenhum.

<pre class="lang:default decode:true">root@black:/home/sidnei# ssh sidnei@10.0.0.106
sidnei@10.0.0.106's password:</pre>

### Fechando a porta

Depois de fazer tudo que era necessário podemos fechar a porta novamente, acertando a sequência de fechamento que também é incluida no nosso arquivo de configuração do servidor.

<pre class="lang:default decode:true ">knock 10.0.0.106 9000:tcp 8000:tcp 7000:tcp</pre>

E a porta será fechada novamente conforme o log nos informa:

<pre class="lang:default decode:true ">Mar 21 15:58:27 server knockd: 10.0.0.103: closeSSH: Stage 1
Mar 21 15:58:27 server knockd: 10.0.0.103: closeSSH: Stage 2
Mar 21 15:58:27 server knockd: 10.0.0.103: closeSSH: Stage 3
Mar 21 15:58:27 server knockd: 10.0.0.103: closeSSH: OPEN SESAME
Mar 21 15:58:27 server knockd: closeSSH: running command: /sbin/iptables -D INPUT -s 10.0.0.103 -p tcp --dport 22 -j ACCEPT</pre>

E era isso, acredito que seja uma camada bem interessante para nossos servidores e o mais importante, não colocando portas padrões na configuração, será muito mais dificil acertar a sequência para poder liberar o ssh.

<a href="https://www.vivaolinux.com.br/artigo/KNOCK-+-SSH?pagina=1" target="_blank">Fonte</a>

Um forte abraço
