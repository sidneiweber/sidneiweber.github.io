# Mudando O Nome Da Placa De Rede

Semana passada me deparei com a seguinte situação, tinha um servidor com  duas placas de rede , eth0 e eth1 , só que a placa de rede eth0 deu pau e foi trocada, porem, quando foi instalada a nova placa o servidor reconheceu como eth2s.

Para resolver essa situação faça o seguinte:

Com o usuário root edite o arquivo:

```shell
vi /etc/udev/rules.d/70-persistent-net.rules
```

Apague as linhas:

![netrules](http://ediomaico.files.wordpress.com/2011/03/70-persistent-net-rules.jpg)

Salva, saia e reinicie !

Suas placas voltarão novamente `eth0` e `eth1`.

[Fonte](http://ediomaico.wordpress.com/2011/03/21/mudando-o-nome-da-placa-de-rede/)

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/mudando-o-nome-da-placa-de-rede/  

