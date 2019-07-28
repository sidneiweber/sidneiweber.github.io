---
id: 527
title: 'Rundeck &#8211; Automatizando suas tarefas'
date: 2018-04-09T21:08:17-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=527
permalink: /rundeck-automatizando-suas-tarefas/
wp_review_user_reviews:
  - "0"
wp_review_review_count:
  - "0"
image: /wp-content/uploads/2018/04/índice.png
categories:
  - Devops
---
O que é esse tal de Rundeck

Falando a grosso modo Rundeck é um automatizador e agendador de tarefas. Obviamente que ele faz muito mais do que isso, ele consegue rodar essas tarefas tanto em Linux quanto em Windows. Consegue-se criar um workflow de tarefas, fazendo uma tarefa depender de outra ou conforme sua execução com sucesso ou insucesso.

Escrito em java e tem sua administração por uma interface web bem simples de ser usado e usa ssh para conexões com Linux e Winrm para conexões com Windows. As configurações ficam salvas em arquivos, geralmente XML, tanto dos jobs (trabalhos) quanto dos nodes (hosts).

Tem uma grande vantagem pois não precisa de agentes rodando nas máquinas clientes e se consegue fazer uma verdadeira orquestração de jobs, podendo escolher se os jobs vão rodar em paralelo ou sequência e assim por diante. Se consegue criar chaves de acesso, ou chaves com senhas dentro do próprio dashboard.  
Existe uma integração com diversos serviços:

<img class="alignnone size-medium wp-image-545" src="http://sidneiweber.com.br/wp-content/uploads/2018/04/Captura-de-tela-de-2018-04-09-21-09-32-300x142.png" alt="" width="300" height="142" srcset="https://sidneiweber.com.br/wp-content/uploads/2018/04/Captura-de-tela-de-2018-04-09-21-09-32-300x142.png 300w, https://sidneiweber.com.br/wp-content/uploads/2018/04/Captura-de-tela-de-2018-04-09-21-09-32-768x364.png 768w, https://sidneiweber.com.br/wp-content/uploads/2018/04/Captura-de-tela-de-2018-04-09-21-09-32-1024x485.png 1024w, https://sidneiweber.com.br/wp-content/uploads/2018/04/Captura-de-tela-de-2018-04-09-21-09-32.png 1042w" sizes="(max-width: 300px) 100vw, 300px" />

Uma das poucas desvantagens que achei até o momento, que algumas configurações como de usuários, nodes, terem que ser feitas pela linha de comando editando diretamente os arquivos.

Para usar o Rundeck, precisamos ter instalado o java (1.8) em nosso servidor. Realizei alguns testes no Centos.

```shell
java -version

java version "1.8.0_131"
Java(TM) SE Runtime Environment (build 1.8.0_131-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.131-b11, mixed mode)
```

E instalaremos o rundeck adicionando o repositório.

```shell
rpm -Uvh http://repo.rundeck.org/latest.rpm
yum install rundeck
```

Após instalação ocorrer tudo bem, podemos conferir verificando a porta onde o serviço roda. Lembrando que caso tenha algum firewall ou bloqueio de portas o mesmo deve ser liberado.

```shell
netstat -an | egrep '4440|4443'
tcp46      0      0  *.4440                 *.*                    LISTEN
```

Agora basta acessarmos o IP do nosso servidor seguido da porta. Ex: http://localhost:4440 e usar a famosa senha de admin/admin

<img class="alignnone size-medium wp-image-542" src="http://sidneiweber.com.br/wp-content/uploads/2018/04/1DavE3K2jDhlyPljVdaeAeQ-300x300.png" alt="" width="300" height="300" srcset="https://sidneiweber.com.br/wp-content/uploads/2018/04/1DavE3K2jDhlyPljVdaeAeQ-300x300.png 300w, https://sidneiweber.com.br/wp-content/uploads/2018/04/1DavE3K2jDhlyPljVdaeAeQ-150x150.png 150w, https://sidneiweber.com.br/wp-content/uploads/2018/04/1DavE3K2jDhlyPljVdaeAeQ-65x65.png 65w, https://sidneiweber.com.br/wp-content/uploads/2018/04/1DavE3K2jDhlyPljVdaeAeQ-60x60.png 60w, https://sidneiweber.com.br/wp-content/uploads/2018/04/1DavE3K2jDhlyPljVdaeAeQ.png 500w" sizes="(max-width: 300px) 100vw, 300px" />

Bom de momento vamos ficar somente com a instalação, nos próximos artigos vamos aprender a cadastrar nodes, executar comandos, scripts e demais coisas que essa baita ferramenta disponibiliza.

Site: <a href="http://rundeck.org/" target="_blank">http://rundeck.org/</a>
