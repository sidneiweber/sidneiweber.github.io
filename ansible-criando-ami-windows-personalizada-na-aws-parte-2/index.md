# Ansible: Criando AMI Windows Personalizada Na AWS (Parte 2)


Na [parte 1](https://sidneiweber.com.br/ansible-criando-ami-windows-personalizada-na-aws-parte-1/) aprendemos como usar um script AWS User Data para configurar uma senha de Administrador e configurar o WinRM no Windows. Agora que sabemos como criar uma instância setando um senha especifica, vamos ao restante dos procedimentos.  Vamos estruturar nosso projeto e manter as coisas organizadas.

Recursos utilizados, caso não tenha algo instalado, não funcionará :

**Python 3.8.0**&lt;br /&gt;
**Módulos pip**:&lt;br /&gt;
* boto&lt;br /&gt;
* boto3&lt;br /&gt;
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

Nosso arquivo hosts ficará assim. O grupo win é onde será adicionada a instância após a criação: &lt;br /&gt;

```yml
localhost ansible_connection=local

[win]

[win:vars]
ansible_connection=winrm
ansible_ssh_port=5986
ansible_ssh_user=Administrator
ansible_ssh_pass=&#34;{{ win_initial_password }}&#34;
ansible_winrm_server_cert_validation=ignore
```

Com essas váriaveis em mãos, vamos iniciar nossa instância base já usando o userdata assim como fizemos no painel da AWS, só que dessa vez diretamente pelo ansible: &lt;br /&gt;

```yml
# cat roles/launch/tasks/main.yml
- name: Find Windows AMI base in this region
  ec2_ami_facts:
    owners: 801119661308
    filters:
      name: Windows_Server-2019-English-Full-Base*
  register: found_amis

- name: Get AMI Windows
  set_fact:
    win_ami_id: &#34;{{ (found_amis.images | first).image_id  }}&#34;

- name: Ensure security group is present
  ec2_group:
    name: WinRM RDP
    description: Inbound WinRM and RDP
    region: &#34;{{ target_aws_region }}&#34;
    vpc_id: &#34;{{ vpc_id }}&#34;
    rules:
    - proto: tcp
      from_port: 80
      to_port: 80
      cidr_ip: 0.0.0.0/0
    - proto: tcp
      from_port: 5986
      to_port: 5986
      cidr_ip: 0.0.0.0/0
    - proto: tcp
      from_port: 3389
      to_port: 3389
      cidr_ip: 0.0.0.0/0
    rules_egress:
    - proto: -1
      cidr_ip: 0.0.0.0/0
  register: sg_out

- name: Ensure instances are running
  ec2:
    region: &#34;{{ target_aws_region }}&#34;
    image: &#34;{{ win_ami_id }}&#34;
    instance_type: &#34;{{ instance_type }}&#34;
    group_id: &#34;{{ sg_out.group_id }}&#34;
    key_name: &#34;{{ keypair }}&#34;
    wait: yes
    wait_timeout: 500
    exact_count: 1
    assign_public_ip: yes
    vpc_subnet_id: &#34;{{ subnet }}&#34;
    count_tag:
      Name: stock-win-ami-test
    instance_tags:
      Name: stock-win-ami-test
    user_data: &#34;{{ lookup(&#39;template&#39;, &#39;userdata.txt.j2&#39;) }}&#34;
  register: ec2_result

- name: wait for WinRM to answer on all hosts
  wait_for:
    port: 5986
    host: &#34;{{ item.public_ip }}&#34;
    delay: 30
    timeout: 300
    state: started
  with_items: &#34;{{ ec2_result.tagged_instances }}&#34;

- name: add hosts to groups
  add_host:
    name: &#34;win-temp-{{ item.id }}&#34;
    ansible_ssh_host: &#34;{{ item.public_ip }}&#34;
    ec2_id: &#34;{{ item.id }}&#34;
    groups: win
  changed_when: false
  with_items: &#34;{{ ec2_result.tagged_instances }}&#34;
```

Agora vamos conectar na instância e fazer a instalação do que precisamos, vamos contar com auxilio de um script para instalar o Chocolatey e algumas ferramentas (JDK e git) somente para exemplo. &lt;br /&gt;
Vamos também instalar algumas features do Windows como IIS, Powershell e .NET Framework, também somente para aprendizado. Também usaremos o módulo do Chocolatey para instalar o 7zip. &lt;br /&gt;

```yml
# cat roles/deploy/tasks/main.yml
- name: Copy Script config
  win_copy:
    src: script.ps1
    dest: C:\Windows\Temp\script.ps1

- name: Execute script
  win_shell: C:\Windows\Temp\script.ps1

- name: ensure IIS and ASP.NET are installed
  win_feature:
    name:
      - Web-Server
      - Web-Http-Redirect
      - Web-DAV-Publishing
      - Web-Custom-Logging
      - Web-Log-Libraries
      - Web-ODBC-Logging
      - Web-Request-Monitor
      - Web-Http-Tracing
      - Web-Dyn-Compression
      - Web-Basic-Auth
      - Web-CertProvider
      - Web-Client-Auth
      - Web-Digest-Auth
      - Web-Cert-Auth
      - Web-IP-Security
      - Web-Url-Auth
      - Web-Windows-Auth
      - Web-App-Dev
      - Web-Net-Ext
      - Web-Net-Ext45
      - Web-Asp-Net45
      - Web-ISAPI-Ext
      - Web-ISAPI-Filter
      - Web-Mgmt-Tools
      - Web-Scripting-Tools
      - Web-Mgmt-Console
      - Web-Mgmt-Service
      - NET-Framework-Features
      - NET-Framework-Core
      - NET-HTTP-Activation
      - NET-Non-HTTP-Activ
      - NET-Framework-45-Features
      - NET-Framework-45-Core
      - NET-Framework-45-ASPNET
      - NET-WCF-Services45
      - MSMQ
      - MSMQ-Services
      - MSMQ-Server
      - FS-SMB1
      - Telnet-Client
      - PowerShellRoot
      - PowerShell
      - PowerShell-V2
      - PowerShell-ISE
      - WAS
      - WAS-Process-Model
      - WAS-NET-Environment
      - WAS-Config-APIs
      - WoW64-Support
    state: present
    include_management_tools: yes
  register: windows_install

- name: Reboot if installing Web-Server feature requires it
  win_reboot:
  when: windows_install.reboot_required

- name: Install 7Zip
  win_chocolatey:
    name: 7zip
    state: present
    
- debug:
    msg: web application is available at http://{{ ansible_ssh_host }}/
```

```yml
# cat roles/deploy/files/script.ps1
# Install Chocolatey
iex ((New-Object System.Net.WebClient).DownloadString(&#39;https://chocolatey.org/install.ps1&#39;))
# Globally Auto confirm every action
choco feature enable -n allowGalobalConfirmation

# Install JDK 8 and git
choco install jdk8
choco install git
```

Agora vamos gerar nossa AMI personalizada, lembrando que o nome deve ser sempre diferente ao gerar uma nova AMI, aqui é interessante incluir uma variável com o número do build do seu pipeline por exemplo: &lt;br /&gt;

```yml
# cat roles/build-ami/tasks/main.yml
- name: Create AMI
  ec2_ami:
    region: &#34;{{ target_aws_region }}&#34;
    instance_id: &#34;{{ item.id }}&#34;
    name: &#34;windows-personalizado&#34;
    wait: yes
    state: present
  with_items: &#34;{{ ec2_result.tagged_instances }}&#34;
  register: ami

- name: Set New AMI id variable
  set_fact:
    ami_result: &#34;{{ (ami.results | first).image_id  }}&#34;
```

Para não ficarmos com essa instância base rodando sem necessidade, vamos exclui-la: &lt;br /&gt;

```yml
# cat roles/terminate/tasks/main.yml
- name: ensure instances are not running
  ec2:
    region: &#34;{{ target_aws_region }}&#34;
    image: &#34;{{ win_ami_id }}&#34;
    instance_type: &#34;{{ instance_type }}&#34;
    group_id: &#34;{{ sg_out.group_id }}&#34;
    key_name: &#34;{{ keypair }}&#34;
    wait: yes
    wait_timeout: 500
    exact_count: 0
    assign_public_ip: yes
    vpc_subnet_id: &#34;{{ subnet }}&#34;
    count_tag:
      Name: stock-win-ami-test
    instance_tags:
      Name: stock-win-ami-test
  register: ec2_result
```

Então nosso arquivo principal para realizarmos essa tarega ficará assim: &lt;br /&gt;

```yml
# cat deploy.yml
- hosts: localhost
  gather_facts: no
  roles:
    - role: launch
      name: win

- hosts: win
  roles:
    - deploy

- hosts: localhost
  gather_facts: no
  connection: local
  roles:
    - build-ami
    - terminate
```

E para rodar tudo e ser feliz basta executar: ***ansible-playbook -i hosts deploy.yml***

**Iniciando a execução:**

![Iniciando Instância](/img/aws-ami/1.png)

**Instância rodando na AWS:**

![Instância iniciada](/img/aws-ami/5.png)

**Instalando aplicações e configurações:**

![Realizando deploy das aplicações](/img/aws-ami/2.png)

**Gerando a AMI e encerrando a instância base:**

![Gerando a AMI e encerrando instância](/img/aws-ami/3.png)

**AMI gerada no painel da AWS:**

![AMI gerada](/img/aws-ami/6.png)

**Resumo das execuções no Ansible:**

![Resumo das execuções](/img/aws-ami/4.png)


Referencia: http://blog.rolpdog.com/2015/09/manage-stock-windows-amis-with-ansible_3.html


---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/ansible-criando-ami-windows-personalizada-na-aws-parte-2/  

