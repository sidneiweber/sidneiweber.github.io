# Utilizando o comando like com variável [PHP-MySQL]


```php
include("conexao.php");
$busca = $_POST['busca'];
// comando like com variavel
// retorna todos os produtos que tenham o valor da variável busca em qualquer posição
$result = mysql_query("SELECT descricao FROM produtos WHERE descricao like '%".$busca."%' ");

// comando like normal
//retorna todos os nomes que tenham a palavra "pedro" em qualquer posição
$result = mysql_query(" SELECT nome FROM funcionarios WHERE nome like '%pedro%' ");</pre>
```

---

> Author: Sidnei Weber  
> URL: https://sidneiweber.com.br/utilizando-o-comando-like-com-variavel-php-mysql/  

