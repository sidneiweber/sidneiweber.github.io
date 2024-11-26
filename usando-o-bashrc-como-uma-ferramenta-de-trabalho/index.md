# Usando O Bashrc Como Uma Ferramenta De Trabalho

Segue o meu .bashrc com vários atalhos e alterações.

```shell
# Cor Verde (Usuario comum)
PS1=&#39;${debian_chroot:&#43;($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\$ &#39;
# Cor Vermelha (root)
#PS1=&#39;${debian_chroot:&#43;($debian_chroot)}\[\033[1;31m\]\u@\h\[\033[00m\]:\[\033[1;34m\]\w\[\033[00m\]\$ &#39;

# Completion
if [ -f /etc/bash_completion ]; then
    . /etc/bash_completion
fi

# Configurações Historico
export HISTIGNORE=&#34;&amp;:ls:[bf]g:exit:reset:clear:cd*&#34;
export HISTSIZE=4096
export HISTCONTROL=&#34;ignoreboth:erasedups&#34;
shopt -s histreedit;

# Mans coloridas
export MANPAGER=&#34;/usr/bin/most -s&#34;

# Alias
alias update=&#39;pacman -Syu&#39;

alias ls=&#39;ls --color=auto&#39;
alias grep=&#39;grep --color=auto&#39;
alias fgrep=&#39;fgrep --color=auto&#39;
alias egrep=&#39;egrep --color=auto&#39;

# Extração de arquivos
# Uso: extrair &lt; arquivo &gt; 
extrair() { 
if [ -f $1 ] ; then
case $1 in
*.tar.bz2) tar xvjf $1 ;; 
*.tar.gz) tar xvzf $1 ;; 
*.tar.xz) tar xvJf $1 ;; 
*.bz2) bunzip2 $1 ;; 
*.rar) unrar x $1 ;; 
*.gz) gunzip $1 ;; 
*.tar) tar xvf $1 ;; 
*.tbz2) tar xvjf $1 ;; 
*.tgz) tar xvzf $1 ;; 
*.zip) unzip $1 ;; 
*.Z) uncompress $1 ;; 
*.7z) 7z x $1 ;; 
*.xz) unxz $1 ;; 
*.exe) cabextract $1 ;; 
*) echo &#34;\`$1&#39;: unrecognized file compression&#34; ;; 
esac 
else
echo &#34;\`$1&#39; is not a valid file&#34;
fi
}

# Misc
alias musica=&#39;mocp -m /media/Documentos/Musica/&#39;

# Top 10 ( mostra os 10 comandos mais utilizados ). copyright 2007 - 2010 Christopher Bratusek 
function top10() { 
history | awk &#39;{a[$2]&#43;&#43; } END{for(i in a){print a[i] &#34; &#34; i}}&#39; | sort -rn | head
} 

# alisa previsao tempo
alias tempo=&#39;curl http://wttr.in/sapiranga&#39;
```

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/usando-o-bashrc-como-uma-ferramenta-de-trabalho/  

