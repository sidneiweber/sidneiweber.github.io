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
Bom hoje vamos seguir com nosso aprendizado em docker, já vimos sobre <a href="http://sidneiweber.com.br/2016/11/17/comandos-basicos-docker/" target="_blank">comandos básicos</a>, <a href="http://sidneiweber.com.br/2016/11/17/iniciando-servidor-apache-no-docker/" target="_blank" rel="noopener noreferrer">iniciar servidor apache</a>, <a href="http://sidneiweber.com.br/2016/11/18/exportar-e-importar-containers-no-docker/" target="_blank" rel="noopener noreferrer">exportar e importar containers</a> e agora a dica é bem simples porém muito útil. Toda vez que subimos um container sem colocar limites nos recursos, o container pode usar todo o recurso da máquina fisica, isso nem sempre é bom, seja por onerar o host ou mesmo para testes da sua aplicação. Então vamos as dicas.

Antes da dica, vamos a outra dica :), com o comando _**docker stats**_ podemos ver o consumo de nossos containers:

<img src="http://sidneiweber.com.br/wp-content/uploads/2017/06/Captura-de-tela_2017-06-13_13-47-34-1024x79.png" srcset="https://sidneiweber.com.br/wp-content/uploads/2017/06/Captura-de-tela_2017-06-13_13-47-34-1024x79.png 1024w, https://sidneiweber.com.br/wp-content/uploads/2017/06/Captura-de-tela_2017-06-13_13-47-34-300x23.png 300w, https://sidneiweber.com.br/wp-content/uploads/2017/06/Captura-de-tela_2017-06-13_13-47-34-768x59.png 768w, https://sidneiweber.com.br/wp-content/uploads/2017/06/Captura-de-tela_2017-06-13_13-47-34.png 1033w" />

Agora vamos as nossas dicas de hoje.

#### Limitar memória do container

```shell
# Para limitar a 512 MEGAS
docker run -it -m 512M ubuntu /bin/bash
#Para limitar a 1 GIGA
docker run -it -m 1G ubuntu /bin/bash
# Verificando a quantidade de memória
docker inspect [container id] |grep -i mem
```

#### Limitar CPU do container

```shell
docker run -it --cpu-shares 1024 ubuntu /bin/bash
docker inspect [container id] |grep -i cpu
```

### Atualizar limites de container em execução

#### Alterando limite de memória

```shell
docker update -m 256M [container id]
```

#### Atualizar limite CPU

```shell
docker update --cpu-shares 512 [container id]
```

Sempre lembrando que para pegar o id do container basta executar _**docker ps**_.
