---
id: 380
title: 'Introdução Firewall Iptables &#8211; Começando'
date: 2017-02-15T10:44:41-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=380
permalink: /introducao-firewall-iptables-comecando/
wp_review_location:
  - bottom
wp_review_desc_title:
  - Resumo
wp_review_color:
  - '#1e73be'
wp_review_fontcolor:
  - '#555555'
wp_review_bgcolor1:
  - '#e7e7e7'
wp_review_bgcolor2:
  - '#ffffff'
wp_review_bordercolor:
  - '#e7e7e7'
wp_review_user_review_type:
  - star
wp_review_user_reviews:
  - "0"
wp_review_review_count:
  - "0"
image: /wp-content/uploads/2017/02/Sele��o_001.png
categories:
  - Firewall
tags:
  - começando com iptables
  - firewall iptables
  - introdução iptables
  - iptables
---
<div id="toc_container" class="no_bullets">
  <p class="toc_title">
    P&aacute;gina de Posts
  </p>
  
  <ul class="toc_list">
    <li>
      <a href="#Firewall_Iptables"><span class="toc_number toc_depth_1">1</span> Firewall Iptables</a><ul>
        <li>
          <a href="#Conceito_de_Firewall"><span class="toc_number toc_depth_2">1.1</span> Conceito de Firewall:</a>
        </li>
        <li>
          <a href="#Tabelas"><span class="toc_number toc_depth_2">1.2</span> Tabelas:</a>
        </li>
        <li>
          <a href="#O_que_sao_chains"><span class="toc_number toc_depth_2">1.3</span> O que são chains?</a>
        </li>
        <li>
          <a href="#Politicas_acoes_targets"><span class="toc_number toc_depth_2">1.4</span> Politicas, ações (targets):</a>
        </li>
        <li>
          <a href="#Estrutura_do_comando"><span class="toc_number toc_depth_2">1.5</span> Estrutura do comando:</a><ul>
            <li>
              <a href="#Comando_principal"><span class="toc_number toc_depth_3">1.5.1</span> Comando principal:</a>
            </li>
            <li>
              <a href="#Subcomandos"><span class="toc_number toc_depth_3">1.5.2</span> Subcomandos:</a>
            </li>
            <li>
              <a href="#Parametros_alguns"><span class="toc_number toc_depth_3">1.5.3</span> Parametros, alguns:</a>
            </li>
          </ul>
        </li>
        
        <li>
          <a href="#Checagem_de_estado_dos_pacotes_state_match"><span class="toc_number toc_depth_2">1.6</span> Checagem de estado dos pacotes (state match):</a>
        </li>
        <li>
          <a href="#Extensoes"><span class="toc_number toc_depth_2">1.7</span> Extensões:</a>
        </li>
        <li>
          <a href="#Arquivos_de_logs_criados_pelo_iptables"><span class="toc_number toc_depth_2">1.8</span> Arquivos de logs criados pelo iptables:</a>
        </li>
        <li>
          <a href="#Exemplos"><span class="toc_number toc_depth_2">1.9</span> Exemplos:</a>
        </li>
      </ul>
    </li>
  </ul>
</div>

## <span id="Firewall_Iptables">Firewall Iptables</span>

### <span id="Conceito_de_Firewall">Conceito de Firewall:</span>

O firewall é usado basicamente como um meio de proteção. Dividindo a rede que se pretende deixar segura da rede não segura.  
Geralmente um firewall é instalado na borta da rede, sendo a entrada e saida dos pacotes da mesma, fazendo a leitura de cada pacote e fazendo o controle do que pode passar para rede interna, ou dando o  redirecinamento correto, servindo de filtro.

<img class="alignnone size-full wp-image-382" src="http://sidneiweber.com.br/wp-content/uploads/2017/02/firewall1.png" alt="" width="804" height="206" srcset="https://sidneiweber.com.br/wp-content/uploads/2017/02/firewall1.png 804w, https://sidneiweber.com.br/wp-content/uploads/2017/02/firewall1-300x77.png 300w, https://sidneiweber.com.br/wp-content/uploads/2017/02/firewall1-768x197.png 768w" sizes="(max-width: 804px) 100vw, 804px" /> 

O iptables é a ferramenta de firewall a nivel de pacotes do linux desde o kernel 2.4 substituindo o ipchains.  
Ele se baseia nas regras e parametros passados para fazer a filtragem dos pacotes, ou seja, compara as regras com os pacotes.

Para termos uma segurança maior, incluindo um controle de navegação na rede interna, uma dupla muito usada e que combina muito bem, é a dupla Iptables + Squid. Squid é um proxy de navegação, mas essa solução falaremos em outra oportunidade

### <span id="Tabelas">Tabelas:</span>

Tabelas são os locais usados para armazenar as chains e conjunto de regras com uma determinada característica em comum. As tabelas podem ser referenciadas com a opção -t tabela e existem basicamente 4 tabelas disponíveis no iptables:  
**Tabela FILTER**: possui cadeias INPUT, OUTPUT, FORWARD  
**Tabela NAT**: possui cadeias PREROUTING, OUTPUT, POSTROUTING  
**Tabela MANGLE**: cadeias PREROUTING, OUTPUT, POSTROUTING, INPUT, FORWARD  
**Tabela RAW**: cadeias PREROUTING, OUTPUT

### <span id="O_que_sao_chains">O que são chains?</span>

As Chains são locais onde as regras do firewall definidas pelo usuário são armazenadas para operação do firewall.

**INPUT**: aplica regra aos pacotes que chegam ao servidor

**OUTPUT**: aplica regras aos pacotes de rede originados e que partem do servidor

**FORWARD**: aplica regras aos pacotes de rede roteados atraves do servidor (para outro servidor ou outra interface do mesmo servidor)

**PREROUTING**: altera pacotes de rede na hora que chegam e antes do roteamento

**POSTROUTING**: altera pacotes de rede após o roteamento. Usado para SNAT

### <span id="Politicas_acoes_targets">Politicas, ações (targets):</span>

**ACCEPT**: pacote permitido  
**DROP**: descartar pacote  
**QUEUE**: enviar o pacote ao userspace (codigo fora do kernel)  
**RETURN**: descontinuar o processamento do pacote e aplicar a regra padrao a ele  
**REJECT**: Descarta o pacote e envia feedback ao remetente  
**DNAT**: Reescreve endereço de destino (NAT)  
**SNAT**: Reescreve endereço de origem (NAT)  
**LOG**: coloca no log informações sobre o pacte

### <span id="Estrutura_do_comando">Estrutura do comando:</span>

#### <span id="Comando_principal">Comando principal:</span>

iptables subcomando chain parametro1 valor1 parametron valorn ação

#### <span id="Subcomandos">Subcomandos:</span>

-A cadeia &#8211; anexa a regra ao final da cadeia  
-L [cadeia] lista as regras da cadeia, ou todas caso a cadeia nao seja especificada  
-F [cadeia] apaga todas as regras na cadeia  
-N cadeia &#8211; Lista todas as regras na cadeia  
-P cadeia politica &#8211; configura a regra padrão da cadeia  
-D cadeia linha &#8211; apaga uma regra em um posição na cadeia  
-X [cadeia] excluiu uma cadeia vazia  
-I cadeia linha &#8211; insere uma regra em uma posição na cadeia  
-Z zera os contadores para todas as cadeias

#### <span id="Parametros_alguns">Parametros, alguns:</span>

-t tabela (filter é a padrao)  
-j ação  
-p protocolo (especifica o protocolo, icmp, tcp, udp, all)  
-s IP (IP de origem do pacote)  
-d IP (IP de destino do pacte)  
-i interface (nome da interface de rede de entrada do pacote)  
-o interface (nome da interface de rede de saida do pacote)  
&#8211;sport portas (Portas de origem)  
&#8211;dport portas (Portas de destino)  
&#8211;syn (identifica nova requisição de conexao)  
&#8211;icmp-type (tipo de mensagem icmp)

### <span id="Checagem_de_estado_dos_pacotes_state_match">Checagem de estado dos pacotes (state match):</span>

-m state &#8211;state OPCAO  
**NEW** cria uma nova conexao  
**ESTABLISHED** pacote que pertence a uma conexao existente  
**RELATED** pacote relacionado mas que nao faz parte de uma conexao existente  
**INVALID** pacote nao pode ser identificado (ex. falta memoria, erro ICMP de conexao nao conhecida)

### <span id="Extensoes">Extensões:</span>

Extensao TCP  
&#8211;tcp-flags (ALL, SYN, ACK, FIN, etc)  
&#8211;source-port ou &#8211;sport  
&#8211;destination-port ou &#8211;dport

Extensao UDP  
Mesmas opções do TCP

Extensao ICMP  
&#8211;icmp-type

Outras extensoes  
-m limit quando usado em LOG serve para limitar o numero de pacotes escritos durante um certo ponto  
&#8211;limit valor

### <span id="Arquivos_de_logs_criados_pelo_iptables">Arquivos de logs criados pelo iptables:</span>

Todo tráfego que for registrado pelo iptables é registrado por padrão no arquivo /var/log/kern.log.

### <span id="Exemplos">Exemplos:</span>

Exibir todas as regras:

<pre class="lang:sh decode:true ">iptables -L -n -v</pre>

Verificar regras (padrão filter &#8211;line-numbers (Exibe linhas))

<pre class="lang:sh decode:true ">iptables -L
iptables -S (lista comandos do iptables)</pre>

Verificar regras tabela nat

<pre class="lang:sh decode:true ">iptables -t nat -L</pre>

Criando uma regra, DROP em tudo que vai pra porta 123

<pre class="lang:sh decode:true ">iptabels -A INPUT -p tcp --dport 123 -j DROP</pre>

Inserindo uma regra, -I por padrao insere a regra no final  
\# indicando a linha ja a regra para a posição referente

<pre class="lang:sh decode:true ">iptables -I INPUT 1 -p tcp --sport 321 --dport 123 -J ACCEPT</pre>

Substituindo uma regra, parametro -R  
\# Substitui a regra 1 (no caso do nosso exemplo)

<pre class="lang:sh decode:true ">iptables -R INPUT 1 -p tcp --sport 321 --dport 123 -J ACCEPT</pre>

Deletar regra, parametro -D  
\# remove linha 1

<pre class="lang:sh decode:true ">iptables -D INPUT 1</pre>

\# apagar usando sintaxe, usar mesmo sintaxe com parametro -D

<pre class="lang:sh decode:true ">iptables -D INPUT -p tcp --dport 80 -j ACCEPT</pre>

Bloquear porta específica  
Sainte:

<pre class="lang:sh decode:true ">iptables -A OUTPUT -p tcp --dport xxx -j DROP</pre>

Entrante:

<pre class="lang:sh decode:true ">iptables -A INPUT -p tcp --dport xxx -j ACCEPT</pre>

Ou múltiplas portas:

<pre class="lang:sh decode:true ">iptables -A INPUT  -p tcp -m multiport --dports 22,80,443 -j ACCEPT
iptables -A OUTPUT -p tcp -m multiport --sports 22,80,443 -j ACCEPT</pre>

Manter registros de Log’s de pacotes bloqueados:

<pre class="lang:sh decode:true ">iptables -A INPUT -i eth0 -j LOG --log-prefix "Quantidade pacotes bloqueados:"
iptables -A INPUT -p tcp -dport 21 -j LOG -log-prefix “Serviço: ftp”</pre>

Os log’s são salvos em /var/log/messages.

Compartilhar internet, parametro ip\_forward precisa ser 1, geralemte altera-se no arquivo &#8220;/proc/sys/net/ipv4/ip\_forward&#8221;. Lembrando que a mudança não é permanente, a cada reinicialização deve-se alterar o parâmetro novamente ou quando criar um sript de firewall incluir o comando para alterar o arquivo com o cat.

<pre class="lang:sh decode:true ">iptables -A INPUT -m state --state RELATED.ESTABLISHED -j ACCEPT
iptables -A FORWARD -m state --state RELATED.ESTABLISHED -j ACCEPT</pre>

Ip Masquarade

<pre class="lang:sh decode:true ">iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE</pre>

Encaminhamento de portas (Ip forwarding)  
Tentando acessar pela interface wan

<pre class="lang:sh decode:true ">iptables -A PREROUTING -t nat -i eth0 -p tcp --dport 80 -j DNAT --to 192.168.10.10:80
iptables -A FORWARD -p tcp -d 192.168.10.10 --dport 80 -j ACCPET</pre>

Reject  
Descarta pacote e envia um retorno a quem enviou o pacote.

<pre class="lang:sh decode:true ">iptables -A INPUT -s 192.168.10.2 -j REJECT --reject-with icmp-net-unreachable
iptables -A INPUT -s 192.168.10.2 -j REJECT --reject-with icmp-host-unreachable
iptables -A INPUT -s 192.168.10.2 -j REJECT --reject-with icmp-proto-unreachable</pre>

entre outras opções do &#8211;reject-with

Criar chain

<pre class="lang:sh decode:true ">iptables -t filter -N [chain]</pre>

Limpar regras

<pre class="lang:sh decode:true ">iptables -t filter -F [CHAIN]</pre>

remover  Chain criada pelo usuario, parametro -X  
zerar contador, parametro -Z

Alterar regra padrão, o ideal INPUT ser drop por padrão

<pre class="lang:sh decode:true ">iptables -P INPUT DROP</pre>

Liberar servidor web

<pre class="lang:sh decode:true ">iptables -A INPUT -m state --state new -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -m state --state new -p tcp --dport 443 -j ACCEPT</pre>

Liberar host especifico

<pre class="lang:sh decode:true ">iptabels -A INPUT -s 192.168.1.20 -j ACCEPT</pre>

Liberar ping (resposta liberada se output esta ACCEPT tbm)

<pre class="lang:sh decode:true ">iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT</pre>

Liberar respostas de ping para outras maquinas

<pre class="lang:sh decode:true ">iptables -A INPUT -p icmp --icmp-type echo-reply -j ACCEPT</pre>

Proteção contra Syn-flood:

<pre class="lang:sh decode:true ">iptables -A FORWARD -p tcp --syn -m limit --limit 1/s -j ACCEPT</pre>

Port scanner suspeito:

<pre class="lang:sh decode:true ">iptables -A FORWARD -p tcp --tcp-flags SYN,ACK,FIN,RST RST -m limit --limit 1/s -j ACCEPT</pre>

Ping da morte:

<pre class="lang:sh decode:true ">iptables -A FORWARD -p icmp --icmp-type echo-request -m limit --limit 1/s -j ACCEPT</pre>

Salvando e restaurando as regras:

<pre class="lang:sh decode:true">iptables-save &gt; arquivo
iptables-restore &lt; arquivo
</pre>