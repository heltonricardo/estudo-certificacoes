# CLF-C01 - AWS Cloud Practitioner

<img src="assets/badge.png" alt="CLF-C01 - AWS Cloud Practitioner" width="200"/>

<!-- TOC tocDepth:2..6 chapterDepth:2..6 -->

- [1. Cloud Computing](#1-cloud-computing)
  - [1.1. Benefícios](#11-benefícios)
  - [1.2. Tipos de serviços](#12-tipos-de-serviços)
    - [1.2.1. IaaS (Infraestrutura como Serviço)](#121-iaas-infraestrutura-como-serviço)
    - [1.2.2. PaaS (Plataforma como Serviço)](#122-paas-plataforma-como-serviço)
    - [1.2.3. SaaS (Software como Serviço)](#123-saas-software-como-serviço)
  - [1.3. Modelos de implantação](#13-modelos-de-implantação)
    - [1.3.1. Nuvem pública](#131-nuvem-pública)
    - [1.3.2. Nuvem privada](#132-nuvem-privada)
    - [1.3.3. Nuvem híbrida](#133-nuvem-híbrida)
  - [1.4. Shared responsibility model](#14-shared-responsibility-model)
  - [1.5. CLI e CloudShell](#15-cli-e-cloudshell)
    - [1.5.1. CLI](#151-cli)
    - [1.5.2. Cloud Shell](#152-cloud-shell)
- [2. Arquitetura de infraestrutura global](#2-arquitetura-de-infraestrutura-global)
  - [2.1. Regiões da AWS](#21-regiões-da-aws)
  - [2.2. Zonas de disponibilidade](#22-zonas-de-disponibilidade)
  - [2.3. Zonas locais (Local zones)](#23-zonas-locais-local-zones)
  - [2.4. AWS Wavelength](#24-aws-wavelength)
  - [2.5. AWS Outposts](#25-aws-outposts)
- [3. IAM](#3-iam)
  - [3.1. Usuário (User)](#31-usuário-user)
  - [3.2. Grupos (Groups)](#32-grupos-groups)
  - [3.3. Funções (Roles)](#33-funções-roles)
  - [3.4. Políticas (Policies)](#34-políticas-policies)

<!-- /TOC -->

## 1. Cloud Computing

A **computação em nuvem**, ou **cloud computing**, refere-se a um modelo de entrega de `serviços` de computação pela internet. Em vez de manter servidores e recursos locais, empresas e indivíduos podem acessar e utilizar poder de processamento, armazenamento e aplicativos virtualizados `hospedados em data centers remotos`. Isso permite escalabilidade flexível, custos mais controláveis e acesso conveniente a recursos tecnológicos, promovendo a agilidade e a eficiência nos negócios e nas atividades cotidianas.

### 1.1. Benefícios

- `Velocidade`: A computação em nuvem oferece a vantagem da rápida implantação de serviços e recursos. A capacidade de provisionar instantaneamente servidores, armazenamento e outros recursos permite que as empresas atendam rapidamente às demandas do mercado e às necessidades dos clientes, reduzindo o tempo necessário para colocar novos serviços em funcionamento.

- `Updates`: Com a computação em nuvem, os provedores podem atualizar seus sistemas e serviços sem interromper a operação. Isso se traduz em menor tempo de inatividade para os usuários finais e garante que os serviços estejam sempre atualizados com as últimas melhorias de segurança, desempenho e funcionalidade.

- `Custo`: A natureza escalonável da computação em nuvem permite que as empresas paguem apenas pelo que usam, evitando custos fixos e investimentos iniciais elevados em infraestrutura de TI. Além disso, muitos provedores oferecem modelos de pagamento flexíveis, como contratos de pagamento por uso, o que pode levar a descontos com base no volume de serviços contratados ou na duração do contrato.

- `Data Security`: Os provedores de serviços em nuvem geralmente investem fortemente em segurança de dados. Eles implementam medidas de segurança avançadas, como criptografia de dados em repouso e em trânsito, autenticação de dois fatores e proteção contra ameaças cibernéticas. Além disso, os serviços em nuvem geralmente oferecem opções de backup automatizado, ajudando a garantir a recuperação de dados em caso de falhas.

- `Escalabilidade`: A capacidade de dimensionar recursos para cima ou para baixo conforme a demanda é uma característica fundamental da computação em nuvem. Isso permite que as empresas se adaptem rapidamente a picos de tráfego sem comprometer o desempenho ou a disponibilidade dos serviços. A escalabilidade pode ser realizada manualmente ou configurada para ser automática, garantindo que os recursos estejam sempre alinhados com as necessidades reais.

### 1.2. Tipos de serviços

![](assets/2023-08-22-13-48-08.png)

Comparado à estrutura de TI local (**on-site**), na qual as empresas mantêm e gerenciam todos os aspectos da infraestrutura, a computação em nuvem oferece maior flexibilidade e eficiência. No entanto, as diferenças entre os modelos de nuvem são notáveis. No `IaaS`, você precisa gerenciar mais camadas, desde o sistema operacional até o aplicativo. No `PaaS`, o foco é principalmente no desenvolvimento do aplicativo, enquanto o provedor cuida das camadas mais baixas. No `SaaS`, a gestão é mínima, já que o provedor lida com todas as camadas.

#### 1.2.1. IaaS (Infraestrutura como Serviço)

Nesse modelo, o provedor de nuvem oferece `infraestrutura virtualizada`, incluindo servidores, armazenamento, redes e recursos de processamento. Os usuários têm controle sobre sistemas operacionais, aplicativos e configurações, mas são responsáveis pelo gerenciamento de componentes de nível mais baixo, como atualizações de sistema operacional e segurança.

#### 1.2.2. PaaS (Plataforma como Serviço)

Aqui, **além da infraestrutura**, o provedor oferece uma `plataforma completa para desenvolvimento e implantação de aplicativos`. Os usuários gerenciam principalmente suas próprias aplicações e dados, enquanto o provedor cuida da infraestrutura subjacente, incluindo sistema operacional, middleware e ambiente de desenvolvimento.

#### 1.2.3. SaaS (Software como Serviço)

No modelo SaaS, os usuários acessam `aplicativos de software através da internet`, **sem a necessidade de instalação local**. Todas as camadas do software, desde a infraestrutura até o aplicativo em si, são gerenciadas pelo provedor do serviço. Os usuários se concentram principalmente no uso do software e nos dados relevantes.

### 1.3. Modelos de implantação

#### 1.3.1. Nuvem pública

A nuvem pública envolve a disponibilização de recursos de computação, como servidores, armazenamento e serviços, por meio da internet `para uso público`. Esses **recursos são compartilhados entre várias organizações e indivíduos**, geralmente hospedados e mantidos por provedores de serviços em nuvem. Ela oferece escalabilidade, flexibilidade e custos mais baixos, sendo ideal para empresas que desejam economizar em infraestrutura própria e pagar apenas pelos recursos utilizados. `A segurança e o isolamento são mantidos para garantir que os dados e as operações de cada cliente permaneçam protegidos e privados dentro desse ambiente`.

#### 1.3.2. Nuvem privada

Uma nuvem privada é uma infraestrutura de `nuvem exclusiva de uma única organização`. Ela pode ser hospedada internamente pela própria organização ou por um provedor de serviços de nuvem dedicado. A nuvem privada oferece controle total sobre a segurança, personalização e conformidade, sendo **adequada para empresas com requisitos rigorosos de privacidade e segurança**, bem como para aquelas que desejam manter certos aplicativos ou dados sensíveis em um ambiente controlado.

#### 1.3.3. Nuvem híbrida

A nuvem híbrida `combina elementos da nuvem pública e privada`. Nesse modelo, as organizações podem manter alguns recursos em uma nuvem privada para garantir segurança e controle, enquanto utilizam recursos da nuvem pública para lidar com picos de demanda, escalabilidade e flexibilidade. Isso **permite que as empresas equilibrem a eficiência da nuvem pública com a capacidade de gerenciar dados sensíveis e processos críticos** internamente.

### 1.4. Shared responsibility model

O "**Shared Responsibility Model**" (**Modelo de Responsabilidade Compartilhada**) é um conceito chave na computação em nuvem que delineia as responsabilidades entre os provedores de serviços em nuvem e os clientes em relação à **segurança e gerenciamento dos recursos**.

> O provedor de nuvem é responsável pela segurança da infraestrutura física e virtual, bem como pela segurança da plataforma em que os serviços são executados.
>
> O cliente é responsável pela segurança dos dados, configurações de acesso e gerenciamento de aplicativos e sistemas implantados na nuvem.

### 1.5. CLI e CloudShell

#### 1.5.1. CLI

A CLI (**Command-Line Interface**) é uma ferramenta que permite aos usuários interagir com serviços em nuvem e `realizar tarefas por meio de comandos digitados em um terminal de linha de comando em suas máquinas locais`. Ela oferece flexibilidade e automação na gestão de recursos e configurações na nuvem, permitindo aos usuários executar operações complexas usando scripts ou comandos individuais.

#### 1.5.2. Cloud Shell

O **Cloud Shell** é uma `interface interativa baseada em navegador` fornecida por alguns provedores de serviços em nuvem. Ele permite que os usuários acessem uma máquina virtual pré-configurada, já conectada às suas contas na nuvem, diretamente do navegador. Isso facilita a experimentação, a execução de comandos e a exploração de recursos **sem a necessidade de configurar ambientes locais**. O **Cloud Shell** é uma maneira conveniente de interagir com serviços em nuvem sem a necessidade de instalar ferramentas de linha de comando em sua máquina local.

## 2. Arquitetura de infraestrutura global

### 2.1. Regiões da AWS

As regiões da AWS são `localizações geográficas` onde a infraestrutura da AWS está hospedada. **Cada região é composta por várias zonas de disponibilidade** e oferece uma variedade de serviços da AWS. Exemplos de regiões incluem US East (Norte da Virgínia), Ásia-Pacífico (Tóquio) e Europa (Frankfurt).

### 2.2. Zonas de disponibilidade

Uma Zona de Disponibilidade (AZ) é um ou mais `data centers` fisicamente separados dentro de uma região. Isso ajuda a aumentar a **resiliência**, **redundância** e **disponibilidade** dos serviços. Os recursos implantados em diferentes AZs em uma região são isolados para garantir maior **confiabilidade**.

### 2.3. Zonas locais (Local zones)

As Zonas Locais são `extensões das regiões` da AWS que permitem a execução de aplicativos e serviços perto de **locais específicos onde há uma demanda mais intensa** de computação. Isso ajuda a **reduzir a latência** para os usuários finais e oferece maior flexibilidade na implantação de recursos.

### 2.4. AWS Wavelength

O AWS Wavelength é uma oferta que coloca recursos de computação e armazenamento da AWS em pontos de presença de `operadoras de telecomunicações`. Isso permite que aplicativos de baixa latência, como serviços de streaming de vídeo e jogos, sejam executados mais próximos dos usuários finais, aproveitando a infraestrutura de rede das operadoras.

### 2.5. AWS Outposts

O AWS Outposts é um serviço que permite a extensão dos serviços da AWS para `ambientes on-premise (locais físicos das empresas)`. Isso possibilita a execução de serviços da AWS em hardware dedicado nas instalações do cliente, proporcionando uma experiência semelhante à nuvem, porém em um ambiente controlado pela empresa.

## 3. IAM

O IAM (**Identity and Access Management**) da AWS é um serviço que `gerencia o acesso aos recursos e serviços` da AWS de forma segura. Ele permite que você controle **quem** pode acessar seus recursos na AWS e quais **ações** específicas eles podem realizar. Com o IAM, você pode criar e gerenciar identidades (como usuários, grupos e funções) e **atribuir permissões granulares** para garantir a segurança e o princípio do menor privilégio, restringindo o acesso apenas ao que é necessário para os usuários e processos.

### 3.1. Usuário (User)

Um usuário é uma `entidade com credenciais únicas que pode interagir com os serviços da AWS`. Os usuários são criados no IAM e podem ser pessoas reais ou processos automatizados. Cada usuário **possui um conjunto de credenciais** (nome de usuário e senha ou chaves de acesso) que são usadas para autenticar e autorizar suas ações na AWS.

### 3.2. Grupos (Groups)

Grupos são `conjuntos lógicos de usuários`. Eles facilitam a **atribuição de permissões a múltiplos usuários de uma vez**. Em vez de atribuir permissões individualmente a cada usuário, você pode associar políticas de permissão a grupos, e os membros desse grupo herdarão essas permissões.

### 3.3. Funções (Roles)

As funções são entidades do IAM que têm permissões associadas a elas e podem ser `temporariamente assumidas por usuários ou serviços dentro da AWS`. Elas são frequentemente usadas para permitir que serviços, como instâncias EC2 ou funções Lambda, `acessem recursos da AWS de maneira segura sem a necessidade de credenciais de longo prazo`. As funções também são usadas para fornecer **acesso temporário a usuários autenticados sem compartilhar chaves de acesso diretas**.

### 3.4. Políticas (Policies)

Políticas são `documentos que definem as permissões e ações` que os usuários, grupos e funções do IAM podem realizar em recursos específicos da AWS. Elas são escritas em **JSON (JavaScript Object Notation)** e detalham quais ações são permitidas ou negadas. As políticas **podem ser anexadas a usuários, grupos e funções** para controlar o acesso de maneira precisa.
