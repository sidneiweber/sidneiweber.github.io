# Verificar Máquinas Ligadas Com Shell Script

Estava interessado em criar uma forma de scannear a rede para saber quantos micros estavam conectados a ela, saber nome, grupo, MAC ADDRESS.

Para que o script funcione será preciso instalar alguns softwares:

dialog:

```shell
apt-get install dialog
```

nmap:

```shell
apt-get install nmap
```

Copie o código e cole em um arquivo texto e salve com um nome de sua preferência, de permissão para executar (chmod &#43;x nome\_do\_arquivo.sh) e em seguida execute-o (./nome\_do\_arquivo.sh):

```bash
#!/bin/bash

Principal ( ) { ## Inicio Primeiro Bloco
clear
# Loop que mostra o menu principal
while : ; do # Mostra o menu na tela, com as ações disponíveis
opcao=$(
dialog --stdout
--title &#39;Menu principal&#39;
--menu &#39;Escolha as opções:&#39;
0 0 0
1 &#39;Scannear IPs da Rede&#39;
0 &#39;Sair&#39;)

[ $? -ne 0 ] &amp;&amp; Sair # Se apertado CANCELAR ou ESC, então vamos Sair...

case $opcao in ## ## Inicio case
1)ipscan ;;
0)Sair ;;

esac ## Fim da verificação
done
}
## FIM MENU PRINCIPAL

## &#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43;&#43; ##

ipscan ( ) {
clear
inicio=$(dialog --stdout --title &#39;Firerock ipscan&#39; --inputbox &#39;Inicio (Ex.192.168.0.1)&#39; 0 0 )

[ $? -ne 0 ] &amp;&amp; Principal # Se apertado CANCELAR ou ESC, então vamos Sair...
final=$(dialog --stdout --title &#39;Firerock ipscan&#39; --inputbox &#39;Final (Ex.192.168.0.254)&#39; 0 0 )

[ $? -ne 0 ] &amp;&amp; ipscan # Se apertado CANCELAR ou ESC, então vamos Sair...

#faixa_rede=`echo &#34;$inicio&#34; | cut -d &#39;.&#39; -f 1-3`
inicio_host=`echo &#34;$inicio&#34; | cut -d &#39;.&#39; -f 4`
final_host=`echo &#34;$final&#34; | cut -d &#39;.&#39; -f 4`

inicio_host=$(expr $inicio_host - 1)
hosts_verificados=$(expr $final_host - $inicio_host)

dialog --yesno &#39;O processo pode levar alguns minutos! Deseja Continuar?&#39; 6 45

if [ $? = 0 ]; then
continua

else
clear
ipscan
fi
}
continua ( ) {
echo &#34; &#34;
echo &#34;STATUS ENDEREÇO IPv4 MAC ADDRESS NOME GRUPO &#34; &amp;gt; /tmp/hosts.txt
echo &#34;------------------------------------------------------------------------------------------&#34; &amp;gt;&amp;gt; /tmp/hosts.txt

ips_on=$(nmap -sP &#34;$inicio-$final_host&#34; | awk &#39;/^Host/ {print $2}&#39;)
online=&#34;0&#34;
offline=&#34;0&#34;

for ip in $ips_on; do
$(nmblookup -A $ip &amp;gt; /tmp/nm_hosts.txt) ## Saída do comando é # entre clientes Windows e Unix (Linux)
mac_address_win2003=$(cat /tmp/nm_hosts.txt | awk &#39;NR==9 {print $4}&#39;)
mac_address_xp=$(cat /tmp/nm_hosts.txt | awk &#39;NR==7 {print $4}&#39;)
nm_pc=$(cat /tmp/nm_hosts.txt | awk &#39;NR==2 {print $1}&#39;)
nm_grupo=$(cat /tmp/nm_hosts.txt | awk &#39;NR==3 {print $1}&#39;)

mac_address_unix=$(cat /tmp/nm_hosts.txt | awk &#39;NR==10 {print $4}&#39;) ##inicio de verificação p/ ver se é cliente Unix

if [ &#34;$mac_address_unix&#34; == &#34;00-00-00-00-00-00&#34; ]; then ## Se $mac_address_unix for igual a 00-00-00-00-00-00 é um cliente unix
#mac_address=$(cat /tmp/nm_hosts.txt | awk &#39;NR==10 {print $4}&#39;)
nm_pc=$(cat /tmp/nm_hosts.txt | awk &#39;NR==2 {print $1}&#39;)
nm_grupo=$(cat /tmp/nm_hosts.txt | awk &#39;NR==6 {print $1}&#39;)
echo &#34;On $ip $mac_address_unix $nm_pc $nm_grupo&#34; &amp;gt;&amp;gt; /tmp/hosts.txt
online=$(expr $online &#43; 1)

else
if [ &#34;$mac_address_xp&#34; == &#34;&#34; ]; then
echo &#34;On $ip $mac_address_win2003 $nm_pc $nm_grupo&#34; &amp;gt;&amp;gt; /tmp/hosts.txt
online=$(expr $online &#43; 1)

else
if [ ! $nm_pc == &#39;No&#39; ]; then
echo &#34;On $ip $mac_address_xp $nm_pc $nm_grupo&#34; &amp;gt;&amp;gt; /tmp/hosts.txt
online=$(expr $online &#43; 1)

else
mac_address=
nm_pc=
nm_grupo=
echo &#34;On $ip $mac_address $nm_pc $nm_grupo&#34; &amp;gt;&amp;gt; /tmp/hosts.txt
online=$(expr $online &#43; 1)
fi
fi
fi
done
offline=$(expr $hosts_verificados - $online)
echo &#34;------------------------------------------------------------------------------------------&#34; &amp;gt;&amp;gt; /tmp/hosts.txt
echo &#34; &#34; &amp;gt;&amp;gt; /tmp/hosts.txt

echo &#34;Informações:&#34; &amp;gt;&amp;gt; /tmp/hosts.txt
echo &#34;Faixa de IPs verificados:&#34; &amp;gt;&amp;gt; /tmp/hosts.txt
echo &#34;Inicio: $inicio&#34; &amp;gt;&amp;gt; /tmp/hosts.txt
echo &#34;Final : $final&#34; &amp;gt;&amp;gt; /tmp/hosts.txt
echo &#34; &#34; &amp;gt;&amp;gt; /tmp/hosts.txt
echo &#34;Hosts Verificado: $hosts_verificados&#34; &amp;gt;&amp;gt; /tmp/hosts.txt
echo &#34;Hosts Online: $online&#34; &amp;gt;&amp;gt; /tmp/hosts.txt
echo &#34;Hosts Offline: $offline&#34; &amp;gt;&amp;gt; /tmp/hosts.txt
echo &#34; &#34; &amp;gt;&amp;gt; /tmp/hosts.txt
echo &#34;OBS:&#34; &amp;gt;&amp;gt; /tmp/hosts.txt
echo &#34;Endereços com status On que não possuem (ou é invalido) MAC ADDRESS, NOME, GRUPO ou qualquer um, geralmente são clientes UNIX.&#34; &amp;gt;&amp;gt; /tmp/hosts.txt
echo &#34;Exemplos:&#34; &amp;gt;&amp;gt; /tmp/hosts.txt
echo &#34;On 192.168.0.1 &#34; &amp;gt;&amp;gt; /tmp/hosts.txt
echo &#34;On 192.168.0.254 00-00-00-00-00-00 Meupc MEUGRUPO&#34; &amp;gt;&amp;gt; /tmp/hosts.txt
dialog
--title &#39;Lista de Hosts Online&#39;
--textbox /tmp/hosts.txt
0 0

ipscan
}

## ------------------------------------------------------------------------------------------------------------------------------------------------------
Sair ( ) {
clear
exit
}
Principal&lt;/pre&gt;
```

Fonte: http://www.vivaolinux.com.br/dica/Ipscan-com-shell-script&#43;dialog&#43;nmap

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/verificar-maquinas-ligadas-do-shell-script/  

