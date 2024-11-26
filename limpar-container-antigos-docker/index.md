# Limpar Container Antigos Docker

Caso sua lista de container esteja muito grande e queira remover alguns containers do seu host, podemos usar o comando abaixo para remover container parados a mais tempo:

```shell
docker ps --filter &#34;status=exited&#34; | grep &#39;weeks ago&#39; | awk &#39;{print $1}&#39; | xargs --no-run-if-empty docker rm
```

Explicando:

```shell
docker ps --filter &#34;status=exited&#34;
```
Lista somente os containers parados, que não estão em execução

```shell
grep &#39;weeks ago&#39;
```
Filtra por containers criados a semanas atrás

```shell
awk &#39;{print $1}&#39;
```
Exibe a primeira coluna, que refere ao CONTAINER ID

```shell
xargs --no-run-if-empty docker rm
```
Pega o que foi filtrado até agora e joga como parâmetro para o _docker rm_

Sempre use os comandos com muito cuidado caso não tenha certeza do que está fazendo, não me responsabilizo por qualquer erro humano ;).


---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/limpar-container-antigos-docker/  

