# DVA-C02 - AWS Certified Developer – Associate

[Voltar para a página principal](../../README.md)

<img src="assets/badge.png" alt="DVA-C02 - AWS Certified Developer – Associate" width="200"/>

<!-- TOC -->

- [1. Conta AWS e IAM](#1-conta-aws-e-iam)
  - [1.1. Conta AWS](#11-conta-aws)
  - [1.2. IAM](#12-iam)
  - [1.3. Custos](#13-custos)
  - [1.4. Assumindo um papel](#14-assumindo-um-papel)
  - [1.5. STS - Security Token Service](#15-sts---security-token-service)
  - [1.6. Access Control Methods](#16-access-control-methods)
- [2. CLI](#2-cli)
  - [2.1. Comandos](#21-comandos)
  - [2.2. Arquivos importantes](#22-arquivos-importantes)
  - [2.3. Assumindo um papel](#23-assumindo-um-papel)
- [3. VPC, EC2 e ELB](#3-vpc-ec2-e-elb)
  - [3.1. VPC](#31-vpc)
    - [3.1.1. Grupos de Segurança e NACLs](#311-grupos-de-seguran%C3%A7a-e-nacls)
  - [3.2. EC2](#32-ec2)
    - [3.2.1. EBS e Instance Stores](#321-ebs-e-instance-stores)

<!-- /TOC -->

## 1. Conta AWS e IAM

### 1.1. Conta AWS

A conta root em AWS é a conta de administrador principal, com acesso total a todos os serviços e recursos da AWS. No entanto, recomenda-se usá-la apenas para criar usuários, grupos, políticas e papéis, e não para atividades do dia a dia.

- **Usuário (User):** Entidade com permissões específicas dentro da AWS. Eles representam pessoas ou aplicações que precisam de acesso aos recursos AWS.

- **Grupo (Group):** Coleção de usuários. Permissões são aplicadas ao grupo, e todos os usuários dentro dele herdam essas permissões.

- **Política (Policy):** Define permissões e especifica quais ações são permitidas ou negadas em quais recursos. Elas são escritas em formato JSON.

- **Papéis (Role):** Semelhante a um usuário, mas não é associada a uma pessoa específica. São usados para conceder permissões temporárias a usuários ou serviços que precisem acessar recursos.

### 1.2. IAM

O IAM (Identity and Access Management) é usado para gerenciar quem pode acessar os recursos AWS e de que forma. Ele permite a autenticação e autorização via API, console, e CLI, usando diferentes entidades chamadas principals.

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

### 1.5. STS - Security Token Service

Serviço que fornece credenciais temporárias para aplicações acessarem outras aplicações.

### 1.6. Access Control Methods

- **Role-Based Access Control (RBAC):** Atribui permissões com base nas funções dos usuários dentro de uma organização, facilitando a gestão de acesso em grandes ambientes.

- **Attribute-Based Access Control (ABAC):** Oferece uma abordagem mais flexível e dinâmica, utilizando tags e múltiplos atributos (como localização e horário) para tomar decisões de acesso em tempo real.

## 2. CLI

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

### 3.1. VPC

**Amazon VPC (Virtual Private Cloud)** é uma porção logicamente isolada dentro de uma região da AWS. Ela é uma rede virtual dedicada à sua conta AWS, equivalente a ter um datacenter próprio dentro da infraestrutura da AWS. Com a VPC, temos controle total sobre quem pode acessar os recursos internos, configurando regras de segurança e roteamento de acordo com as necessidades. Por padrão, é possível criar até 5 VPCs por região.

Dentro de uma VPC, existem **Zonas de Disponibilidade** (Availability Zones), que são unidades de isolamento físico para aumentar a resiliência da infraestrutura. Essas zonas são subdivididas em **subnets** (sub-redes), que podem ser classificadas como públicas ou privadas. As **subnets públicas** são acessíveis externamente, permitindo a comunicação com a Internet, enquanto as **subnets privadas** são isoladas e não possuem acesso direto à Internet. Os recursos, como instâncias EC2 e bancos de dados, são implantados dentro dessas subnets.

Para controlar o tráfego dentro da VPC, há um roteador interno que utiliza uma **tabela de roteamento** para definir como o tráfego deve ser encaminhado. Na "borda" da VPC, encontra-se o **Internet Gateway**, que é necessário para permitir que as instâncias dentro das subnets públicas acessem a Internet.

![](assets/2024-10-24-15-13-03.png)

É possível criar várias VPCs em uma única região, e cada uma delas deve ter um bloco de endereços IP exclusivo, definido em formato **CIDR (Classless Inter-Domain Routing)**, que especifica o intervalo de endereços IP disponíveis. Dentro da VPC, cada subnet também possui seu próprio endereço IP CIDR, garantindo isolamento e segmentação de rede.

![](assets/2024-10-24-15-18-56.png)

**Conexões e Componentes Adicionais**

- **Peering Connection**: Uma conexão direta entre duas VPCs, permitindo que elas se comuniquem como se estivessem na mesma rede.
- **NAT Instance**: Uma instância que habilita o acesso à Internet para instâncias EC2 em subnets privadas, gerenciada por você.
- **NAT Gateway**: Similar à NAT Instance, porém gerenciada pela AWS, fornecendo acesso à Internet para instâncias em subnets privadas de forma mais escalável.
- **Virtual Private Gateway**: O lado da VPC que faz parte de uma conexão de VPN, usada para conectar a rede local do cliente à VPC da AWS.
- **Customer Gateway**: O lado do cliente de uma conexão de VPN, representando o dispositivo de borda que se conecta à VPC.
- **AWS Direct Connect**: Uma conexão de rede privada de alta velocidade e alta largura de banda, que liga a rede do cliente diretamente à AWS, sem passar pela Internet pública.
- **Security Group**: Um firewall a nível de instância, que controla o tráfego de entrada e saída para os recursos implantados.
- **Network ACL (Access Control List)**: Um firewall a nível de subnet, que controla o tráfego para e a partir das subnets na VPC.

#### 3.1.1. Grupos de Segurança e NACLs

Os Network ACLs (NACLs) e Grupos de Segurança são firewalls usados para proteger o tráfego na VPC:

- **Network ACLs:** Aplicadas no nível da subnet, controlam o tráfego que entra e sai. Permitem ou negam o tráfego com base em regras de portas, protocolos e IPs.

- **Grupos de Segurança:** Aplicados no nível da instância, controlam o tráfego permitido para recursos específicos. Um mesmo grupo pode ser usado em instâncias de diferentes subnets.

![](assets/2024-10-24-16-28-30.png)

### 3.2. EC2

O Amazon EC2 (Elastic Compute Cloud) é um serviço essencial da AWS que oferece servidores virtuais. A AWS gerencia os hosts físicos, enquanto nós gerenciamos as instâncias, que podem executar Windows, Linux ou macOS.

O EC2 é um tipo de IaaS (Infrastructure as a Service), permitindo que você escolha atributos de hardware para cada instância e instale suas aplicações. Cada instância opera dentro de uma VPC (Virtual Private Cloud).

No Amazon EC2, as instâncias operam com três tipos de endereços IP:

- **IP Público:** Acessível pela Internet, mas é dinâmico e pode mudar se a instância for parada e iniciada novamente.

- **IP Privado:** Usado para comunicação interna entre instâncias na mesma VPC. Para que uma instância com IP privado acesse a Internet, é necessária a configuração de um NAT (Network Address Translation), que permite a tradução do IP privado para um IP público.

- **IP Elástico:** Um IP público estático que você pode associar a uma instância. Ao contrário do IP público dinâmico, o IP elástico não é perdido quando a instância é desligada, garantindo que você mantenha o mesmo endereço IP mesmo após reinicializações.

![](assets/2024-10-24-21-21-08.png)

#### 3.2.1. EBS e Instance Stores

O EBS (Elastic Block Store) oferece volumes de armazenamento para instâncias EC2. Esses volumes são um sistema de armazenamento em bloco, diferente do armazenamento em arquivo, e existem dentro de uma Zona de Disponibilidade (AZ).

![](assets/2024-10-24-21-45-10.png)

As instâncias EC2 também possuem instance store volumes, que são fisicamente conectados aos hosts EC2. Esses volumes oferecem alta performance, mas os dados não são persistidos após o desligamento da instância.

![](assets/2024-10-24-21-50-29.png)

Os backups do EBS são chamados de snapshots, que são armazenados no S3 (um serviço da AWS na mesma região) e não na AZ. Os snapshots são incrementais, ou seja, só fazem backup das alterações desde o último snapshot. A partir de um snapshot, você pode criar um novo volume EBS ou uma Amazon Machine Image (AMI), que permite lançar instâncias pré-configuradas rapidamente.

![](assets/2024-10-24-21-59-24.png)
