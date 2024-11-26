# Remover Extensão .Php Com .Htaccess (Rápido E Fácil)

Já havia tentado de várias maneiras remover a extensão .php dos meus arquivos, mas todas sem sucesso. Porém consegui fazer de uma maneira muito simples, editando o arquivo .htaccess. Lembrando que para funcionar a modulo &#34;mod_rewrite&#34; deve estar habilitado no seu servidor web.

Criaremos o arquivo .htaccess na raiz do nosso projeto com o seguinte conteúdo

```
&lt;IfModule mod_rewrite.c&gt;
RewriteEngine on
RewriteCond %{REQUEST_FILENAME} !-d
RewriteCond %{REQUEST_FILENAME}.php -f
RewriteRule ^(.*)$ $1.php

&lt;/IfModule&gt;
```

E quando formos criarmos nosso link no php, aqui no caso estamos com o exemplo signup.php, basta digitar assim:

```html
&lt;a href=&#34;signup&#34;&gt;signup here&lt;/a&gt;
```

Sem a extensão .php. O servidor irá fazer todo o resto do trabalho.

[Fonte](http://www.codingcage.com/2015/11/how-to-remove-php-html-extensions-with.html)

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/remover-extensao-php-com-htaccess-rapido-e-facil/  

