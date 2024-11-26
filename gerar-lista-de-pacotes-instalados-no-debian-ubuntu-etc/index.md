# Gerar Lista De Pacotes Instalados No Debian, Ubuntu, Etc

Para gerar uma lista dos pacotes instalados no sistema, poderemos usar o **dpkg** para isso. Pode ser muito útil na hora de criar sistemas com a mesma base

#### Gerando lista de pacotes

```shell
sudo dpkg --get-selections &gt; install.list
```

#### Instalando pacotes a partir da lista

```shell
sudo dpkg --set-selections &lt; install.list
sudo apt-get -y update
sudo apt-get dselect-upgrade
```

[Fonte](http://www.dicas-l.com.br/dicas-l/20161025.php)

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/gerar-lista-de-pacotes-instalados-no-debian-ubuntu-etc/  

