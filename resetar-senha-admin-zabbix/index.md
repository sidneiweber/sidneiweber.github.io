# Resetar Senha Admin Zabbix

Hoje vamos a uma dica rápida para quem esqueceu ou não sabe a senha de Admin do painel de administração do Zabbix. Eu estava testando a ferramenta e depois de um tempo se mexer havia esquecido a senha, tive que resetá-la. Para isso a única coisa que precisamos é ter a senha de root do mysql, tendo ela podemos logar no terminal:

```shell
mysql -u root -p
Enter password:
```

Dentro do terminal a gente vai fazer o seguinte:

```shell
mysql&gt; use zabbix;
mysql&gt; UPDATE users SET passwd=md5(‘novasenha’) WHERE alias=’Admin’;
```

Pronto, senha resetada.

[Fonte:](https://jorgepretel.com.br/2016/04/reset-na-senha-admin-do-zabbix/)

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/resetar-senha-admin-zabbix/  

