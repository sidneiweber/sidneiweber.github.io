# Codecs Ubuntu 9.04

Paso #1: Agregar el Repositorio de Medibuntu  
Abre el terminal ubicado en Aplicaciones/Accesorios/Terminal, y ejecuta el siguiente comando:

```bash
sudo wget http://www.medibuntu.org/sources.list.d/jaunty.list –output-document=/etc/apt/sources.list.d/medibuntu.list
```

Paso #2: Agregar la llave GPG
Ahora ejecuta este otro comando:

```bash
sudo apt-get update &amp;&amp; sudo apt-get install medibuntu-keyring &amp;&amp; sudo apt-get update
```

Paso #3: Instalar Codec’s  
Ahora podemos instalar los codec’s que necesitemos. Ejecuta cada linea en el Terminal para instalar el codec nombrado:

```bash
sudo apt-get install libdvdcss2  
sudo apt-get install w32codecs  
sudo apt-get install non-free-codecs  
sudo apt-get install ffmpeg
```

Si deseas instalar todo de una sola vez solo ejecuta esto:

```bash
sudo apt-get install libdvdcss2 w32codecs non-free-codecs ffmpeg
```


---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/codecs-ubuntu-904/  

