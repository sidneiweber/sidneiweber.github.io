# Instalando e gerenciando programas no Windows com Chocolatey


Hoje lhes apresento uma ferramenta muito boa para gerenciar os programas no Windows, chamada [Chocolatey](https://chocolatey.org/). Para quem está acostumando com gerenciadores de pacotes do Linux como apt, yum, etc, vai se sentir em casa. Ele consegue instalar e atualizar e remover diversos programas, facilitando muito o trabalho dos técnicos e até para gerenciar um grande parque de máquinas do seu trabalho.

O programa é suporte do Windows 7 em diante e Windows server 2003 em diante, tem como pré requisito o programa .NET Framework 4+.

A instalação é bem simples e pode ser feita via **cmd** ou **Powershell**

Instalando via CMD:

```
@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
```

Instalando via Powershell

```
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```
Após a instalação o comando choco já estará disponivel. Segue algumas opções do comando:

  * list - Lista os pacotes disponíveis, enquanto fazia testes haviam incríveis **5644 pacotes**
  * search - Realiza pesquisa de pacotes
  * info - Traz informações sobre um pacote
  * install - Obviamente, instala
  * upgrade - Atualiza
  * uninstall - Adivinhe, remove 🙂

Caso queiramos instalar o VLC por exemplo:

```shell
choco install vlc
```

![chocolatey](/img/uploads/2018/04/Captura-de-tela-de-2018-04-17-20-32-04.png)


Há também uma página onde pode se verificar uma lista com os pacotes pelo link [https://chocolatey.org/packages](https://chocolatey.org/packages).

Sem contar ainda em um gerenciador gráfico chamado Chocolatey GUI, que pode sem instalado com o comando _choco install chocolateygui._

![chocolatey](https://chocolatey.org/content/images/ChocolateyGUI_main_screen.png)

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/instalando-e-gerenciando-programas-no-windows-com-chocolatey/  

