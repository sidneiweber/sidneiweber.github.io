---
id: 334
title: Comandos de manipulação de permissões no Linux
date: 2016-12-13T15:54:07-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=334
permalink: /comandos-de-manipulacao-de-permissoes-no-linux/
categories:
  - Linux
---
<div id="toc_container" class="no_bullets">
  <p class="toc_title">
    P&aacute;gina de Posts
  </p>
  
  <ul class="toc_list">
    <li>
      <a href="#Entendo_um_pouco_o_sistema_de_permissoes_no_sistema_Linux"><span class="toc_number toc_depth_1">1</span> Entendo um pouco o sistema de permissões no sistema Linux</a><ul>
        <li>
          <a href="#Diferenca_de_permissoes_entre_arquivos_e_diretorios"><span class="toc_number toc_depth_2">1.1</span> Diferença de permissões entre arquivos e diretórios:</a>
        </li>
      </ul>
    </li>
    
    <li>
      <a href="#Lista_de_comandos_para_trabalhar_as_permissoes"><span class="toc_number toc_depth_1">2</span> Lista de comandos para trabalhar as permissões</a><ul>
        <li>
          <a href="#chmod"><span class="toc_number toc_depth_2">2.1</span> chmod</a><ul>
            <li>
              <a href="#Sintaxe"><span class="toc_number toc_depth_3">2.1.1</span> Sintaxe</a>
            </li>
            <li>
              <a href="#Opcoes"><span class="toc_number toc_depth_3">2.1.2</span> Opções</a>
            </li>
            <li>
              <a href="#Exemplos"><span class="toc_number toc_depth_3">2.1.3</span> Exemplos</a>
            </li>
          </ul>
        </li>
        
        <li>
          <a href="#chgrp"><span class="toc_number toc_depth_2">2.2</span> chgrp</a><ul>
            <li>
              <a href="#Sintaxe-2"><span class="toc_number toc_depth_3">2.2.1</span> Sintaxe</a>
            </li>
            <li>
              <a href="#Opcoes-2"><span class="toc_number toc_depth_3">2.2.2</span> Opções</a>
            </li>
          </ul>
        </li>
        
        <li>
          <a href="#chown"><span class="toc_number toc_depth_2">2.3</span> chown</a><ul>
            <li>
              <a href="#Sintaxe-3"><span class="toc_number toc_depth_3">2.3.1</span> Sintaxe</a>
            </li>
            <li>
              <a href="#Opcoes-3"><span class="toc_number toc_depth_3">2.3.2</span> Opções</a>
            </li>
            <li>
              <a href="#Exemplos-2"><span class="toc_number toc_depth_3">2.3.3</span> Exemplos</a>
            </li>
          </ul>
        </li>
        
        <li>
          <a href="#umask"><span class="toc_number toc_depth_2">2.4</span> umask</a>
        </li>
      </ul>
    </li>
  </ul>
</div>

## <span id="Entendo_um_pouco_o_sistema_de_permissoes_no_sistema_Linux">Entendo um pouco o sistema de permissões no sistema Linux</span>

Pelo fato do Linux ser multiusuário, as permissões deve estar bem alinhadas para que o usuário tenha acesso somente aquilo que é de seu direito, incluindo pastas, arquivos e inclusive periféricos, como impressoras e drivers de CD por exemplo.  
A Estrtutura básica das permissões é separada em três classes:

  * Dono: define as permissões ao dono do arquivo, ou seja, que criou o arquivo.
  * Grupo: define as permissões para o grupo de usuários ao qual o dono do arquivo pertence.
  * Outros: define as permissões para os demais usuarios, que não seja o dono ou que faça parte do grupo.

Dentro de cada classe citada anteriormente, temos os tipos de acesso:

  * Leitura (r): permissão de leitura para arquivos. Caso seja um diretório permite a listagem do seu conteúdo.
  * Escrita (w): permite a escrita em arquivos ou criação dentro de pastas.
  * Execução (x): permite a execução de um programa &#8220;executável&#8221;

Quando a gente executa um ls -la no terminal, podemos ver como funciona:

<img class="alignnone size-full wp-image-339" src="/assets/img/uploads/2016/12/Sele��o_003.png" /> 

No começo de cada linha temos 10 colunas referente as permissões de cada arquivo, onde a primeira coluna identifica o tipo do arquivo, se é um arquivo, um diretório, um link, etc. Após a primeira coluna, temos um conjunto de três colunas para cada classe de permissões, ou seja, do dono, do grupo e outros contando da esquerda para direita.

### <span id="Diferenca_de_permissoes_entre_arquivos_e_diretorios">Diferença de permissões entre arquivos e diretórios:</span>

<div class="su-table su-table-alternate">
  <table>
    <tr bgcolor="red">
      <td>
        <strong><span style="color: #000000;">Objeto</span></strong>
      </td>
      
      <td>
        <span style="color: #000000;"><strong>Leitura (r)</strong><br /> </span>
      </td>
      
      <td>
        <span style="color: #000000;"><strong>Gravação (w)</strong><br /> </span>
      </td>
      
      <td>
        <span style="color: #000000;"><strong>Execução (x)</strong><br /> </span>
      </td>
    </tr>
    
    <tr>
      <td>
        Arquivo
      </td>
      
      <td>
        Permite ler o conteúdo do arquivo
      </td>
      
      <td>
        Permite alterar o arquivo
      </td>
      
      <td>
        Permite executar arquivo como um programa
      </td>
    </tr>
    
    <tr>
      <td>
        Diretório
      </td>
      
      <td>
        Permite listar o conteúdo do diretório
      </td>
      
      <td>
        Permite criar e apagar arquivos no diretório
      </td>
      
      <td>
        Permite ler e gravar arquvos no diretório
      </td>
    </tr>
  </table>
</div>

## <span id="Lista_de_comandos_para_trabalhar_as_permissoes">Lista de comandos para trabalhar as permissões</span>

### <span id="chmod">chmod</span>

Muda as permissões de acesso a um determinado arquivo ou diretório.

#### <span id="Sintaxe">Sintaxe</span>

<pre class="lang:sh decode:true">chmod [opções] [permissões] [diretório/arquivo]</pre>

#### <span id="Opcoes">Opções</span>

_-v, &#8211;verbose_

Mostra todos os arquivos que estão sendo processados.

_-f, &#8211;silent_

Não mostra a maior parte das mensagens de erro.

_-c, &#8211;change_

Semelhante a opção -v, mas só mostra os arquivos que tiveram as permissões alteradas.

_-R, &#8211;recursive_

Muda permissões de acesso do _diretório/arquivo_ no diretório atual e sub-diretórios.

ugoa+-=rwxXst

  * _ugoa_ &#8211; Indica o nível de acesso será mudado. Especificam, em ordem, usuário (u), grupo (g), outros (o), todos (a).
  * _+-=_ &#8211; _+_ adiciona a permissão, _&#8211;_ retira a permissão do arquivo e _=_ define a permissão exatamente como especificado.
  * rwx &#8211; _r_ permissão de leitura do arquivo. _w_ permissão de gravação. _x_ permissão de execução (ou acesso a diretórios).

#### <span id="Exemplos">Exemplos</span>

<pre class="lang:sh decode:true ">chmod o-r teste.txt
# Retira (-) a permissão de leitura (r) do arquivo teste.txt para os outros usuários (usuários que não são donos e não pertencem ao grupo do arquivo teste.txt).
chmod a+x teste.txt
# Inclui (+) a permissão de execução do arquivo teste.txt para o dono, grupo e outros usuários.
chmod 777 teste.txt
# Coloca permissão total de escrita, leitura e execução no arquivo teste.txt para todos usuários</pre>

###<img class="alignnone size-full wp-image-347" src="/assets/img/uploads/2016/12/Sele��o_004.png" /> 

### <span id="chgrp">chgrp</span>

Muda o grupo de um arquivo ou diretório

#### <span id="Sintaxe-2">Sintaxe</span>

<pre class="lang:sh decode:true">chgrp [opções] [grupo] [arquivo/diretório]</pre>

#### <span id="Opcoes-2">Opções</span>

_-v, &#8211;verbose_

Mostra todas as mensagens e arquivos sendo modificados.

_-R, &#8211;recursive_

Altera os grupos de arquivos/sub-diretórios do diretório atual.

### <span id="chown">chown</span>

Altera dono de um arquivo ou diretório. Pode também ser usado para mudar o grupo

#### <span id="Sintaxe-3">Sintaxe</span>

<pre class="lang:sh decode:true ">chown [opções] [dono.grupo] [diretório/arquivo]</pre>

#### <span id="Opcoes-3">Opções</span>

_-v, &#8211;verbose_

Mostra os arquivos enquanto são alterados.

_-R, &#8211;recursive_

Altera dono e grupo de arquivos no diretório atual e sub-diretórios.

#### <span id="Exemplos-2">Exemplos</span>

<pre class="lang:sh decode:true ">chown sidnei teste.txt
# Muda o dono do arquivo teste.txt para sidnei.

chown sidnei.admin teste.txt
# Muda o dono do arquivo teste.txt para sidnei e seu grupo para admin.
</pre>

### <span id="umask">umask</span>

O comando umask define as permissões iniciais quando um arquivo ou diretório for criado. Digitando _umask_ sem nenhum parâmetro podemos visualizar nosso umask atual. O umask cria permissão diferente caso o arquivo seja um executável e se for um arquivo texto. Veja a tabela a seguir:

<pre class="">---------------------------------------------
     |       |        ARQUIVO       | DIRETÓRIO  |
     | UMASK |----------------------|            |
     |       |   Binário  |  Texto  |            |
     |------------------------------|------------|
     |   0   |    r-x     |   rw-   |    rwx     |
     |   1   |    r--     |   rw-   |    rw-     |
     |   2   |    r-x     |   r--   |    r-x     |
     |   3   |    r--     |   r--   |    r--     |
     |   4   |    --x     |   -w-   |    -wx     |
     |   5   |    ---     |   -w-   |    -w-     |
     |   6   |    --x     |   ---   |    --x     |
     |   7   |    ---     |   ---   |    ---     |
     ---------------------------------------------</pre>

Caso seu umask seja 022, os arquivos de texto será criados por padrão com permissão 644, ou seja, rw- para o dono, r&#8211; para o grupo e r&#8211; para outros. Para que alterar o umask, geralmente deve-se alterar seu valor no arquivo_ **/etc/profile**_.