# Desligar Ou Reiniciar O Computador Com Hora Marcada

Para programar o computador para desligar em um certo horário, basta como root usar o seguinte comando:

```shell
shutdown -h hh:mm
```

Sendo que hh são as horas no formato de 24 horas e mm são os minutos.

Outra maneira para programar o desligamento do seu pc é usar o seguinte comando:

```shell
shutdown -h &#43;m
```

Sendo que m é o número de minutos que você deseja até o computador desligar.

Ex:

```shell
shutdown -h &#43;300
```

Significa que o computador desligará daqui a 300 minutos.

Depois de executar um desses comandos começará uma contagem regressiva no seu terminal. Da mesma maneira podemos utilizar esses dois modelos para reiniciar o computador. A diferença é que em vez de passar o parâmetro -h, passaremos o parâmetro -r. Ficaria assim:

```shell
shutdown -r hh:mm
```
ou
```shell
shutdown -r &#43;m
```

[Fonte](http://www.vivaolinux.com.br/dica/Desligar-ou-reiniciar-o-computador-com-hora-marcada)

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/desligar-ou-reiniciar-o-computador-com-hora-marcada/  

