# Comando para saber quando foi instalado o seu Linux


```shell
ls -lct /etc | tail -1 | awk '{print $6, $7, $8}'
```