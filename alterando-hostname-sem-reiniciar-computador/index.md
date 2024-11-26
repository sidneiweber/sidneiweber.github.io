# Alterando Hostname Sem Reiniciar Computador

Para podermos alterar o nome da máquina sem precisar reiniciar é muito simples. Primeiramente precisamos alterar o arquivo /etc/hostname. Mas após a alteração notamos que o nome não muda, mesmo dando o comando hostname, o nome continua o antigo. Para essa alteração valer sem precisar reiniciar, pois as vezes pode se tratar de um servidor que não pode parar no momento, basta digitar o comando abaixo:

```shell
echo &#34;novo-hostname&#34; &gt; /proc/sys/kernel/hostname
```

Pronto, problema resolvido.

[Fonte](https://www.vivaolinux.com.br/dica/Debian-Wheezy-Alterando-hostname-sem-reiniciar)

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/alterando-hostname-sem-reiniciar-computador/  

