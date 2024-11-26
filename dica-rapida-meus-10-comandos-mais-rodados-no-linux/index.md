# [Dica Rápida] Meus 10 Comandos Mais Rodados No Linux

Com este comando podemos conferir quais os 10 comandos mais rodados em nossa máquina:

```shell
history|awk &#39;{print $2}&#39;|awk &#39;BEGIN {FS=&#34;|&#34;} {print $1}&#39;|sort|uniq -c|sort -rn|head -10
```

Meu resultado foi:

```shell
history|awk &#39;{print $2}&#39;|awk &#39;BEGIN {FS=&#34;|&#34;} {print $1}&#39;|sort|uniq -c|sort -rn|head -10
    248 sudo
    148 vi
    101 sh
     49 ping
     49 ls
     40 systemctl
     38 ifconfig
     38 htop
     31 ps
     26 du
sidnei@black:~$
```

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/dica-rapida-meus-10-comandos-mais-rodados-no-linux/  

