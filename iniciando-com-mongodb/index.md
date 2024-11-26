# Iniciando Com MongoDB

Após termos realizado a instalação do MongoDB [nesse post](https://sidneiweber.com.br/2019/03/08/instalando-mongodb-community-edition-4-0-no-ubuntu/), hoje vamos iniciar com os primeiros passos com nosso banco de dados.

### Utilizando o Mongo Shell

Quando estamos utilizando o mongo em localhost (127.0.0.1) não é necessário usuário e senha para realizar a conexão.

```shell
$mongo
MongoDB shell version v4.0.6
connecting to: mongodb://127.0.0.1:27017/?gssapiServiceName=mongodb
Implicit session: session { &#34;id&#34; : UUID(&#34;319f1942-5755-4448-a5a5-282acf77ed6d&#34;) }
MongoDB server version: 4.0.6
```

Primeiro comando a ser usado é o **use,** utilizado para selecionar o banco usado.

```shell
$use usuarios
switched to db usuarios
```

Método **insert( )** para armazenar um documento contendo as chaves &#34;name&#34; e &#34;idade&#34;. As informações são armazenadas na estrutura, chave/valor, similar ao JSON.

```shell
db.usuarios.insert({ name: &#34;Sidnei&#34;, idade: 31} )
WriteResult({ &#34;nInserted&#34; : 1 })
```

No comando db.**usuarios**.insert, esse usuários corresponde a uma coleção, e ela não precisa de uma estrutura definida, podendo ser dinâmica caso haja necessidade. Podemos usar o comando abaixo sem alterar nenhum tipo de definição de estrutura que o insert irá funcionar normalmente.

```shell
db.usuarios.insert({ name: &#34;Sidnei&#34;, idade: 31, cidade: &#34;Sapiranga&#34; })
WriteResult({ &#34;nInserted&#34; : 1 })
```

Use o método **find( )** para visualizar os documentos inseridos. Vamos buscar o que foi salvo na coleção **usuarios**:

```shell
db.getCollection(&#39;usuarios&#39;).find({})
{ &#34;_id&#34; : ObjectId(&#34;5ca3bbb7719bb01a6641f7cb&#34;), &#34;name&#34; : &#34;Sidnei&#34;, &#34;idade&#34; : 31 }
{ &#34;_id&#34; : ObjectId(&#34;5ca3bd99719bb01a6641f7cc&#34;), &#34;name&#34; : &#34;Sidnei&#34;, &#34;idade&#34; : 31, &#34;cidade&#34; : &#34;Sapiranga&#34; }
```

Essa pesquisa também pode ser aprofundada, por exemplo pesquisando só quem está na cidade &#34;Sapiranga&#34;

```shell
db.getCollection(&#39;usuarios&#39;).find({cidade:&#34;Sapiranga&#34;})
{ &#34;_id&#34; : ObjectId(&#34;5ca3bd99719bb01a6641f7cc&#34;), &#34;name&#34; : &#34;Sidnei&#34;, &#34;idade&#34; : 31, &#34;cidade&#34; : &#34;Sapiranga&#34; }
```

E para sairmos do nosso shell basta executar o comando:

```shell
$exit
bye
```

Para o início está de bom tamanho, até a próxima.


---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/iniciando-com-mongodb/  

