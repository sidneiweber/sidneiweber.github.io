---
id: 640
title: 'Comando fuser &#8211; Quem mexeu no meu arquivo'
date: 2018-11-06T09:28:53-03:00
author: Sidnei Weber
layout: post
image: /wp-content/fuser.png
guid: http://sidneiweber.com.br/?p=640
permalink: /comando-fuser-quem-mexeu-no-meu-arquivo/
wp_review_location:
  - bottom
wp_review_desc_title:
  - Resumo
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
wp_review_total:
  - "0"
wp_review_schema:
  - null
wp_review_rating_schema:
  - author
wp_review_show_schema_data:
  - "0"
wp_review_box_template:
  - default
categories:
  - Linux
---
O **fuser** é um programa que permite que saibamos qual processo está utilizando determinado arquivo, socket (portas) e sistema de arquivos especificado. Aprender sua manipulação é essencial para poder administrar um servidor para saber o que está acontecendo principalmente nas conexões. É um comando extremamente flexível, vamos ver suas opções e seu uso.

<table border="1" cellpadding="4" align="center">
  <tr>
    <th>
      Diretiva
    </th>

    <th>
      Descrição
    </th>

    <th colspan="2">
      Exemplo
    </th>
  </tr>

  <tr>
    <td>
      -a, &#8211;all
    </td>

    <td>
      Mostra todos os arquivos, inclusive os que estão sem uso
    </td>

    <td>
      <code># fuser -a *</code>
    </td>
  </tr>

  <tr>
    <td>
      -k, &#8211;kill
    </td>

    <td>
      Desativa/Mata os processos que estão utilizando determinado arquivo
    </td>

    <td>
      <code># fuser -k /home/zonebin</code>
    </td>
  </tr>

  <tr>
    <td>
      -i, &#8211;interactive
    </td>

    <td>
      Pede confirmação sempre que for matar um processo utilizando um arquivo
    </td>

    <td>
      <code># fuser -ik /home/zonebin</code>
    </td>
  </tr>

  <tr>
    <td>
      -m, &#8211;mount
    </td>

    <td>
      Especifica um sistema de arquivos para descobrir qual processo está sendo utilizado
    </td>

    <td>
      <code># fuser -m /dev/sda1</code>
    </td>
  </tr>

  <tr>
    <td>
      -s, &#8211;silent
    </td>

    <td>
      Realiza as operações indicadas silenciosamente, não use a opção -a, -u, -v
    </td>

    <td>
      <code># fuser -ks /home</code>
    </td>
  </tr>

  <tr>
    <td>
      -u, &#8211;user
    </td>

    <td>
      Mostra o nome de usuário que iniciou o processo que está utilizando o arquivo
    </td>

    <td>
      <code># fuser -u /var/log/messages</code>
    </td>
  </tr>

  <tr>
    <td>
      -4, &#8211;ipv4
    </td>

    <td>
      Mostra processos de IPV4 somente
    </td>

    <td>
      <code># fuser -4 ssh/tcp -6,</code>
    </td>
  </tr>

  <tr>
    <td>
      -ipv6
    </td>

    <td>
      Mostra somente processos de sockets IPV6
    </td>

    <td>
      <code># fuser -6 25/tcp</code>
    </td>
  </tr>
</table>

**Tipos de acesso:**  
c  Diretório atual  
e  Arquivo executável rodando  
f  Arquivo aberto (omitido no modo de display padrão)  
F  arquivo aberto para escrita (omitido no modo de display padrão)  
r  Diretório root  
m  Arquivo mapeado ou biblioteca compartilhada

**Exemplos:  
** Mostrar os processos em execução no diretório atual:**  
**

```shell
fuser -v .
```

Verificando se está sendo usado socket TCP ou UDP, como a porta 22 (SSH):

```shell
fuser -v -n tcp 22
```

Para mais informações:

```shell
man fuser
```
