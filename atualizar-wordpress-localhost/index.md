# Atualizar WordPress Localhost

Para atualizar o WordPress instalado localmente, basta trocar o método do sistema de arquivos com o parâmetro:  **FS_METHOD**

A seguir, estão as constantes válidas para atualizações do WordPress:

  * **FS_METHOD** obriga o método do sistema de arquivos. Deve ser &#34;direct&#34;, &#34;ssh&#34;, &#34;ftpext&#34;, ou &#34;ftpsockets&#34;. Geralmente, você deve apenas mudar isso se estiver enfrentando problemas de atualização, se mudar, e não adiantar **mude de volta/remova**, Na maioria das circunstâncias, definir **ftpsockets** vai funcionar se o método escolhido automaticamente não funcionar. 
      * **(Primary Preference) &amp;#8220;Direct&amp;#8221;** obriga a usar solicitações Direct File I/O de dentro do PHP, o que possui muitas questões de segurança em servidores mal configurados, pode ser escolhido automaticamente quando necessário.
      * **(Secondary Preference) &amp;#8220;ssh&amp;#8221;** obriga a usar a extensão SSH PHP.
      * **(3rd Preference) &amp;#8220;ftpext&amp;#8221;** obriga a usar a extensão FTP PHP para acesso FTP e finalmente:
      * **(4th Preference) &amp;#8220;ftpsockets&amp;#8221;** usa classe de Sockets PHP para acesso FTP.

```php
define(&#39;FS_METHOD&#39;, direct);
```

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/atualizar-wordpress-localhost/  

