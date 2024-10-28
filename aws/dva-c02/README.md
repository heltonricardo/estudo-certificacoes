# DVA-C02 - AWS Certified Developer – Associate

[Voltar para a página principal](../../README.md)

<img src="assets/badge.png" alt="DVA-C02 - AWS Certified Developer – Associate" width="200"/>

<!-- TOC -->

- [1. Conta AWS e IAM](#1-conta-aws-e-iam)
  - [1.1. Conta AWS](#11-conta-aws)
  - [1.2. IAM: Identity and Access Management](#12-iam-identity-and-access-management)
  - [1.3. Custos](#13-custos)
  - [1.4. Assumindo um papel](#14-assumindo-um-papel)
  - [1.5. STS: Security Token Service](#15-sts-security-token-service)
  - [1.6. Access Control Methods](#16-access-control-methods)
- [2. CLI: Command Line Interface](#2-cli-command-line-interface)
  - [2.1. Comandos](#21-comandos)
  - [2.2. Arquivos importantes](#22-arquivos-importantes)
  - [2.3. Assumindo um papel](#23-assumindo-um-papel)
- [3. VPC, EC2 e ELB](#3-vpc-ec2-e-elb)
  - [3.1. VPC: Virtual Private Cloud](#31-vpc-virtual-private-cloud)
    - [3.1.1. Grupos de Segurança e NACLs](#311-grupos-de-seguran%C3%A7a-e-nacls)
  - [3.2. EC2: Elastic Compute Cloud](#32-ec2-elastic-compute-cloud)
    - [3.2.1. EBS: Elastic Block Store](#321-ebs-elastic-block-store)
    - [3.2.2. Instance Stores](#322-instance-stores)
    - [3.2.3. EFS: Elastic File System](#323-efs-elastic-file-system)
      - [3.2.3.1. Classes de armazenamento](#3231-classes-de-armazenamento)
      - [3.2.3.2. Desempenho](#3232-desempenho)
    - [3.2.4. Metadata e User Data](#324-metadata-e-user-data)
    - [3.2.5. Access Keys e IAM Roles](#325-access-keys-e-iam-roles)
    - [3.2.6. Auto Scaling](#326-auto-scaling)
      - [3.2.6.1. ASG: Auto Scaling Groups](#3261-asg-auto-scaling-groups)
    - [3.2.7. ECB: Elastic Load Balancing](#327-ecb-elastic-load-balancing)
- [4. Amazon S3 e CloudFront](#4-amazon-s3-e-cloudfront)
  - [4.1. S3: Simple Storage Service](#41-s3-simple-storage-service)

<!-- /TOC -->

## 1. Conta AWS e IAM

### 1.1. Conta AWS

A conta root em AWS é a conta de administrador principal, com acesso total a todos os serviços e recursos da AWS. No entanto, recomenda-se usá-la apenas para criar usuários, grupos, políticas e papéis, e não para atividades do dia a dia.

- **Usuário (User):** Entidade com permissões específicas dentro da AWS. Eles representam pessoas ou aplicações que precisam de acesso aos recursos AWS.

- **Grupo (Group):** Coleção de usuários. Permissões são aplicadas ao grupo, e todos os usuários dentro dele herdam essas permissões.

- **Política (Policy):** Define permissões e especifica quais ações são permitidas ou negadas em quais recursos. Elas são escritas em formato JSON.

- **Papéis (Role):** Semelhante a um usuário, mas não é associada a uma pessoa específica. São usados para conceder permissões temporárias a usuários ou serviços que precisem acessar recursos.

### 1.2. IAM: Identity and Access Management

O IAM é usado para gerenciar quem pode acessar os recursos AWS e de que forma. Ele permite a autenticação e autorização via API, console, e CLI, usando diferentes entidades chamadas principals.

### 1.3. Custos

Para uma gestão eficaz dos recursos na AWS, é crucial compreender e utilizar ferramentas que ajudem a monitorar e otimizar os custos dos serviços.

- **Budget:** Refere-se à criação e gerenciamento de orçamentos na AWS, onde você define limites de gastos e configura alertas para monitorar o uso e os custos dos serviços.

- **Cost Explorer:** É uma ferramenta usada para analisar os custos e o uso dos serviços na AWS. Permite visualizar tendências de gastos ao longo do tempo e identificar áreas onde os custos podem ser otimizados.

### 1.4. Assumindo um papel

1. Crie um role (AWS Account para o exemplo). Acesse-o o role e copie o ARN (algo como `arn:aws:iam::123/role/nome-role`).

2. Acesse o cadastro do usuário e adicione uma permissão inline JSON para ele:

   ```
   {
     "Version": "2012-10-17",
     "Statement": {
       "Effect": "Allow",
       "Action": "sts:AssumeRole",
       "Resource": "arn:aws:iam::123/role/nome-role"
     }
   }
   ```

   > Ela permite que o usuário troque de papéis temporariamente.

3. Acesse o role criado e copie o link para troca de papéis. Faça login via IAM de um usuário e acesse esse link. Algumas informações já estarão preenchidas. Basta clicar em trocar para ter acesso aos serviços especificados no role.

### 1.5. STS: Security Token Service

Serviço que fornece credenciais temporárias para aplicações acessarem outras aplicações.

### 1.6. Access Control Methods

- **Role-Based Access Control (RBAC):** Atribui permissões com base nas funções dos usuários dentro de uma organização, facilitando a gestão de acesso em grandes ambientes.

- **Attribute-Based Access Control (ABAC):** Oferece uma abordagem mais flexível e dinâmica, utilizando tags e múltiplos atributos (como localização e horário) para tomar decisões de acesso em tempo real.

## 2. CLI: Command Line Interface

O AWS CLI é uma ferramenta de linha de comando para gerenciar serviços da AWS. Permite automatizar tarefas, configurar recursos e realizar operações diretamente do terminal. Você pode instalá-lo usando pip ou gerenciadores de pacotes e executar comandos no formato `aws [serviço] [operação]`.

### 2.1. Comandos

- `aws help`: Apresenta ajuda sobre os serviços disponíveis;
- `aws ec2 help`: Apresenta ajuda sobre os comandos disponíveis para o serviço EC2;

---

- `aws configure`: Configura credenciais **default** de acesso AWS;
- `aws configure --profile nome-perfil`: Configura credenciais de acesso AWS no perfil especificado;

---

- `aws s3 ls`: Lista todos os buckets S3;
- `aws s3 mb s3://my-bucket`: Cria o bucket **my-bucket**;
- `aws s3 cp arquivo.txt s3://my-bucket`: Faz o upload do **arquivo.txt** para o bucket **my-bucket**;
- `aws s3 ls s3://my-bucket`: Lista os arquivos no bucket **my-bucket**;
- `aws s3 rb s3://my-bucket`: Remove o bucket **my-bucket** (não apaga bucket com conteúdo);
- `aws s3 rb s3://my-bucket --force`: Remove o bucket **my-bucket** mesmo com conteúdo;

---

- `aws ec2 describe-instances`: Mostra detalhes das instâncias EC2.

> [!IMPORTANT]
> Sempre que os comandos são executados, o perfil usado é o **default** a menos que especifiquemos um usando: `aws comando --profile nome-perfil`.

### 2.2. Arquivos importantes

- `.aws/config`: Contém configurações, como região especificada;
- `.aws/credentials`: Contém os dados da credencial em texto sem criptografia.

> [!NOTE]
> No Linux: o diretório `.aws` está onde os arquivos de instalação foram descompactados;
>
> No Windows: o diretório `.aws` está na pasta `C:\Users\User`.

### 2.3. Assumindo um papel

Copiar o código ARN do papel em IAM > Roles > NomeRole (algo como `arn:aws:iam::123/role/nome-role`) e colar usando este template no arquivo `.aws/config`:

```
[profile nome-role]
    role_arn = arn:aws:iam::123/role/nome-role
    source_profile = default
```

## 3. VPC, EC2 e ELB

### 3.1. VPC: Virtual Private Cloud

VPC é uma porção logicamente isolada dentro de uma região da AWS. Ela é uma rede virtual dedicada à sua conta AWS, equivalente a ter um datacenter próprio dentro da infraestrutura da AWS. Com a VPC, temos controle total sobre quem pode acessar os recursos internos, configurando regras de segurança e roteamento de acordo com as necessidades. Por padrão, é possível criar até 5 VPCs por região.

Dentro de uma VPC, existem **Zonas de Disponibilidade** (Availability Zones), que são unidades de isolamento físico para aumentar a resiliência da infraestrutura. Essas zonas são subdivididas em **subnets** (sub-redes), que podem ser classificadas como públicas ou privadas. As **subnets públicas** são acessíveis externamente, permitindo a comunicação com a Internet, enquanto as **subnets privadas** são isoladas e não possuem acesso direto à Internet. Os recursos, como instâncias EC2 e bancos de dados, são implantados dentro dessas subnets.

Para controlar o tráfego dentro da VPC, há um roteador interno que utiliza uma **tabela de roteamento** para definir como o tráfego deve ser encaminhado. Na "borda" da VPC, encontra-se o **Internet Gateway**, que é necessário para permitir que as instâncias dentro das subnets públicas acessem a Internet.

![](assets/2024-10-24-15-13-03.png)

É possível criar várias VPCs em uma única região, e cada uma delas deve ter um bloco de endereços IP exclusivo, definido em formato **CIDR (Classless Inter-Domain Routing)**, que especifica o intervalo de endereços IP disponíveis. Dentro da VPC, cada subnet também possui seu próprio endereço IP CIDR, garantindo isolamento e segmentação de rede.

![](assets/2024-10-24-15-18-56.png)

**Conexões e Componentes Adicionais**

- **Peering Connection:** Uma conexão direta entre duas VPCs, permitindo que elas se comuniquem como se estivessem na mesma rede.
- **NAT Instance:** Uma instância que habilita o acesso à Internet para instâncias EC2 em subnets privadas, gerenciada por você.
- **NAT Gateway:** Similar à NAT Instance, porém gerenciada pela AWS, fornecendo acesso à Internet para instâncias em subnets privadas de forma mais escalável.
- **Virtual Private Gateway:** O lado da VPC que faz parte de uma conexão de VPN, usada para conectar a rede local do cliente à VPC da AWS.
- **Customer Gateway:** O lado do cliente de uma conexão de VPN, representando o dispositivo de borda que se conecta à VPC.
- **AWS Direct Connect:** Uma conexão de rede privada de alta velocidade e alta largura de banda, que liga a rede do cliente diretamente à AWS, sem passar pela Internet pública.
- **Security Group:** Um firewall a nível de instância, que controla o tráfego de entrada e saída para os recursos implantados.
- **Network ACL (Access Control List):** Um firewall a nível de subnet, que controla o tráfego para e a partir das subnets na VPC.

#### 3.1.1. Grupos de Segurança e NACLs

Os Network ACLs (NACLs) e Grupos de Segurança são firewalls usados para proteger o tráfego na VPC:

- **Network ACLs:** Aplicadas no nível da subnet, controlam o tráfego que entra e sai. Permitem ou negam o tráfego com base em regras de portas, protocolos e IPs.

- **Grupos de Segurança:** Aplicados no nível da instância, controlam o tráfego permitido para recursos específicos. Um mesmo grupo pode ser usado em instâncias de diferentes subnets.

![](assets/2024-10-24-16-28-30.png)

### 3.2. EC2: Elastic Compute Cloud

EC2 é um serviço essencial da AWS que oferece servidores virtuais. A AWS gerencia os hosts físicos, enquanto nós gerenciamos as instâncias, que podem executar Windows, Linux ou macOS.

O EC2 é um tipo de IaaS (Infrastructure as a Service), permitindo que você escolha atributos de hardware para cada instância e instale suas aplicações. Cada instância opera dentro de uma VPC (Virtual Private Cloud).

No Amazon EC2, as instâncias operam com três tipos de endereços IP:

- **IP Público:** Acessível pela Internet, mas é dinâmico e pode mudar se a instância for parada e iniciada novamente.

- **IP Privado:** Usado para comunicação interna entre instâncias na mesma VPC. Para que uma instância com IP privado acesse a Internet, é necessária a configuração de um NAT (Network Address Translation), que permite a tradução do IP privado para um IP público.

- **IP Elástico:** Um IP público estático que você pode associar a uma instância. Ao contrário do IP público dinâmico, o IP elástico não é perdido quando a instância é desligada, garantindo que você mantenha o mesmo endereço IP mesmo após reinicializações.

![](assets/2024-10-24-21-21-08.png)

#### 3.2.1. EBS: Elastic Block Store

O EBS oferece volumes de armazenamento para instâncias EC2. Esses volumes são um sistema de armazenamento em bloco, diferente do armazenamento em arquivo, e existem dentro de uma Zona de Disponibilidade (AZ).

![](assets/2024-10-24-21-45-10.png)

#### 3.2.2. Instance Stores

As instâncias EC2 também possuem instance store volumes, que são fisicamente conectados aos hosts EC2. Esses volumes oferecem alta performance, mas os dados não são persistidos após o desligamento da instância.

![](assets/2024-10-24-21-50-29.png)

Os backups do EBS são chamados de snapshots, que são armazenados no S3 (um serviço da AWS na mesma região) e não na AZ. Os snapshots são incrementais, ou seja, só fazem backup das alterações desde o último snapshot. A partir de um snapshot, você pode criar um novo volume EBS ou uma Amazon Machine Image (AMI), que permite lançar instâncias pré-configuradas rapidamente.

![](assets/2024-10-24-21-59-24.png)

#### 3.2.3. EFS: Elastic File System

O EFS é um sistema de arquivos compartilhado que permite que múltiplas instâncias EC2 se conectem a ele, mesmo em diferentes Zonas de Disponibilidade (AZs). As instâncias se conectam a um ponto de montagem na AZ, utilizando o protocolo NFS (Network File System), que é compatível apenas com Linux.

![](assets/2024-10-24-22-31-00.png)

Para sistemas de arquivos regionais, as operações de gravação são duravelmente armazenadas em várias AZs, e aplicações clientes NFS podem usar bloqueios de arquivo NFS v4 para garantir consistência durante leituras e gravações.

##### 3.2.3.1. Classes de armazenamento

- **EFS Standard:** Usando SSDs para baixa latência.
- **EFS Infrequent Access (IA):** Uma opção econômica para dados menos acessados.
- **EFS Archive:** A opção mais barata para dados arquivados.

> Todas as classes oferecem 99,999999999% de durabilidade.

É possível replicar um sistema de arquivos em outra região para recuperação de desastres, com RPO/RTO em minutos. Vários pontos de montagem podem ser criados na réplica, mas apenas como somente leitura. Também é viável conectar computadores on-premises a esses sistemas, desde que utilizem o EFS.

![](assets/2024-10-24-22-38-17.png)

O EFS integra-se com o AWS Backup para backups automáticos do sistema de arquivos.

##### 3.2.3.2. Desempenho

Em termos de desempenho, existem duas opções:

- **Provisioned Throughput:** Permite especificar um nível de throughput independente do tamanho do sistema de arquivos.
- **Bursting Throughput:** O throughput escala com a quantidade de armazenamento, permitindo picos de desempenho conforme necessário.

> Throughput: quantidade de dados que pode ser processada ou transferida em um determinado período de tempo.

#### 3.2.4. Metadata e User Data

- **EC2 Metadata**: Informações sobre a instância EC2, como ID, IP etc.
  - **IMDSv1**: Método antigo e menos seguro.
  - **IMDSv2**: Requer uso de token para maior segurança.
- **User Data**: Script executado automaticamente na primeira inicialização da instância.
  - Deve ser codificado em **base64** (feito automaticamente no console e AWS CLI).
  - Limite de **16 KB** em formato bruto (antes de ser codificado).
  - Executado apenas **uma vez**, no primeiro boot.

#### 3.2.5. Access Keys e IAM Roles

AWS Access Keys são usadas na CLI e têm as mesmas permissões do usuário IAM. O problema é que são credenciais de longo prazo, armazenadas em texto simples na instância, o que aumenta o risco de comprometimento. Para evitar isso, use IAM Roles com políticas atribuídas, que não são armazenadas na instância. O serviço utiliza o STS da AWS para obter tokens temporários.

#### 3.2.6. Auto Scaling

EC2 Auto Scaling ajusta automaticamente a quantidade de instâncias, substituindo ou adaptando a capacidade de clusters para atender à demanda. Ele é compatível com EC2, ECS e EKS, e se integra a outros serviços como CloudWatch (monitoramento e escalonamento), ELB (balanceamento de carga), EC2 Spot Instances (otimização de custo) e VPC (deploy entre AZs).

![](assets/2024-10-28-14-44-13.png)

O escalonamento é horizontal (scale-out), proporcionando elasticidade e escalabilidade, aumentando a capacidade quando necessário e reduzindo quando possível. Possui health checks para EC2 e ELB, além de um período de espera (grace period) antes de iniciar operações. Existem quatro modos de escalonamento: manual, dinâmico (sob demanda), preditivo (usando ML) e agendado.

##### 3.2.6.1. ASG: Auto Scaling Groups

Auto Scaling Groups permitem a criação e gerenciamento automáticos de grupos de instâncias EC2, ajustando a capacidade de acordo com a demanda. Com ASG, é possível configurar políticas de escalabilidade para aumentar ou reduzir o número de instâncias, promovendo alta disponibilidade e otimização de custos. ASG monitora o estado das instâncias com health checks e, se necessário, substitui instâncias com falhas automaticamente. Ele suporta escalonamento manual, dinâmico, preditivo e agendado, atendendo tanto a picos de uso quanto a demandas mais previsíveis.

#### 3.2.7. ECB: Elastic Load Balancing

Amazon ELB (Elastic Load Balancing) oferece alta disponibilidade e tolerância a falhas, permitindo que múltiplas instâncias fiquem atrás de um único endpoint. Ele distribui o tráfego de forma transparente entre EC2, ECS, endereços IP, Lambda e outros balanceadores. Se uma instância falhar, o ELB redireciona automaticamente a sessão para outra instância disponível.

![](assets/2024-10-28-15-08-45.png)
**Tipos de Load Balancer:**

- **Application Load Balancer (ALB):** Opera na camada de aplicação (HTTP/HTTPS) e permite roteamento avançado com base em caminhos, hosts, parâmetros de consulta e endereços IP de origem.

- **Network Load Balancer (NLB):** Opera na camada de transporte (TCP/UDP) e usa roteamento baseado no protocolo IP, oferecendo latência ultrabaixa para conexões de alto desempenho.

- **Gateway Load Balancer (GLB):** Ideal para implantar, escalar e gerenciar appliances de terceiros (como firewalls e sistemas de detecção de intrusão) em redes VPC. Combina roteamento com um modelo de encaminhamento que facilita a implementação de soluções de segurança em larga escala.

![](assets/2024-10-28-15-18-56.png)

## 4. Amazon S3 e CloudFront

### 4.1. S3: Simple Storage Service

O Amazon S3 é um serviço de armazenamento de objetos, onde cada bucket funciona como um contêiner para guardar arquivos de qualquer tipo, com capacidade para milhões de objetos. Com ótimo custo-benefício, ele permite gerenciar objetos por meio de métodos HTTP como GET, POST e DELETE e pode ser acessado globalmente pela internet via HTTPS.

Formas de acessar um objeto (key) em um bucket: \
![](assets/2024-10-28-16-17-31.png)

> Cada objeto no S3 possui uma key (nome), ID de versão, conteúdo (valor), metadados e informações de controle de acesso.

Como o S3 está fora de redes privadas (VPCs) da AWS, conexões de instâncias EC2 ao S3 geralmente requerem acesso à internet por meio de um Internet Gateway. Para evitar isso, é possível configurar um S3 Gateway Endpoint, que permite o acesso ao S3 diretamente através de endereços privados, mantendo as conexões dentro da rede da AWS.

![](assets/2024-10-28-16-31-09.png)

> File storage x Object storage
>
> File storage organiza dados em diretórios hierárquicos e é montado no sistema operacional, aparecendo como uma unidade de disco (exemplo: EFS no AWS). A conexão é persistente, permitindo acesso imediato aos arquivos.
>
> Object storage armazena dados em buckets, sem hierarquia real (flat namespace). Nomes com pontos ou prefixos podem simular diretórios, mas não formam uma estrutura de pastas. O acesso é feito via API REST, e não é possível montar o storage como uma unidade de disco.
