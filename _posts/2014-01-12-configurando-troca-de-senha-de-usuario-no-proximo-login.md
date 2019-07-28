---
id: 107
title: Configurando troca de senha de usuário no próximo login
date: 2014-01-12T18:51:44-03:00
author: Sidnei Weber
layout: post
guid: http://sidiweber.wordpress.com/?p=107
permalink: /configurando-troca-de-senha-de-usuario-no-proximo-login/
categories:
  - Linux
---
Para isso, utilizaremos o comando chage. Antes, listamos as propriedades de login deste usuário: 

<pre># chage -l  </pre>

Exemplo: 

<pre># chage -l perm

  Última mudança de senha                              : Jan 07, 2014
  Senha expira                                         : nunca
  Senha inativa                                        : nunca
  Conta expira                                         : nunca
  Número mínimo de dias entre troca de senhas          : 0
  Número máximo de dias entre troca de senhas          : 99999
  Número de dias de avisos antes da expiração da senha : 7
</pre>

Como podemos visualizar, a senha deste usuário &#8220;nunca expira&#8221;. Então, forçaremos a expiração de senha para o próximo login que este usuário venha fazer, executando o comando a seguir: 

<pre># chage -d 0 perm </pre>

Fonte: <http://www.vivaolinux.com.br/dica/Configurando-troca-de-senha-de-usuario-no-proximo-login>