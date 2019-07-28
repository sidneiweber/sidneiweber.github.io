---
id: 131
title: 'Instalar servidor Samba [Dica rápida]'
date: 2014-02-11T23:59:10-03:00
author: Sidnei Weber
layout: post
guid: http://sidiweber.wordpress.com/?p=131
permalink: /instalar-servidor-samba-dica-rapida/
categories:
  - Samba
  - Servidores
---
Primeiramente instalaremos o pacote:

<pre>apt-get install samba</pre>

Depois alteramos a configuração do arquivo:

<pre>vi /etc/samba/smb.conf</pre>

E alteramos alguns parametros:

<pre>[global]
#nome do grupo de trabalho
workgroup = casa
#como a maquina irá aparecer na rede Windows
netbios name = servidor de arquivos
#autenticação
#modo de acesso ao servidor
security = user / share
#lembrado que user é quando se criará um usuário no sistema, e share sem usuário

#compartilhamentos
[arquivos]
#descrição do compartilhamento
comment = meus arquivos
#caminho da pasta no servidor
path = /arquivos # ou o diretório desejado
public = yes
browseable = yes #se está visível ou oculto na rede
writeable = yes #permite escrita
read only = no #somente leitura
valid users = VOCE

# define a mascara em que os arquivos serão criados
create mask = 0700 #(terão a permissão rwx somente para o root)

# define a mascara em que os diretórios serão criados
directory mask = 0700</pre>

Vamos criar o diretório compartilhado no servidor:

<pre>mkdir /arquivos</pre>

Adicionando um usuário para acessar o Samba:

<pre>smbpasswd -a VOCE</pre>

Reinicie o serviço:

<pre>service smbd restart</pre>

Pronto, servidor disponível. <a href="http://cristianojosef.blogspot.com.br/2013/02/configurando-um-servidor-samba-no.html" target="_blank">Fonte</a>