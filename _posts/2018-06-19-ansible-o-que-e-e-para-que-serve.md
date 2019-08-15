---
layout: post
title: Ansible - O que é e para que serve
id: 525
date: '2018-06-19 20:34:23 -0300'
author: Sidnei Weber
guid: http://sidneiweber.com.br/?p=525
permalink: "/ansible-o-que-e-e-para-que-serve/"
wp_review_location:
- bottom
wp_review_desc_title:
- Resumo
wp_review_color:
- "#1e73be"
wp_review_fontcolor:
- "#555555"
wp_review_bgcolor1:
- "#e7e7e7"
wp_review_bgcolor2:
- "#ffffff"
wp_review_bordercolor:
- "#e7e7e7"
wp_review_user_review_type:
- star
image: "/wp-content/uploads/2018/06/ansible.png"
categories:
- Ansible
- Devops
---

> ### <span id="ANSIBLE_LOVES_THE_REPETITIVE_WORK_YOUR_PEOPLE_HATE">ANSIBLE LOVES THE REPETITIVE WORK YOUR PEOPLE HATE</span>

Com essa frase começa a apresentação da ferramenta Ansible em seu próprio site. Bom, resumidamente o Ansible é um software que automatiza o provisionamento de software, gerenciamento de configuração e implantação de aplicativos. Ou seja, tudo aquilo que era feito repetidas vezes para configurar, atualizar um servidor ou serviço, pode ser automatizado com Ansible.

Bem vindo ao mundo da automação 🙂

Obviamente o Ansible não é a única ferramenta que pode fazer esse trabalho, temos outras ferramentas como Chef, Puppet, Saltstack. Todas elas tem suas características, qualidades e defeitos em particular, não realizar comparação entre essas ferramentas, vou somente dar a minha posição de o por que escolhi o Ansible.

#### <span id="Simplicidade_e_recursos">Simplicidade e recursos:</span>

Ansible foi desenvolvido em Python, então praticamente todas as versões de Linux terão suporte a mesma.  
Mais de 1000 módulos para tudo quanto é tipo de áreas: banco de dados, monitoramento, nuvem e até para Windows.  
Comandos &#8220;ad-hoc&#8221; diretamente para diversos recursos. Podemos criar playbooks usando o padrão YAML de fácil entendimento.  
Possui módulos para Docker, Vmware, Proxmox, AWS, Openstack, Azure, gerenciamento de pacotes, enfim, são muitos módulos mesmo. Caso queira ver a lista completa, <a href="https://docs.ansible.com/ansible/latest/modules/list_of_all_modules.html" target="_blank" rel="noopener">acesse este endereço.</a>

#### <span id="Sem_agentes">Sem agentes:</span>

Principal recurso que me fez optar em estudar o Ansible foi pelo fato de não necessitar o uso de agentes nos clientes, basta que o cliente tenha Python instalado e acesso via SSH ou Winrm para Windows.

### <span id="Instalacao_Ansible">Instalação Ansible:</span>

A instalação segue o mesmo nível de simplicidade de seu uso, basta utilizar o gerenciador de pacotes de sua distribuição:

**Ubuntu**:

```shell
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get update -y && sudo apt-get install -y ansible
```

**Centos, Fedora:**

```shell
yum install -y epel-release && yum install -y ansible
```

### <span id="Execucao_AD_HOC_vs_Playbook">Execução: AD HOC vs Playbook</span>

Essa são as duas maneiras que temos de executar nossos comandos no Ansible como dito anteriormente. Um arquivo muito importante para é o <span class="wp_shortcodes_tooltip" title="Arquivo muito importante" data-gravity="n" data-fade="0">/etc/ansible/hosts</span> onde a gente pode organizar as máquinas onde poderemos realizar as execuções, em breve escrevei um artigo com alguns macetes desse arquivo.

Vamos por a mão na massa executando nosso primeiro comando em localhost, somente para teste usaremos o módulo &#8220;ping&#8221; :

```shell
root@localhost:~# ansible 127.0.0.1 -m ping

127.0.0.1 | SUCCESS =&gt; {
    "changed": false,
    "ping": "pong"
}
```

Sucesso, tivemos o retorno do ping do nosso localhost ;).

Bom no próximo artigo irei explicar como realizar execuções em algumas máquinas remotas ao mesmo tempo e alguns outro macetes. Até a próxima!
