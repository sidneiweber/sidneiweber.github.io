# Reduzindo Custos Na AWS (EC2) - Parte 1


A redução de custos no ambiente de nuvem é um assunto constante, a utlização é simples porém o desperdício de recursos pode ocorrer com bastante facilidade. Para te ajudar vou dividir as dicas em três partes, dividindo em EC2, ECS e RDS, três serviços distintos da [AWS](https://aws.amazon.com/pt/).

Na primeira parte começaremos com o EC2, que permite a criação de instâncias (&#34;máquinas virtuais&#34;) com facilidade, podendo ser usado tanto com Windows, quanto com Linux. Bom pra quem ainda não sabe, os recursos da AWS são cobrados por uso, então quando criamos uma instância no EC2, ela será cobrada pelo tempo que estiver ligada e veria de valor dependendo da [tipo de instância escolhida](https://aws.amazon.com/pt/ec2/instance-types/).

Bom a dica pode ser usada por quem utiliza os recursos EC2 durante o expediente de trabalho, seja em produção, que precise estar funcionando somente no horário de trabalho ou ambientes de desenvolvimento, que geralmente são usados por um determinado periodo do dia. A gente irá programar o start/stop dessas instâncias. Iremos utlizar funções [Lambdas](https://aws.amazon.com/pt/lambda/) combinadas com [eventos do Cloudwatch](https://docs.aws.amazon.com/pt_br/AmazonCloudWatch/latest/events/WhatIsCloudWatchEvents.html).

Precisaremos de uma função IAM com permissão para acessar os recursos EC2. Pode usar o nome que achar melhor. Aqui vai uma colinha da política, lembrando que a função precisa ser configurada com o serviço Lambda:
```json
{
    &#34;Version&#34;: &#34;2012-10-17&#34;,
    &#34;Statement&#34;: [
        {
            &#34;Sid&#34;: &#34;VisualEditor0&#34;,
            &#34;Effect&#34;: &#34;Allow&#34;,
            &#34;Action&#34;: [
                &#34;ec2:StartInstances&#34;,
                &#34;ec2:StopInstances&#34;,
                &#34;logs:PutLogEvents&#34;
            ],
            &#34;Resource&#34;: [
                &#34;arn:aws:logs:*:*:log-group:*:*:*&#34;,
                &#34;arn:aws:ec2:*:*:instance/*&#34;
            ]
        },
        {
            &#34;Sid&#34;: &#34;VisualEditor1&#34;,
            &#34;Effect&#34;: &#34;Allow&#34;,
            &#34;Action&#34;: [
                &#34;ec2:DescribeInstances&#34;
            ],
            &#34;Resource&#34;: &#34;*&#34;
        },
        {
            &#34;Sid&#34;: &#34;VisualEditor2&#34;,
            &#34;Effect&#34;: &#34;Allow&#34;,
            &#34;Action&#34;: [
                &#34;logs:CreateLogStream&#34;,
                &#34;logs:PutLogEvents&#34;
            ],
            &#34;Resource&#34;: &#34;arn:aws:logs:*:*:log-group:*&#34;
        }
    ]
}
```

Acessando Lambda no Console da AWS, clicaremos em criar uma função:
![Criar função](/img/aws/1.png)

Iremos escolher a opção para criar do zero, escolheremos um nome, a linguagem Python 2.7, usar uma função existente e escolher a função IAM criada anteriormente. A primeira função será para realizar o stop das instâncias.
![](/img/aws/2.png)

No código da função (imagem abaixo) iremos alterar para o seguinte código, lembrando de alterar na linha 3 a região utilizada e na linha 5 os seus Instances IDs, se tiver mais de um basta separar por vírgula:

![](/img/aws/3.png)

```python
import boto3
# Enter the region your instances are in e.g., &#39;eu-west-1&#39;
region = &#39;us-east-1&#39;
# Enter your instance IDs here
instances = [&#39;i-02fb6a97792f0802a&#39;]

def lambda_handler(event, context):
    ec2 = boto3.client(&#39;ec2&#39;, region_name=region)
    ec2.stop_instances(InstanceIds=instances)
    print &#39;Instances are now stopped: &#39; &#43; str(instances)
```

Usandos os mesmos passos já podemos criar a função lambda para iniciar as instâncias, bastando mudar o código da função:
```python
import boto3
# Enter the region your instances are in e.g., &#39;eu-west-1&#39;
region = &#39;us-east-1&#39;
# Enter your instance IDs here
instances = [&#39;i-02fb6a97792f0802a&#39;]

def lambda_handler(event, context):
    ec2 = boto3.client(&#39;ec2&#39;, region_name=region)
    ec2.start_instances(InstanceIds=instances)
    print &#39;Instances started: &#39; &#43; str(instances)
```

Agora vamos a criação do gatilho para acionar os eventos do Cloudwatch. Clicando em adicionar gatilho, vamos escolher a opção Eventos do Cloudwatch.

![](/img/aws/4.png)
![](/img/aws/5.png)

Vamos criar uma nova regra para esse gatilho, dando um nome e escolhendo a Expressão de programação, que é uma expressão Cron. Não esquecendo que esse cron é ajustado para UTC. Podemos adicionar o gatilho

![](/img/aws/6.png)

Faremos o mesmo na função de Start

![](/img/aws/7.png)

E está pronto, nos horários programados as instâncias definidas irão ser desligadas e ligadas, reduzindo o custo nesse tempo que irá permanecer desligadas. Qualquer dúvida ou correção basta deixar nos comentários :).


---

> Autor: Sidnei Weber  
> URL: https://sidneiweber.com.br/reduzindo-custos-na-aws-ec2-parte-1/  

