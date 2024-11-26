# Validando Formulários PHP


## &lt;span id=&#34;Validando_CEP&#34;&gt;Validando CEP&lt;/span&gt;

O código abaixo valida o CEP informado através do método POST (conforme script abaixo).

```php    
&lt;?php
&lt;span style=&#34;font-family:Consolas, Monaco, monospace;&#34;&gt;
// Validando CEP&lt;/span&gt;
if($_POST[&#39;cep&#39;]){

if (!eregi(&#34;^[0-9]{5}-[0-9]{3}$&#34;, $_POST[&#39;cep&#39;])) {
echo &#34;&lt;script language=&#34;JavaScript&#34;&gt;alert(&#39;CEP inválido !!!&#39;);&lt;/script&gt;&#34;;

}else{
echo &#34;O CEP $cep foi validado com sucesso!!!&#34;;
}
}
?&gt;
```

Onde informamos que o CEP foi validado com sucesso, tu poderá customizar de acordo com suas necessidades!

## &lt;span id=&#34;Validando_Data&#34;&gt;Validando Data&lt;/span&gt;

O código abaixo valida a Data informada através do método POST (conforme script abaixo).

```php
&lt;?php

// Validando Data
if($_POST[&#39;data&#39;]){
if (!eregi(&#34;^[0-9]{2}/[0-9]{2}/[0-9]{4}$&#34;, $_POST[&#39;data&#39;])) {
echo &#34;&lt;script language=&#34;JavaScript&#34;&gt;alert(&#39;Data inválida !!!&#39;);&lt;/script&gt;&#34;;

}else{
echo &#34;A Data $data foi validada com sucesso!!!&#34;;
}
}
?&gt;
``` 
    

Onde informamos que validação da Data foi efetuada com sucesso, tu poderá customizar de acordo com suas necessidades!

## &lt;span id=&#34;Validando_Endereco_de_EMail&#34;&gt;Validando Endereço de EMail&lt;/span&gt;

O código abaixo deverá validar o Endereço de Email informado através do método POST (conforme script abaixo).

```php 
&lt;?php

// Validando o EMail
if ($_POST[&#39;email&#39;]){

if (!eregi(&#34;^[a-z0-9_.-]&#43;@[a-z0-9_.-]*[a-z0-9_-]&#43;.[a-z]{2,4}$&#34;, $_POST[&#39;email&#39;])) {
echo &#34;&lt;script language=&#34;JavaScript&#34;&gt;alert(&#39;Email inválido !!!&#39;);&lt;/script&gt;&#34;;

}else{
echo &#34;O EMail $email foi validado com sucesso!!!&#34;;

}
}
?&gt;
```

Onde informamos que validação do EMail foi efetuado com sucesso, tu poderá customizar de acordo com suas necessidades!

## &lt;span id=&#34;Validando_Telefones&#34;&gt;Validando Telefones&lt;/span&gt;

Abaixo temos 2 exemplos de validação de telefone.

Exemplo 01:

```php
&lt;?php

// Validando Telefone no Formato xxxx-xxxx
if($_POST[&#39;telefone&#39;]){

if (!eregi(&#34;^[0-9]{4}-[0-9]{4}$&#34;, $_POST[&#39;telefone&#39;])) {
echo &#34;&lt;script language=&#34;JavaScript&#34;&gt;alert(&#39;Telefone inválido !!!&#39;);&lt;/script&gt;&#34;;

}else{
echo &#34;O Telefone $telefone foi validado com sucesso!!!&#34;;

}
}
?&gt;
```    

Exemplo 02:

```php 
&lt;?php

// Validando Telefone no Formato (DDD) xxxx-xxxx
if($_POST[&#39;telefone&#39;]){

if (!eregi(&#34;^([0-9]{3}) [0-9]{4}-[0-9]{4}$&#34;, $_POST[&#39;telefone&#39;])) {
echo &#34;&lt;script language=&#34;JavaScript&#34;&gt;alert(&#39;Telefone inválido !!!&#39;);&lt;/script&gt;&#34;;

}else{
echo &#34;O Telefone $telefone foi validado com sucesso!!!&#34;;
&lt;span style=&#34;font-family:Consolas, Monaco, monospace;&#34;&gt;}&lt;/span&gt;
}
?&gt;
```

Onde informamos que a validação do Telefone foi efetuada com sucesso, tu poderá customizar de acordo com suas necessidades!

## &lt;span id=&#34;Validando_Pagina&#34;&gt;Validando Página&lt;/span&gt;

Esse script é especial e necessário para quem é desenvolvedor web!

Imagine aquele sistema enorme que você produziu e deixou no Servidor de seu cliente?

Após receber o conteúdo ele vende ou fornece cópia para um “amigo” que quer uma solução similar!

Criptografando o código e colocando este conteúdo, você garantirá a segurança de suas informações!

Vamos dar uma olhada no código?

```php
&lt;?php

&lt;span style=&#34;font-family:Consolas, Monaco, monospace;&#34;&gt;// Valida a cópia do Sistema&lt;/span&gt;

$server = $_SERVER[&#39;SERVER_NAME&#39;];
$endereco = $_SERVER [&#39;REQUEST_URI&#39;];
$url =&#34;http://&#34; . $server . $endereco;

$url_certa = &#34;http://enderecodosite.com/&#34;;

if($url != $url_certa) {
echo &#34;&lt;script language=&#34;JavaScript&#34;&gt;alert(&#39;VOCÊ NÃO TEM LICENÇA PARA USAR ESTA LOJA - Entre em contato com o EMail email@seuemail.com.br para validar sucópia.&#39;);&lt;/script&gt;&#34;;

}else{

echo &#34;COLOQUE AQUI O CÓDIGO DA PÁGINA&#34;;
}
&lt;span style=&#34;font-family:Consolas, Monaco, monospace;&#34;&gt;?&gt;

&lt;a href=&#34;http://www.webmaster.pt/como-validar-formulario-8269.html&#34;&gt;Fonte&lt;/a&gt;&lt;/span&gt;
```

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/validando-formularios-php/  

