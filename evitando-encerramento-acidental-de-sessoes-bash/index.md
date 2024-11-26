# Evitando Encerramento Acidental De Sessões Bash

A sequência de teclas &#34;`CTRL&#43;D`&#34; encerra uma sessão bash. Às vezes digitamos estas teclas por acidente e encerramos uma sessão acidentalmente.

Para evitar que isto ocorra, definimos a variável de ambiente `IGNOREEOF`:

```shell
export IGNOREEOF=1
```

Desta forma, para encerrar uma sessão bash, precisamos digitar a sequência `CTRL&#43;D` duas vezes ou então digitar `exit`.

Esta variável de ambiente deve ser definida no arquivo `.bashrc`.

Fonte: [Dicas-L](http://www.dicas-l.com.br/arquivo/encerramento_acidental_de_sessoes_bash.php#.VDVCZdRdW2w)

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/evitando-encerramento-acidental-de-sessoes-bash/  

