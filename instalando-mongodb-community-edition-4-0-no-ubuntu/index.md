# Instalando MongoDB Community Edition 4.0 No Ubuntu


### &lt;span id=&#34;O_que_e_MongoDB&#34;&gt;O que é MongoDB&lt;/span&gt;

O MongoDB é um banco de dados NoSQL orientado a documentos de alto desempenho (sistema noSQL significa que ele não fornece tabelas, linhas, etc.). Ele armazena dados em documentos semelhantes a JSON com esquemas dinâmicos para melhor desempenho.

### &lt;span id=&#34;Adicionando_repositorios&#34;&gt;Adicionando repositórios&lt;/span&gt;

Para instalar **MongoDB Community Edition** no Ubuntu, precisamos primeiro importar a chave pública usada pelo gerenciador de pacotes.

```shell
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
```

No Ubuntu 18.04

```shell
echo &#34;deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu bionic/mongodb-org/4.0 multiverse&#34; | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
sudo apt-get update
```

No Ubuntu 16.04

```shell
echo &#34;deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.0 multiverse&#34; | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
sudo apt-get update
```

No Ubuntu 14.04

```shell
echo &#34;deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/4.0 multiverse&#34; | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
sudo apt-get update
```

### &lt;span id=&#34;Instalando_o_pacote&#34;&gt;Instalando o pacote&lt;/span&gt;

```shell
sudo apt-get install -y mongodb-org
```

### &lt;span id=&#34;Habilitando_e_iniciando_servico&#34;&gt;Habilitando e iniciando serviço&lt;/span&gt;

```shell
systemctl enable mongod.service
systemctl start mongod.service
```

E pronto já podemos usar no mongo, lembrando que é necessário liberar a porta 27017 no firewall caso o mesmo esteja habilitado. Nos próximos posts falaremos um pouco mais sobre o mongo.


---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/instalando-mongodb-community-edition-4-0-no-ubuntu/  

