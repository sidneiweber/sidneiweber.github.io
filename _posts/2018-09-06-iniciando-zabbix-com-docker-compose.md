---
id: 644
title: Iniciando Zabbix com Docker Compose
date: 2018-09-06T23:16:18-03:00
author: Sidnei Weber
layout: post
permalink: /iniciando-zabbix-com-docker-compose/
img: /uploads/2017/10/zabbix.png
categories:
  - Zabbix
---
Obviamente precisaremos ter instalado o docker e docker-compose, caso não saiba como instalar pode acessar o <a href="https://docs.docker.com/install/" target="_blank" rel="noopener">link</a> e esse outro <a href="https://docs.docker.com/compose/install/" target="_blank">link</a> . Precisaremos criar um arquivo **docker-compose.yml** com o seguinte conteúdo:

```yaml
persistentDB:
  img "busybox:latest"
  volumes:
    - /var/lib/mysql
zabbixDB:
  img "monitoringartist/zabbix-db-mariadb"
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
  img "monitoringartist/zabbix-3.0-xxl:latest"
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
