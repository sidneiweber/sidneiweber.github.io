# Iniciando Zabbix Com Docker Compose

Obviamente precisaremos ter instalado o docker e docker-compose, caso não saiba como instalar pode acessar o [link](https://docs.docker.com/install/) e esse outro [link](https://docs.docker.com/compose/install/). Precisaremos criar um arquivo **docker-compose.yml** com o seguinte conteúdo:

```yaml
persistentDB:
  img &#34;busybox:latest&#34;
  volumes:
    - /var/lib/mysql
zabbixDB:
  img &#34;monitoringartist/zabbix-db-mariadb&#34;
  environment:
    MARIADB_USER: zabbix
    MARIADB_PASS: senha
    PHP_date_timezone: America/Sao_Paulo
    ZS_StartDiscoverers: &#34;5&#34;
    ZS_StartPingers: &#34;5&#34;
  volumes_from:
    - persistentDB
  volumes:
    - &#34;/etc/localtime:/etc/localtime:ro&#34;
    - &#34;/srv/zabbix/backups:/backups&#34;
  hostname: zabbix-db
zabbix:
  img &#34;monitoringartist/zabbix-3.0-xxl:latest&#34;
  ports:
    - &#34;80:80&#34;
    - &#34;10051:10051&#34;
  volumes:
    - &#34;/etc/localtime:/etc/localtime:ro&#34;
  links:
    - &#34;zabbixDB:zabbix.db&#34;
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

Caso queiram contribuir segue o github desse código: [https://github.com/sidneiweber/zabbix-docker](https://github.com/sidneiweber/zabbix-docker)


---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/iniciando-zabbix-com-docker-compose/  

