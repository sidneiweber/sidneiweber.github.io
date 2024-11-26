# VirtualBox: Reduzindo Imagens VDI

As imagens VDI são dinamicamente expansíveis. Isto é legal, porque é possível criar um arquivo pequeno que vai crescendo a medida que o disco da máquina virtual precisa armazenar mais arquivos. Mas se depois de um tempo você liberar espaço no &amp;#8220;disco virtual&amp;#8221;, o arquivo VDI não é reduzido.

Para resolver isto, é preciso seguir as seguintes etapas:

1) Zerar os setores não utilizados no sistema de arquivos virtual do arquivo VDI. Se o sistema convidado for Linux, você provavelmente vai encontrar uma solução com o dd. No meu caso, o sistema virtual era o Windows XP, então utilizei o aplicativo ccleaner que, além de remover arquivos desnecessários, possui a opção (em avançado) de preencher com zero o espaço livre.

2) Rode o seguinte programa (na máquina hospedeira):

```shell
vboxmanage modifyvdi nome_do_seu_arquivo.vdi compact
```

Aqui consegui reduzir de 5 para 3,8GB o meu arquivo.

**Fonte**: &lt;http://www.vivaolinux.com.br/dica/VirtualBox-Reduzindo-imagens-VDI&gt;

---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/virtualbox-reduzindo-imagens-vdi/  

