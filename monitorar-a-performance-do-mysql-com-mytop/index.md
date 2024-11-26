# Monitorar a Performance Do MySQL Com Mytop

Desenvolvido por _Jeremy D. Zawodny_, o _Mytop_ é uma ferramenta para monitorar o MySQL baseada em console (sem interface gráfica). É utilizada para verificar o desempenho geral e threads do MySQL.

Roda na maioria dos sistemas [Linux](http://www.vivaolinux.com.br/linux/)/Unix (incluindo Mac OS X), que tenham o Perl, DBI e Term:: ReadKey instalados. E com o Term:: ANSIColor instalado, você ainda terá cores. Se você instalar o Time::HiRes, você terá consultas de status em tempo real/segundos.

Plataformas suportadas:

  * Linux
  * FreeBSD
  * Mac OS X
  * BSDI
  * Solaris
  * Windows

Vamos instalar o Mytop, abra o terminal (console) e siga as instruções.

Para sistemas que utilizam o apt-get, você pode instalar como este comando:

```shell
sudo apt-get install mytop
```

Em sistemas baseados no Red Hat, como Fedora, você pode executar o comando:

```shell
yum -y install mytop
```

Se preferir, você pode fazer o download do arquivo em:

  * &lt;http://jeremy.zawodny.com/mysql/mytop/&gt;

Execute estes comandos para descompactar e instalar o Mytop:

```shell
tar -zxvf mytop-&lt;version&gt;.tar.gz
$ cd mytop-&lt;version&gt;
$ perl Makefile.PL
$ make
$ make test
$ sudo make install
```

Pronto, a ferramenta está instalada!

# Executando o Mytop

A maneira mais simples de executar Mytop é executar o comando diretamente na linha de comando. No terminal digite:

mytop -u &lt;usuário&gt; -p &lt;senha&gt; -h &lt;host&gt;_

Por exemplo:

```shell
mytop -u tsarmento -p vol2011 -h 172.16.99.253
```

Alguns outros argumentos:

  * &amp;#8221; ? &amp;#8221; &amp;#8211; Exibe ajuda;
  * &amp;#8221; d &amp;#8221; &amp;#8211; Mostra as conexões a uma determinada base de dados &amp;#8211; Nome da base de dado;
  * &amp;#8221; f &amp;#8221; &amp;#8211; Mostra a consulta completa de uma dado ID de processo (deve ser um processo ativo);
  * &amp;#8221; F &amp;#8220;- Desabilita todos os filtros (host, user, and db);
  * &amp;#8221; h &amp;#8221; &amp;#8211; Mostra apenas as consultas de um determinado host, conectar a um computador remoto;
  * &amp;#8221; I &amp;#8221; &amp;#8211; Mostra o status do InnoDB;
  * &amp;#8221; k &amp;#8221; &amp;#8211; Mata um processo;
  * &amp;#8221; m &amp;#8221; &amp;#8211; Muda o modo de exibição de top para qps (Queries Per Second Mode). Ele exibirá na tela a quantidade de querys por segundo;
  * &amp;#8221; o &amp;#8221; &amp;#8211; Inverte a ordem padrão de ordenação;
  * &amp;#8221; p &amp;#8221; &amp;#8211; Pausa a exibição;
  * &amp;#8221; q &amp;#8221; &amp;#8211; Sair do mytop;
  * &amp;#8221; r &amp;#8221; &amp;#8211; Reset os contadores de status do servidor via comando FLUSH STATUS;
  * &amp;#8221; s &amp;#8221; &amp;#8211; Muda o tempo de atualização do refresh (em segundos);
  * &amp;#8221; u &amp;#8221; &amp;#8211; Mostra os processos de um determinado usuário;
  * &amp;#8221; P &amp;#8221; &amp;#8211; Especifica uma porta não-padrão do MySQL para conectar;

Se você não quer ter que lembrar suas opções, pode criar um arquivo _~/.mytop_ para armazenar os argumentos neste formato:

```
user=root
pass=
host=localhost
db=minhabasededados
delay=5
port=3306
socket=
batchmode=0
header=1
color=1
idle=1
```

Usando um arquivo de configuração irá ajudar a assegurar que a sua senha do banco de dados não fique visível aos usuários na linha de comando. Apenas certifique-se de que as permissões do arquivo ~/.mytop estão de tal forma que os outros usuários não tenham permissão de leitura (a menos que você queira, claro).

Você pode ter algum espaço em branco nas linhas do arquivo de configuração, depois do =. Para mais informações acesse:

  * &lt;http://jeremy.zawodny.com/mysql/mytop&gt;

Agradeço a todos pela atenção.

Viva o Linux, porque nós amamos a Liberdade!

[Fonte](http://www.vivaolinux.com.br/dica/Monitorar-a-performance-do-MySQL-com-Mytop)

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/monitorar-a-performance-do-mysql-com-mytop/  

