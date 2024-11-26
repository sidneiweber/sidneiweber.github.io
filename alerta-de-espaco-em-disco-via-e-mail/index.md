# Alerta De Espaço Em Disco via E-Mail

Script para enviar e-mail quando o uso de disco chegar a 90% de uso

```shell
df -k | grep -e &#39;lv&#39; | awk &#39;{ print $4 &#34; &#34; $7 }&#39; | while read output;
do
echo $output
usep=$(echo $output | awk &#39;{ print $1}&#39; | cut -d&#39;%&#39; -f1 )
partition=$(echo $output | awk &#39;{ print $2 }&#39; )
if [ $usep -ge 90 ]; then
echo &#34;Verifique o diretorio &#34;$partition&#34; com ($usep%) de uso no servidor $(hostname)&#34; | mail -s &#34;Alerta! Disco excedido em $usep%&#34; seu_email@provedor.com
fi
done
```

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/alerta-de-espaco-em-disco-via-e-mail/  

