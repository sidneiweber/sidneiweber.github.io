---
id: 295
title: Comandos básicos Docker
date: 2016-11-17T10:33:43-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=295
permalink: /comandos-basicos-docker/
img: /uploads/2016/11/índice-220x159.png
categories:
  - Docker
  - Servidores
---
Docker é um ferramenta que venha aprendendo a pouco tempo, não explicarei o que é o docker, apenas alguns detalhes no uso. Caso queira uma explicação melhor sobre o que é docker, recomendo esse <a href="http://www.mundodocker.com.br/o-que-e-docker/" target="_blank">artigo do Mundo Docker</a>.

Segue abaixo alista dos comandos mais básicos e explicações básicas sobre o docker:

```shell
docker search ubuntu # Procura versões do sistema ubuntu
docker pull [nome da imagem] # baixar imagem
docker images # listar imagens
docker run [nome da imagem ou id] # iniciar container com a imagem baixada
docker ps # listar containers
docker ps -a # Verifica todos os containers, inclusive os que estão parados
docker exec [id do container] [comando] # executa comandos no container
docker rm [id do container]
```

Iniciar container com alguns detalhes a mais:

<pre class="lang:sh decode:true">docker run -it -p &lt;porta_host&gt;:&lt;porta_container&gt; --name &lt;nome_container&gt; &lt;nome_imagem&gt;</pre>

<p class="aLF-aPX-K0-aPE aLF-aPX-aLK-ayr-auR ">
  Sendo que o -i significa interatividade e o -t que queremos um link com o terminal do container.
</p>

Iniciar uma sessão bash em um container que já esteja rodando:

<pre class="lang:default decode:true ">docker exec -it &lt;nome_container&gt; bash</pre>

Verificar os logs de um container:

<pre class="lang:default decode:true ">docker logs &lt;nome_container&gt;</pre>

Remover todos os containers parados:

<pre class="lang:sh decode:true">docker rm -f $(docker ps -a -q)</pre>

Remover uma imagem baixada:

<pre class="lang:default decode:true ">docker rmi -f &lt;nome_imagem&gt;</pre>

Copiar um arquivo do container para o host:

<pre class="lang:default decode:true ">docker cp &lt;nome_container&gt;:/caminho/no/container /caminho/no/host</pre>

<div id="toc_container" class="no_bullets">
  <p class="toc_title">
    P&aacute;gina de Posts
  </p>
  
  <ul class="toc_list">
    <li>
      <a href="#Salvando_alteracoes_de_um_container_modificado"><span class="toc_number toc_depth_1">1</span> Salvando alterações de um container modificado</a>
    </li>
    <li>
      <a href="#Dockerfile"><span class="toc_number toc_depth_1">2</span> Dockerfile</a><ul>
        <li>
          <ul>
            <li>
              <a href="#FROM"><span class="toc_number toc_depth_3">2.0.1</span> FROM</a>
            </li>
            <li>
              <a href="#MAINTAINER"><span class="toc_number toc_depth_3">2.0.2</span> MAINTAINER</a>
            </li>
            <li>
              <a href="#RUN"><span class="toc_number toc_depth_3">2.0.3</span> RUN </a>
            </li>
            <li>
              <a href="#ENV"><span class="toc_number toc_depth_3">2.0.4</span> ENV</a>
            </li>
            <li>
              <a href="#EXPOSE"><span class="toc_number toc_depth_3">2.0.5</span> EXPOSE</a>
            </li>
            <li>
              <a href="#ADD"><span class="toc_number toc_depth_3">2.0.6</span> ADD</a>
            </li>
            <li>
              <a href="#ENTRYPOINT"><span class="toc_number toc_depth_3">2.0.7</span> ENTRYPOINT</a>
            </li>
            <li>
              <a href="#CMD"><span class="toc_number toc_depth_3">2.0.8</span> CMD</a>
            </li>
            <li>
              <a href="#Exemplo_de_dockerfile"><span class="toc_number toc_depth_3">2.0.9</span> Exemplo de dockerfile</a>
            </li>
          </ul>
        </li>
      </ul>
    </li>
  </ul>
</div>

## <span id="Salvando_alteracoes_de_um_container_modificado">Salvando alterações de um container modificado</span>

Após instalar alguns programas ou fazer modificações no seu container, é possível que queira salvá-lo para não perder essas alterações. Para isso existe a opção _commit_ do docker que irá gerar uma nova imagem do seu container com as alterações. Pegaremos como base o ID do nosso container:

<pre class="lang:sh decode:true ">root@black:/home/sidnei# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                  NAMES
f8d74ee7155a        7e616530e7ea        "/bin/bash"         12 minutes ago      Up 12 minutes       0.0.0.0:8080-&gt;80/tcp   lonely_mccarthy
root@black:/home/sidnei#</pre>

Com nosso ID em mãos faremos o commit:

<pre class="lang:sh decode:true ">root@black:/home/sidnei# docker commit f8d74ee7155a debian-apache
sha256:9a232ff09aaf601dfbe487c3b20802079cd5e1a55115fb3a47473f9e44ab8bf0
root@black:/home/sidnei# docker images
REPOSITORY            TAG                 IMAGE ID            CREATED             SIZE
debian-apache         latest              9a232ff09aaf        4 seconds ago       226.9 MB
</pre>

## <span id="Dockerfile">Dockerfile</span>

Um Dockerfile é um script que automatiza a criação de imagens docker. Veja alguns exemplos de comandos que podem ser utilizados no Dockerfile. Em outros posts trarei com mais detalhes como cada um funciona.

#### <span id="FROM"><strong>FROM</strong></span> {.aLF-aPX-K0-aPE.aLF-aPX-aLK-ayr-auR}

<p class="aLF-aPX-K0-aPE aLF-aPX-aLK-ayr-auR ">
  Primeira instrução, define a imagem base.
</p>

<pre class="lang:default decode:true ">FROM ubuntu14:04</pre>

#### <span id="MAINTAINER"><strong>MAINTAINER</strong></span> {.aLF-aPX-K0-aPE.aLF-aPX-aLK-ayr-auR}

<p class="aLF-aPX-K0-aPE aLF-aPX-aLK-ayr-auR ">
  Especifica o autor da imagem.
</p>

<pre class="lang:default decode:true ">MAINTAINER Foo foo@bar.com</pre>

#### <span id="RUN"><strong>RUN </strong></span> {.aLF-aPX-K0-aPE.aLF-aPX-aLK-ayr-auR}

<p class="aLF-aPX-K0-aPE aLF-aPX-aLK-ayr-auR ">
  Equivalente ao comando docker run.
</p>

<pre class="lang:default decode:true ">RUN apt-get install python</pre>

#### <span id="ENV"><strong>ENV</strong></span> {.aLF-aPX-K0-aPE.aLF-aPX-aLK-ayr-auR}

<p class="aLF-aPX-K0-aPE aLF-aPX-aLK-ayr-auR ">
  Define uma variável de ambiente.
</p>

<pre class="lang:default decode:true ">ENV PORT=8000</pre>

#### <span id="EXPOSE"><strong>EXPOSE</strong></span> {.aLF-aPX-K0-aPE.aLF-aPX-aLK-ayr-auR}

<p class="aLF-aPX-K0-aPE aLF-aPX-aLK-ayr-auR ">
  Expõe portas.
</p>

<pre class="lang:default decode:true ">EXPOSE 8000</pre>

#### <span id="ADD"><strong>ADD</strong></span> {.aLF-aPX-K0-aPE.aLF-aPX-aLK-ayr-auR}

<p class="aLF-aPX-K0-aPE aLF-aPX-aLK-ayr-auR ">
  Copia arquivos do host hospedeiro para dentro da imagem.
</p>

<pre class="lang:default decode:true ">ADD foo.txt /bar/foo.txt</pre>

#### <span id="ENTRYPOINT"><strong>ENTRYPOINT</strong></span> {.aLF-aPX-K0-aPE.aLF-aPX-aLK-ayr-auR}

<p class="aLF-aPX-K0-aPE aLF-aPX-aLK-ayr-auR ">
  Permite que a imagem seja executada como uma aplicativo (a partir da linha de comando especificada).
</p>

<pre class="lang:default decode:true ">ENTRYPOINT ["python", "app.py"]</pre>

#### <span id="CMD"><strong>CMD</strong></span> {.aLF-aPX-K0-aPE.aLF-aPX-aLK-ayr-auR}

<p class="aLF-aPX-K0-aPE aLF-aPX-aLK-ayr-auR ">
  Comando que será executado quando a execução do container for acionada.
</p>

<pre class="lang:default decode:true">CMD ["supervisord"]</pre>

#### <span id="Exemplo_de_dockerfile">Exemplo de dockerfile</span>

<pre class="lang:sh decode:true">FROM debian:lastest

MAINTAINER Sidnei Weber &lt;sidnei.weber@gmal.com&gt;

RUN apt-get update
RUN apt-get install -y apache2
RUN /etc/init.d/apache2 start</pre>

Para gerar a imagem a partir do nosso dockerfile usaremos o docker build. Lembrando que se criamos o docker file em alguma pasta especifica, deveremos estar dentro desta pasta para executar o comando a seguir:

<pre class="lang:sh decode:true ">docker build -t teste .</pre>

Por hoje era isso pessoal, em breve estaremos estudando mais sobre o assunto.

Fonte: <a href="http://www.diego-garcia.info/2015/02/15/docker-por-onde-comecar/" target="_blank">Diego Garcia</a>