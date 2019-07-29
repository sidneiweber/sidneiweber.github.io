---
id: 192
title: SCP Fácil
date: 2015-07-06T16:23:19-03:00
author: Sidnei Weber
layout: page
guid: https://sidiweber.wordpress.com/?page_id=192
geo_public:
  - "0"
wp_review_user_reviews:
  - "0"
wp_review_review_count:
  - "0"
wp_review_location:
  - bottom
wp_review_desc_title:
  - Resumo
wp_review_color:
  - '#1e73be'
wp_review_fontcolor:
  - '#555555'
wp_review_bgcolor1:
  - '#e7e7e7'
wp_review_bgcolor2:
  - '#ffffff'
wp_review_bordercolor:
  - '#e7e7e7'
wp_review_user_review_type:
  - star
---
<div class="post-content box mark-links">
  <p>
    Projeto que fiz para facilitar o envio de arquivos de uma máquina para outra com o SCP. Programas necessários: nmap e yad
  </p>

  <p>
    <img class="alignnone size-full wp-image-314" src="http://sidneiweber.com.br/wp-content/uploads/2015/07/scp.png" alt="scp" width="64" height="61" />
  </p>

```shell
#!/bin/bash
# yad com FORMULARIOS, que bacana, tem algumas novidades aprecie com calma
principal() {
FORMULARIO=$( \
   yad --form \
       --title="SCP Fácil" \
       --text "&lt;big&gt;Envio arquivos com facilidade para outras máquinas com &lt;b&gt;SCP Fácil&lt;/b&gt;&lt;/big&gt;" \
       --width=400 \
       --height=250 \
       --image="/usr/share/pixmaps/scp.png" \
       --field="Selecionar arquivo:":FL "$HOME/$USER" \
       --field="IP:" "" \
       --field="Usuário destino:" "$USER" \
       --field="Porta:": "22"\
        --field="Senha:":H "123456"\
     #--field='Executar':BTN "scp -rp -P%4 %1 %3@%2:~" --no-buttons
)
# ver se o usuário clicou em 'sair' or no 'x' da janela
ACAO="$?"
test "$ACAO" -eq "1" || test "$ACAO" -eq "252"
if [ "$?" -eq "0" ]; then
   exit
fi

ARQUIVO=$(echo "$FORMULARIO" | cut -d"|" -f 1)
IP=$(echo "$FORMULARIO" | cut -d"|" -f 2)
USUARIO=$(echo "$FORMULARIO" | cut -d"|" -f 3)
PORTA=$(echo "$FORMULARIO" | cut -d"|" -f 4)
SENHA=$(echo "$FORMULARIO" | cut -d"|" -f 5)


sshpass -p "$SENHA" scp -rp -P$PORTA $ARQUIVO $USUARIO@$IP:~ && zenity --window-icon=$ICONE --info --text=" Arquivos enviados com sucesso" || zenity --window-icon=$ICONE --error --text="Erro ao enviar arquivo, verifique se os dados estão corretos"
principal
}
principal
#.EOF
```

  <p>
    Pretendo melhorar ele com o tempo
  </p>

  <p>
    Segue o link:<a href="https://github.com/emmilinux/scpfacil.git" target="_blank" rel="noopener"> scp-facil</a>
  </p>
</div>
