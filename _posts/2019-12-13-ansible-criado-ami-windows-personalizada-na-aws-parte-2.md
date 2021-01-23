---
layout: post
title: 'Ansible: Criado AMI Windows personalizada na AWS (Parte 2)'
subtitle: Criando Windows personalizado e gerando AMI com Ansible
description: Na [parte 1](https://sidneiweber.com.br/ansible-criado-ami-windows-personalizada-na-aws-parte-1/) aprendemos como usar um script AWS User Data para configurar uma senha de Administrador e configurar o WinRM no Windows. Agora que sabemos como criar uma instância setando um senha especifica, vamos ao restante dos procedimentos.  Vamos estruturar nosso projeto e manter as coisas organizadas.
date: '2019-12-27 17:04:43'
tags: [aws, ansible, windows]
image: "/assets/img/aws-ami/ansible-aws.png"
---

Na [parte 1](https://sidneiweber.com.br/ansible-criado-ami-windows-personalizada-na-aws-parte-1/) aprendemos como usar um script AWS User Data para configurar uma senha de Administrador e configurar o WinRM no Windows. Agora que sabemos como criar uma instância setando um senha especifica, vamos ao restante dos procedimentos.  Vamos estruturar nosso projeto e manter as coisas organizadas.

Recursos utilizados, caso não tenha algo instalado, não funcionará :

**Python 3.8.0**<br />
**Módulos pip**:<br />
* boto<br />
* boto3<br />
* pywinrm
 
 **Ansible 2.9.2**

Já podemos supor que você tenha o Ansible configurado corretamente para sua conta da AWS (por exemplo, boto instalado, credenciais do IAM configuradas). Consulte o Guia da AWS da Ansible se precisar de ajuda para fazer isso. Por simplicidade, esses exemplos também pressupõem que você tenha uma VPC padrão funcional em sua região (você deve ter, a menos que a tenha excluído). Se você precisar de ajuda para configurar isso, consulte a página da Amazon em VPCs padrão.

Caso queira ir direto para os arquivos usados, pode acessar no github: [https://github.com/sidneiweber/ansible-windows-ami](https://github.com/sidneiweber/ansible-windows-ami)

Vamos iniciar pelas nossas variáveis, onde vamos setar a região da AWS, o tipo de instância, nossa chave, vpc e subnet, nossa senha que usamos na [primeira parte ](https://sidneiweber.com.br/ansible-criado-ami-windows-personalizada-na-aws-parte-1/) do artigo e alguns detalhes sobre os volumes:

```yaml
# cat group_vars/all.yml
target_aws_region: us-east-1
instance_type: t3.small
keypair: keypair
vpc_id: vpc-xxxxx
subnet: subnet-xxxxx
win_initial_password: myTempPassword123!
volumes:
  - device_name: /dev/sda1
    device_type: gp2
    volume_size: 30
    delete_on_termination: true
```

Nosso arquivo hosts ficará assim. O grupo win é onde será adicionada a instância após a criação: <br />

```yml
localhost ansible_connection=local

[win]

[win:vars]
ansible_connection=winrm
ansible_ssh_port=5986
ansible_ssh_user=Administrator
ansible_ssh_pass="{{ win_initial_password }}"
ansible_winrm_server_cert_validation=ignore
```

Com essas váriaveis em mãos, vamos iniciar nossa instância base já usando o userdata assim como fizemos no painel da AWS, só que dessa vez diretamente pelo ansible: <br />

<script src="https://gist.github.com/sidneiweber/d229e9fc41249683f505dc4566566e18.js"></script>

Agora vamos conectar na instância e fazer a instalação do que precisamos, vamos contar com auxilio de um script para instalar o Chocolatey e algumas ferramentas (JDK e git) somente para exemplo. <br />
Vamos também instalar algumas features do Windows como IIS, Powershell e .NET Framework, também somente para aprendizado. Também usaremos o módulo do Chocolatey para instalar o 7zip. <br />

<script src="https://gist.github.com/sidneiweber/66df2a3f64afd13054b0f46c374be344.js"></script>

<script src="https://gist.github.com/sidneiweber/355aef53cef5d3830b7ebae241011250.js"></script>

Agora vamos gerar nossa AMI personalizada, lembrando que o nome deve ser sempre diferente ao gerar uma nova AMI, aqui é interessante incluir uma variável com o número do build do seu pipeline por exemplo: <br />

<script src="https://gist.github.com/sidneiweber/d7d3704c942ef1baf4d25995d96be36a.js"></script>

Para não ficarmos com essa instância base rodando sem necessidade, vamos exclui-la: <br />

<script src="https://gist.github.com/sidneiweber/9b3d8791ad11cf0a7ad798446b58b6d1.js"></script>

Então nosso arquivo principal para realizarmos essa tarega ficará assim: <br />

<script src="https://gist.github.com/sidneiweber/a59cfe0e7de5e2d410b8cdf0c2030528.js"></script>

E para rodar tudo e ser feliz basta executar: ***ansible-playbook -i hosts deploy.yml***

**Iniciando a execução:**

![Iniciando Instância](/assets/img/aws-ami/1.png)

**Instância rodando na AWS:**

![Instância iniciada](/assets/img/aws-ami/5.png)

**Instalando aplicações e configurações:**

![Realizando deploy das aplicações](/assets/img/aws-ami/2.png)

**Gerando a AMI e encerrando a instância base:**

![Gerando a AMI e encerrando instância](/assets/img/aws-ami/3.png)

**AMI gerada no painel da AWS:**

![AMI gerada](/assets/img/aws-ami/6.png)

**Resumo das execuções no Ansible:**

![Resumo das execuções](/assets/img/aws-ami/4.png)


Referencia: http://blog.rolpdog.com/2015/09/manage-stock-windows-amis-with-ansible_3.html
