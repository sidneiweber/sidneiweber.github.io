---
id: 644
title: Iniciando Zabbix com Docker Compose
date: 2018-09-06T23:16:18-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=644
permalink: /iniciando-zabbix-com-docker-compose/
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
image: /wp-content/uploads/2017/10/zabbix.png
categories:
  - Zabbix
---
Obviamente precisaremos ter instalado o docker e docker-compose, caso não saiba como instalar pode acessar o <a href="https://docs.docker.com/install/" target="_blank" rel="noopener">link</a> e esse outro <a href="https://docs.docker.com/compose/install/" target="_blank">link</a> . Precisaremos criar um arquivo **docker-compose.yml** com o seguinte conteúdo:

```compose
persistentDB:
  image: "busybox:latest"
  volumes:
    - /var/lib/mysql
zabbixDB:
  image: "monitoringartist/zabbix-db-mariadb"
  environment:
    MARIADB_USER: zabbix
    MARIADB_PASS: senha
    PHP_date_timezone: America/Sao_Paulo
    ZS_StartDiscoverers: "5"
    ZS_StartPingers: "5"
  volumes_from:
    - persistentDB
  volumes:
    - "/etc/localtime:/etc/localtime:ro"
    - "/srv/zabbix/backups:/backups"
  hostname: zabbix-db
zabbix:
  image: "monitoringartist/zabbix-3.0-xxl:latest"
  ports:
    - "80:80"
    - "10051:10051"
  volumes:
    - "/etc/localtime:/etc/localtime:ro"
  links:
    - "zabbixDB:zabbix.db"
  environment:
    ZS_DBHost: zabbix.db
    ZS_DBUser: zabbix
    ZS_DBPassword: senha
    TERM: xterm
```

E iremos executar o seguinte comando:

```shell
docker-compose up -d
```

Caso queiram contribuir segue o github desse código: <a href="https://github.com/sidneiweber/zabbix-docker" target="_blank" rel="noopener">https://github.com/sidneiweber/zabbix-docker</a>
