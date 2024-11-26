# Melhor Maneira De Converter Data Para Mysql [PHP]

Se você quer converter uma data vinda do MYSQL para o formato PT-BR use o seguinte comando:

```php
$data = implode(&#34;/&#34;,array_reverse(explode(&#34;-&#34;,$data)));
```

Assim vai converter a data do mysql para o formato brasileiro.

Ex: 2010-31-04 para 31/04/2010

Se você quer converter uma data em formato brasileiro para inserir no mysql use:

```php
$data = implode(&#34;-&#34;,array_reverse(explode(&#34;/&#34;,$data)));
```

O resultado será: 31/04/2010 para 2010-31-04

Fonte: &lt;http://www.l9web.com.br/blog/?p=68&gt;

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/melhor-maneira-de-converter-data-para-mysql-php/  

