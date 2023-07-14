# Reconhecer HD novo Linux sem reiniciar

Hoje vamos a mais uma dica rápida. Pra que usa seus servidores virtualizados e precisa adicionar um novo HD seja por falta de espaço ou pelo motivo que for, não precisa reiniciar o servidor para ter o HD reconhecido. Basta apenas executar um simples comando que ordena um "scan" no barramento.

Vale lembrar também que essa dica é para virtualizações com Hot plug habilitado.

```shell
echo "- – -" > /sys/class/scsi_host/host0/scan
```

Obrigado e até a próxima.


---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/reconhecer-hd-novo-linux-sem-reiniciar/  

