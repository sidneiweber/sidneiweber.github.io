---
id: 495
title: Alterar politica de senhas no Linux com PAM
date: 2017-10-17T12:41:59-03:00
author: Sidnei Weber
layout: post
guid: http://sidneiweber.com.br/?p=495
permalink: /alterar-politica-de-senhas-no-linux/
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
wp_review_user_reviews:
  - "0"
wp_review_review_count:
  - "0"
image: /wp-content/uploads/2017/10/pam1.png
categories:
  - Linux
  - Segurança
---
Para podermos ter um controle maior sobre a segurança dos nossos sistemas e rede de computadores, podemos definir uma política de senhas onde as mesmas devem ter um grau alto de dificuldade. Podendo definir quantidade de caracteres especiais, números, tamanho da senha, tempo que ela vai expirar, não repetir a mesma senha digitada anteriormente, etc.

Como não podemos confiar totalmente nas instruções passadas para os usuários, devemos forçar essas opções. Usaremos o pam para realizar esses ajustes.

O **PAM** surgiu como um intermediador entre as aplicações e o mecanismo de autenticação. Todas as aplicações agora têm suporte ao PAM, que tem uma interface de comunicação única. Então quando quisermos fazer qualquer modificação de onde autenticar, basta apenas modificar a configuração do PAM e todo o resto das aplicações já estará configurada automaticamente. Muito mais prático.

Na família Debian, o arquivo a ser ajustado será o /etc/pam.d/common-password. Em outros sistemas procure verificar se o arquivo será o mesmo. Como requisito precisaremos instalar o pacote _**libpam-cracklib.**_

<pre class="lang:default decode:true">apt-get install libpam-cracklib</pre>

Faça um backup do arquivo para garantir:

<pre class="lang:sh decode:true ">cp /etc/pam.d/common-password /root/</pre>

E agora vamos editá-lo, deixando com apenas a linha abaixo:

<pre class="lang:sh decode:true ">vi /etc/pam.d/common-password

password requisite pam_cracklib.so minlen=8 difok=3 ucredit=-1 ocredit=-1 retry=3</pre>

Onde:

**retry = 3** : tentativas antes de retornar com erro. O padrão é 1.  
**minlen = 8** : O tamanho mínimo aceitável para a nova senha.  
**difok = 3** : Essa opção não deixa ter 3 letras iguais a senha antiga. Por exemplo a senha antigo é pastel e tentar alterar para pastoso irá ser rejeitada  
**ucredit =** -1 : A nova senha deve conter pelo menos 1 caracteres maiúsculos.  
**ocredit** = -2 : A nova senha deve conter pelo menos 2 caracteres especiais.

#### Diferença entre opções positivas e negativas

Como podemos ver na opção **ucredit** usamos um valor negativo isso porque os números negativos significam que queremos no mínimo o valor x, sendo uma exigência. Quando usamos o numero positivo estamos indicando o valor máximo.

#### Outras opções

**dcredit=x**: Informa a quantidade digitos, numeros, exigidos na senha  
**lcredit=x**: Representa a quantidade caracteres minusculos, acredito que seja pouco usada

#### Proibir senhas já usadas

No mesmo arquivos iremos acrescentar

<pre class="lang:sh decode:true ">password sufficient pam_unix.so use_authtok md5 shadow remember=10</pre>

**remember=10** : Senha não poderá ser igual as ultimas 10

Testando, lembrando que se tentar trocar senha como root, ele dará o aviso porém irá alterar a senha mesmo assim. Caso seja um usuário comum ele não irá aceita a troca da senha.

<pre class="lang:sh decode:true ">passwd sidnei
SENHA INCORRETA: é simples demais</pre>

Fonte:  
<a href="http://blog.marcelocavalcante.net/blog/2011/09/27/politica-de-senhas-no-linux-senhas-com-data-para-expirar/" target="_blank" rel="noopener">http://blog.marcelocavalcante.net/blog/2011/09/27/politica-de-senhas-no-linux-senhas-com-data-para-expirar/</a>  
<a href="https://www.cyberciti.biz/faq/securing-passwords-libpam-cracklib-on-debian-ubuntu-linux/" target="_blank" rel="noopener">https://www.cyberciti.biz/faq/securing-passwords-libpam-cracklib-on-debian-ubuntu-linux/</a>