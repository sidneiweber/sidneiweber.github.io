# Dicas Segurança WordPress


### Não divulgue a versão do seu WordPress

Esta informação fica localizadas no arquivo header.php de seu tema. Para desabilitar, remova a linha a seguir:

```php
&lt;meta name=&#34;generator&#34; content=&#34;WordPress &lt;?php bloginfo(&#39;version&#39;); ?&gt;&#34; /&gt;
```

Outra maneira de remover esta informação é adicionar o código abaixo ao seu arquivos functions.php:

```php
&lt;pre&gt;&lt;?php remove_action(‘wp_head’, ‘wp_generator’); ?&gt;&lt;/pre&gt;
```

### Remoção dos arquivos readme.html e install.php

### Remova os plugins e temas que não estão sendo utilizados

### Não use o login padrão do Admin do WordPress

### Bloqueie a listagem de arquivos em suas pastas

Para impedir que os arquivos de suas pastas sejam listados, crie ou modifique o arquivo .htaccess (se seu site rodar em Linux) e inclua a seguinte linha:

```php
Options All -Indexes
```

O arquivo deve estar na pasta principal (“/”) da instalação do WordPress juntamente com o arquivo wp-config.php.

### Desabilite o WP_DEBUG.

A variável global WP\_DEBUG permite ao desenvolvedor, depurar a aplicação. Deixar estas informações visíveis também pode fornecer informações valiosas aos atacantes. Para desabilitar a variável WP\_DEBUG, edite o arquivo wp-config.php e altere de true para false.

```php
define(‘WP_DEBUG’, false);
```

### Desabilite o registro de novos usuários

Ao fazer isso você impede que qualquer um tenha acesso ao painel de administração do site. Vá até a seção Geral e desmarque a opção Qualquer pessoa pode se registrar, ou simplesmente delete o arquivo wp-register.php

Este post, de maneira nenhuma tem o objetivo de ser um guia definitivo mas sim apenas um ponto de partida para aqueles que conhecem pouco de segurança no WordPress ou para complementar os conhecimentos daqueles que já aplicam técnicas para proteção de sites e blogs.

[Fonte](http://www.pcredesecia.com.br/2013/11/32-dicas-de-seguranca-para-wordpress.html)

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/dicas-seguranca-wordpress/  

