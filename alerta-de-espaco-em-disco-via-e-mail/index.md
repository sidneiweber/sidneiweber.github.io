# Alerta de espaço em disco via e-mail

Script para enviar e-mail quando o uso de disco chegar a 90% de uso

```shell
df -k | grep -e 'lv' | awk '{ print $4 " " $7 }' | while read output;
do
echo $output
usep=$(echo $output | awk '{ print $1}' | cut -d'%' -f1 )
partition=$(echo $output | awk '{ print $2 }' )
if [ $usep -ge 90 ]; then
echo "Verifique o diretorio "$partition" com ($usep%) de uso no servidor $(hostname)" | mail -s "Alerta! Disco excedido em $usep%" seu_email@provedor.com
fi
done
```

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/alerta-de-espaco-em-disco-via-e-mail/  

