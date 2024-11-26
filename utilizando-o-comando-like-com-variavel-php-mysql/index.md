# Utilizando O Comando Like Com Variável [PHP-MySQL]


```php
include(&#34;conexao.php&#34;);
$busca = $_POST[&#39;busca&#39;];
// comando like com variavel
// retorna todos os produtos que tenham o valor da variável busca em qualquer posição
$result = mysql_query(&#34;SELECT descricao FROM produtos WHERE descricao like &#39;%&#34;.$busca.&#34;%&#39; &#34;);

// comando like normal
//retorna todos os nomes que tenham a palavra &#34;pedro&#34; em qualquer posição
$result = mysql_query(&#34; SELECT nome FROM funcionarios WHERE nome like &#39;%pedro%&#39; &#34;);&lt;/pre&gt;
```

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/utilizando-o-comando-like-com-variavel-php-mysql/  

