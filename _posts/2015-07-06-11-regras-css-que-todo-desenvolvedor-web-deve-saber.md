---
id: 168
title: 11 regras CSS que todo desenvolvedor web deve saber
description: 11 regras CSS que todo desenvolvedor web deve saber
date: 2015-07-06T15:43:13-03:00
author: Sidnei Weber
layout: post
permalink: /11-regras-css-que-todo-desenvolvedor-web-deve-saber/
geo_public:
  - "0"
wp_review_user_reviews:
  - "0"
wp_review_review_count:
  - "0"
categories:
  - CSS
---
<div id="toc_container" class="no_bullets">
  <p class="toc_title">
    P&aacute;gina de Posts
  </p>
  
  <ul class="toc_list">
    <li>
      <a href="#media"><span class="toc_number toc_depth_1">1</span> @media</a>
    </li>
    <li>
      <a href="#background-size"><span class="toc_number toc_depth_1">2</span> background-size</a>
    </li>
    <li>
      <a href="#font-face"><span class="toc_number toc_depth_1">3</span> @font-face</a>
    </li>
    <li>
      <a href="#overflowhidden"><span class="toc_number toc_depth_1">4</span> overflow:hidden</a>
    </li>
    <li>
      <a href="#margin_0_auto"><span class="toc_number toc_depth_1">5</span> margin: 0 auto;</a>
    </li>
    <li>
      <a href="#inputtype8221text8221"><span class="toc_number toc_depth_1">6</span> input[type=&#8221;text&#8221;]</a>
    </li>
  </ul>
</div>

### <span id="media">@media</span>

A regra @media não só nos permite definir estilos para nossa página da web quando impressa na tela. Hoje em dia esta regra atingiu um patamar mais avançado com as “media queries“, que são associadas à criação de sites “adaptativos” ou “responsivos”, ou seja, que se ajustam ao tamanho da tela do dispositivo no qual estiverem sendo acessados.

Você pode criar uma media query usando propriedades como min-width para ajustar seu layout de acordo com o tamanho do “viewport” do dispositivo do usuário.

<pre>[css]
@media screen and (max-width: 960px) {
// seus estilos vão aqui ....
}
[/css]</pre>

### <span id="background-size">background-size</span>

Aí está uma propriedade CSS3 muito útil que ganhou total suporte nos navegadores modernos. Antes, para fazer com que uma imagem, definida como background, fosse ajustada 100% (full size), de acordo com o tamanho do elemento que faz parte, era necessário algumas linhas de código, hacks e até javascripts. Agora nós precisamos de apenas uma linha de código, ou melhor, apenas uma propriedade:`background-size`

<pre>[css]
body {
background: url(image.jpg) no-repeat;
background-size: 100%;
}
[/css]</pre>

### <span id="font-face">@font-face</span>

<pre>[css]

@font-face {
font-family: Blackout;
src: url("assests/blackout.ttf") format("truetype");
}
[/css]</pre>

### <span id="overflowhidden">overflow:hidden</span>

<pre>[css]

.container {
overflow: hidden;
}
[/css]</pre>

Existe uma série de soluções e hacks para ajudar a resolver o problema com os elementos flutuantes. Este problema ocorre quando temos, dentro de um elemento de bloco (um DIV por exemplo), um outro elemento com float. Esse elemento que “flutua” não força automaticamente a altura do elemento container, ou seja, a altura do elemento container não acompanha a altura do elemento com float. Isto ocorre porque o elemento que está flutuando deixa de considerar o elemento container como pai.

Um jeito hiper simples de “limpar” os elementos flutuantes é simplesmente declarar `overflow: hidden;` no elemento container. Isto é muito interessante, porque não precisamos mais adicionar “lixo”  no nosso código html, como o tão famoso `<br style="clear:both" />`.

### <span id="margin_0_auto">margin: 0 auto;</span>

<div id="crayon-537cd819bce56207608020">
  <div>
    <table class="mceItemTable">
      <tr>
        <td>
          <div>
            <div>
              1
            </div>
            
            <div>
              2
            </div>
            
            <div>
              3
            </div>
          </div>
        </td>
        
        <td>
          <div>
            <div id="crayon-537cd819bce56207608020-1">
              #container {
            </div>
            
            <div id="crayon-537cd819bce56207608020-2">
                  margin: 0 auto;
            </div>
            
            <div id="crayon-537cd819bce56207608020-3">
              }
            </div>
          </div>
        </td>
      </tr>
    </table>
  </div>
</div>

É surpreendente que até então não exista nenhuma propriedade especifica para centralizar elementos. Mas enquanto isso não acontece, nós podemos utilizar o recurso de margem automática. Ao adicionarmos `margin: 0 auto;` em um elemento de bloco, este será centralizado.

### <span id="inputtype8221text8221">input[type=&#8221;text&#8221;]</span>

O seletor `input[type="text"]`, bem como outros seletores avançados no geral, irão elevar suas habilidades com CSS do nível intermediário para o avançado. Seletores de atributos, em particular, são extremamente úteis para estilizar elementos sem que precisemos criar classes adicionais.

Você poderá manipular não só campos do tipo texto, mas também radio, checkbox, submit, password, file, etc.

<pre>[css]

input[type="text"] {
width: 200px;
}

input[type="checkbox"]{
margin-right: 1em;
}
[/css]</pre>

<a href="http://wpmidia.com.br/desenvolvimento-web/11-regras-css-todo-desenvolvedor-web-deve-saber/" target="_blank">Fonte</a>