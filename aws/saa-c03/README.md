# SAA-C03 - AWS Certified Solutions Architect - Associate

[<- Voltar para a página principal](../../README.md)

<img src="assets/badge.png" alt="SAA-C03 - AWS Certified Solutions Architect - Associate" width="200"/>

---

**Sumário**

<!-- TOC -->

- [1. Analytics](#1-analytics)
    - [1.1. Amazon Athena](#11-amazon-athena)
    - [1.2. Amazon EMR Elastic MapReduce](#12-amazon-emr-elastic-mapreduce)
    - [1.3. Amazon Kinesis](#13-amazon-kinesis)
    - [1.4. Amazon OpenSearch Service](#14-amazon-opensearch-service)
    - [1.5. Amazon QuickSight](#15-amazon-quicksight)
    - [1.6. AWS Glue](#16-aws-glue)
    - [1.7. AWS Data Pipeline](#17-aws-data-pipeline)
    - [1.8. AWS Lake Formation](#18-aws-lake-formation)
    - [1.9. Amazon MSK Managed Streaming for Apache Kafka](#19-amazon-msk-managed-streaming-for-apache-kafka)
    - [1.10. AWS Data Exchange](#110-aws-data-exchange)
- [2. Integração de aplicações](#2-integra%C3%A7%C3%A3o-de-aplica%C3%A7%C3%B5es)
    - [2.1. Amazon SQS Simple Queue Service](#21-amazon-sqs-simple-queue-service)
    - [2.2. Amazon SNS Simple Notification Service](#22-amazon-sns-simple-notification-service)
    - [2.3. Amazon EventBridge](#23-amazon-eventbridge)
    - [2.4. Amazon MQ](#24-amazon-mq)
    - [2.5. AWS Step Functions](#25-aws-step-functions)
    - [2.6. AWS AppSync](#26-aws-appsync)
    - [2.7. Amazon AppFlow](#27-amazon-appflow)
- [3. Gerenciamento de custos da AWS](#3-gerenciamento-de-custos-da-aws)
    - [3.1. AWS Budgets](#31-aws-budgets)
    - [3.2. AWS Cost and Usage Report](#32-aws-cost-and-usage-report)
    - [3.3. AWS Cost Explorer](#33-aws-cost-explorer)
    - [3.4. Savings Plans](#34-savings-plans)
- [4. Computação](#4-computa%C3%A7%C3%A3o)
    - [4.1. Amazon EC2 Elastic Compute Cloud](#41-amazon-ec2-elastic-compute-cloud)
    - [4.2. Amazon EC2 Auto Scaling](#42-amazon-ec2-auto-scaling)
    - [4.3. AWS Elastic Beanstalk](#43-aws-elastic-beanstalk)
    - [4.4. AWS Batch](#44-aws-batch)
    - [4.5. AWS Serverless Application Repository](#45-aws-serverless-application-repository)
    - [4.6. AWS Outposts](#46-aws-outposts)
    - [4.7. VMware Cloud on AWS](#47-vmware-cloud-on-aws)
    - [4.8. AWS Wavelength](#48-aws-wavelength)
- [5. Contêineres](#5-cont%C3%AAineres)
    - [5.1. Amazon ECS Elastic Container Service](#51-amazon-ecs-elastic-container-service)
    - [5.2. Amazon ECS Anywhere Elastic Container Service](#52-amazon-ecs-anywhere-elastic-container-service)
    - [5.3. Amazon EKS Elastic Kubernetes Service](#53-amazon-eks-elastic-kubernetes-service)
    - [5.4. Amazon EKS Anywhere Elastic Kubernetes Service](#54-amazon-eks-anywhere-elastic-kubernetes-service)
    - [5.5. Amazon EKS Distro Elastic Kubernetes Service Distro](#55-amazon-eks-distro-elastic-kubernetes-service-distro)
    - [5.6. Amazon ECR Elastic Container Registry](#56-amazon-ecr-elastic-container-registry)
- [6. Banco de dados](#6-banco-de-dados)
    - [6.1. Amazon RDS Relational Database Service](#61-amazon-rds-relational-database-service)
    - [6.2. Amazon Aurora](#62-amazon-aurora)
    - [6.3. Amazon Aurora Serverless](#63-amazon-aurora-serverless)
    - [6.4. Amazon Redshift](#64-amazon-redshift)
    - [6.5. Amazon DynamoDB](#65-amazon-dynamodb)
    - [6.6. Amazon ElastiCache](#66-amazon-elasticache)
    - [6.7. Amazon DocumentDB MongoDB-compatible](#67-amazon-documentdb-mongodb-compatible)
    - [6.8. Amazon Neptune](#68-amazon-neptune)
    - [6.9. Amazon QLDB Quantum Ledger Database](#69-amazon-qldb-quantum-ledger-database)
    - [6.10. Amazon Keyspaces for Apache Cassandra](#610-amazon-keyspaces-for-apache-cassandra)
- [7. Ferramentas do desenvolvedor](#7-ferramentas-do-desenvolvedor)
    - [7.1. AWS X-Ray](#71-aws-x-ray)
- [8. Web e dispositivos móveis de front-end](#8-web-e-dispositivos-m%C3%B3veis-de-front-end)
    - [8.1. Amazon API Gateway](#81-amazon-api-gateway)
    - [8.2. AWS Amplify](#82-aws-amplify)
    - [8.3. Amazon Pinpoint](#83-amazon-pinpoint)
    - [8.4. AWS Device Farm](#84-aws-device-farm)
- [9. Machine learning](#9-machine-learning)
    - [9.1. Amazon SageMaker](#91-amazon-sagemaker)
    - [9.2. Amazon Comprehend](#92-amazon-comprehend)
    - [9.3. Amazon Rekognition](#93-amazon-rekognition)
    - [9.4. Amazon Polly](#94-amazon-polly)
    - [9.5. Amazon Lex](#95-amazon-lex)
    - [9.6. Amazon Transcribe](#96-amazon-transcribe)
    - [9.7. Amazon Translate](#97-amazon-translate)
    - [9.8. Amazon Textract](#98-amazon-textract)
    - [9.9. Amazon Kendra](#99-amazon-kendra)
    - [9.10. Amazon Forecast](#910-amazon-forecast)
    - [9.11. Amazon Fraud Detector](#911-amazon-fraud-detector)
- [10. Gerenciamento e governança](#10-gerenciamento-e-governan%C3%A7a)
    - [10.1. AWS Management Console](#101-aws-management-console)
    - [10.2. AWS CLI Command Line Interface](#102-aws-cli-command-line-interface)
    - [10.3. AWS CloudFormation](#103-aws-cloudformation)
    - [10.4. AWS CloudTrail](#104-aws-cloudtrail)
    - [10.5. Amazon CloudWatch](#105-amazon-cloudwatch)
    - [10.6. AWS Systems Manager](#106-aws-systems-manager)
    - [10.7. AWS Config](#107-aws-config)
    - [10.8. AWS Auto Scaling](#108-aws-auto-scaling)
    - [10.9. AWS Compute Optimizer](#109-aws-compute-optimizer)
    - [10.10. AWS Trusted Advisor](#1010-aws-trusted-advisor)
    - [10.11. AWS Well-Architected Tool](#1011-aws-well-architected-tool)
    - [10.12. AWS Organizations](#1012-aws-organizations)
    - [10.13. AWS Control Tower](#1013-aws-control-tower)
    - [10.14. AWS License Manager](#1014-aws-license-manager)
    - [10.15. AWS Service Catalog](#1015-aws-service-catalog)
    - [10.16. AWS Proton](#1016-aws-proton)
    - [10.17. AWS Health Dashboard](#1017-aws-health-dashboard)
    - [10.18. Amazon Managed Grafana](#1018-amazon-managed-grafana)
    - [10.19. Amazon Managed Service for Prometheus](#1019-amazon-managed-service-for-prometheus)
- [11. Serviços de mídia](#11-servi%C3%A7os-de-m%C3%ADdia)
    - [11.1. Amazon Elastic Transcoder](#111-amazon-elastic-transcoder)
    - [11.2. Amazon Kinesis Video Streams](#112-amazon-kinesis-video-streams)
- [12. Migração e transferência](#12-migra%C3%A7%C3%A3o-e-transfer%C3%AAncia)
    - [12.1. AWS DMS Database Migration Service](#121-aws-dms-database-migration-service)
    - [12.2. AWS Migration Hub](#122-aws-migration-hub)
    - [12.3. AWS Application Migration Service](#123-aws-application-migration-service)
    - [12.4. AWS Application Discovery Service](#124-aws-application-discovery-service)
    - [12.5. AWS DataSync](#125-aws-datasync)
    - [12.6. AWS Transfer Family](#126-aws-transfer-family)
    - [12.7. AWS Snow Family](#127-aws-snow-family)
- [13. Redes e entrega de conteúdo](#13-redes-e-entrega-de-conte%C3%BAdo)
    - [13.1. AWS Client VPN](#131-aws-client-vpn)
    - [13.2. Amazon CloudFront](#132-amazon-cloudfront)
    - [13.3. AWS Direct Connect](#133-aws-direct-connect)
    - [13.4. ELB Elastic Load Balancing](#134-elb-elastic-load-balancing)
    - [13.5. AWS Global Accelerator](#135-aws-global-accelerator)
    - [13.6. AWS PrivateLink](#136-aws-privatelink)
    - [13.7. Amazon Route 53](#137-amazon-route-53)
    - [13.8. AWS Site-to-Site VPN](#138-aws-site-to-site-vpn)
    - [13.9. AWS Transit Gateway](#139-aws-transit-gateway)
    - [13.10. Amazon VPC Virtual Private Cloud](#1310-amazon-vpc-virtual-private-cloud)
- [14. Segurança, identidade e conformidade](#14-seguran%C3%A7a-identidade-e-conformidade)
    - [14.1. AWS IAM Identity and Access Management](#141-aws-iam-identity-and-access-management)
    - [14.2. AWS IAM Identity Center AWS Single Sign-On](#142-aws-iam-identity-center-aws-single-sign-on)
    - [14.3. AWS KMS Key Management Service](#143-aws-kms-key-management-service)
    - [14.4. AWS Secrets Manager](#144-aws-secrets-manager)
    - [14.5. Amazon Cognito](#145-amazon-cognito)
    - [14.6. AWS Directory Service](#146-aws-directory-service)
    - [14.7. AWS RAM Resource Access Manager](#147-aws-ram-resource-access-manager)
    - [14.8. AWS Artifact](#148-aws-artifact)
    - [14.9. AWS Audit Manager](#149-aws-audit-manager)
    - [14.10. AWS ACM Certificate Manager](#1410-aws-acm-certificate-manager)
    - [14.11. AWS CloudHSM](#1411-aws-cloudhsm)
    - [14.12. Amazon Macie](#1412-amazon-macie)
    - [14.13. Amazon GuardDuty](#1413-amazon-guardduty)
    - [14.14. Amazon Inspector](#1414-amazon-inspector)
    - [14.15. Amazon Detective](#1415-amazon-detective)
    - [14.16. AWS Firewall Manager](#1416-aws-firewall-manager)
    - [14.17. AWS WAF Web Application Firewall](#1417-aws-waf-web-application-firewall)
    - [14.18. AWS Shield](#1418-aws-shield)
    - [14.19. AWS Network Firewall](#1419-aws-network-firewall)
    - [14.20. AWS Security Hub](#1420-aws-security-hub)
- [15. Sem servidor](#15-sem-servidor)
    - [15.1. AWS Lambda](#151-aws-lambda)
    - [15.2. AWS Fargate](#152-aws-fargate)
    - [15.3. AWS AppSync](#153-aws-appsync)
- [16. Armazenamento](#16-armazenamento)
    - [16.1. Amazon S3 Simple Storage Service](#161-amazon-s3-simple-storage-service)
    - [16.2. Amazon S3 Glacier](#162-amazon-s3-glacier)
    - [16.3. Amazon EBS Elastic Block Store](#163-amazon-ebs-elastic-block-store)
    - [16.4. Amazon EFS Elastic File System](#164-amazon-efs-elastic-file-system)
    - [16.5. Amazon FSx File System](#165-amazon-fsx-file-system)
    - [16.6. AWS Backup](#166-aws-backup)
    - [16.7. AWS Storage Gateway](#167-aws-storage-gateway)

<!-- /TOC -->

[<- Voltar para a página principal](../../README.md)

---

## 1. Analytics

#### 1.1. Amazon Athena

É um serviço de consulta interativo que permite executar consultas SQL diretamente em dados armazenados no Amazon S3, sem necessidade de provisionar infraestrutura. Athena escala automaticamente e cobra por volume de dados digitalizados, suportando múltiplos formatos como CSV, JSON, Parquet e ORC, facilitando análises rápidas e ad hoc.

#### 1.2. Amazon EMR (Elastic MapReduce)

É uma plataforma gerenciada para processamento distribuído de grandes volumes de dados utilizando frameworks como Hadoop, Spark e Presto. Oferece provisionamento rápido e escalável de clusters, com flexibilidade para executar análises complexas e processamento batch em ambientes elásticos.

#### 1.3. Amazon Kinesis

É um conjunto de serviços para ingestão e processamento de dados em tempo real, incluindo streams de dados contínuos, entrega automática para destinos e análise em streaming usando SQL. Permite construir aplicações que processam grandes volumes de dados em baixa latência, para casos como monitoramento e análise de logs.

#### 1.4. Amazon OpenSearch Service

É um serviço gerenciado que permite implementar clusters para busca, análise e visualização de dados utilizando OpenSearch ou Elasticsearch. Suporta indexação eficiente e consultas rápidas em grandes volumes, com recursos para monitoramento, alertas e criação de dashboards.

#### 1.5. Amazon QuickSight

É uma solução de business intelligence que possibilita criar visualizações interativas, painéis e relatórios a partir de dados diversos. É escalável, com cobrança por usuário ativo ou sessão, e inclui recursos de machine learning para gerar insights automáticos e análises avançadas.

#### 1.6. AWS Glue

É um serviço serverless de ETL que automatiza a extração, transformação e carregamento de dados para preparação analítica. Inclui um catálogo de dados centralizado, gera código ETL automaticamente em Python ou Scala e suporta múltiplos formatos, facilitando a integração e limpeza dos dados.

#### 1.7. AWS Data Pipeline

É um serviço de orquestração que automatiza o movimento e transformação de dados entre fontes diferentes, incluindo serviços AWS e ambientes on-premises. Permite criar workflows com dependências, agendamento e monitoramento, garantindo a execução confiável de processos ETL e carga de dados.

#### 1.8. AWS Lake Formation

É um serviço que simplifica a criação e governança de data lakes seguros no Amazon S3, automatizando a ingestão, catalogação, limpeza e controle de acesso aos dados. Centraliza a administração de permissões e políticas de segurança para facilitar o uso e análise dos dados em larga escala.

#### 1.9. Amazon MSK (Managed Streaming for Apache Kafka)

É um serviço gerenciado que facilita a criação e operação de clusters Apache Kafka, oferecendo alta disponibilidade, escalabilidade e segurança integrada. Remove a complexidade de gerenciar a infraestrutura Kafka, permitindo focar na construção de aplicações de streaming de dados.

#### 1.10. AWS Data Exchange

É uma plataforma que permite descobrir, assinar e consumir datasets de provedores externos de forma segura e automatizada. Facilita o acesso a dados externos para uso em análises e aplicações, com controle granular sobre permissões e atualizações automáticas das assinaturas.

## 2. Integração de aplicações

#### 2.1. Amazon SQS (Simple Queue Service)

É um serviço gerenciado de filas de mensagens que garante desacoplamento e escalabilidade entre componentes de aplicações distribuídas. Suporta filas padrão com entrega pelo menos uma vez e filas FIFO para garantir ordenação e entrega única, além de permitir o controle de visibilidade das mensagens.

#### 2.2. Amazon SNS (Simple Notification Service)

É um serviço de mensageria pub/sub que permite enviar notificações instantâneas para múltiplos assinantes via SMS, email, HTTP endpoints, ou outras filas. Oferece entrega escalável, alta disponibilidade e suporte a mensagens push para aplicações distribuídas.

#### 2.3. Amazon EventBridge

É um serviço de barramento de eventos que permite construir arquiteturas orientadas a eventos, roteando eventos de aplicações, serviços AWS e SaaS para destinos configuráveis. Suporta regras complexas para filtragem e transformação, facilitando a criação de sistemas desacoplados e escaláveis.

#### 2.4. Amazon MQ

É um serviço gerenciado para brokers de mensagens compatível com protocolos padrão como MQTT, AMQP e JMS. Facilita a migração e operação de aplicações baseadas em mensagens com compatibilidade para brokers tradicionais, garantindo alta disponibilidade, segurança e gerenciamento simplificado.

#### 2.5. AWS Step Functions

É um serviço de orquestração que permite criar workflows visuais e coordenar múltiplos serviços AWS e componentes em processos sequenciais ou paralelos. Oferece controle de estados, tratamento de erros e execução condicional, facilitando a automação e a gestão de processos complexos em aplicações.

#### 2.6. AWS AppSync

É um serviço gerenciado que facilita a criação de APIs GraphQL para aplicações, oferecendo sincronização de dados em tempo real, atualizações offline e segurança integrada. É escalável e simplifica o desenvolvimento de aplicações modernas que precisam acessar dados distribuídos de múltiplas fontes.

#### 2.7. Amazon AppFlow

É um serviço gerenciado que permite criar fluxos de dados bidirecionais entre aplicações SaaS e serviços AWS de forma segura e escalável, sem necessidade de código. Suporta transformações e filtragens durante a transferência, facilitando a automação da sincronização de dados entre diferentes sistemas.

## 3. Gerenciamento de custos da AWS

#### 3.1. AWS Budgets

É um serviço que permite criar orçamentos personalizados para monitorar custos e uso da AWS, com alertas configuráveis para quando os limites definidos são atingidos ou excedidos. Facilita o controle financeiro ao fornecer visibilidade detalhada e notificações proativas para evitar gastos inesperados.

#### 3.2. AWS Cost and Usage Report

É um serviço que gera relatórios detalhados e configuráveis sobre custos e uso da AWS, permitindo análises granulares por serviço, recurso, tags e períodos específicos. Esses relatórios são armazenados no Amazon S3 e podem ser usados para auditoria, monitoramento e integração com ferramentas externas de análise.

#### 3.3. AWS Cost Explorer

É uma ferramenta interativa que permite visualizar, analisar e entender padrões de custos e uso na AWS ao longo do tempo. Oferece gráficos personalizáveis, filtros avançados e previsões de gastos, auxiliando na identificação de tendências e oportunidades para otimização financeira.

#### 3.4. Savings Plans

É uma opção de compromisso de uso que oferece descontos significativos sobre a tarifa sob demanda em troca de um compromisso de uso consistente por um período (geralmente 1 ou 3 anos). Oferece flexibilidade para aplicar os descontos a diferentes tipos de instâncias e serviços, ajudando a reduzir custos fixos.

## 4. Computação

#### 4.1. Amazon EC2 (Elastic Compute Cloud)

É um serviço que oferece capacidade computacional escalável na nuvem por meio de instâncias virtuais configuráveis. Permite escolher tipos variados de instâncias, sistemas operacionais, armazenamento e redes, oferecendo controle total sobre o ambiente computacional e a possibilidade de escalabilidade manual ou automática.

#### 4.2. Amazon EC2 Auto Scaling

É um recurso que ajusta automaticamente o número de instâncias EC2 em execução com base em políticas definidas, métricas de desempenho ou agendamentos. Garante alta disponibilidade e desempenho otimizando custos, ao garantir a quantidade ideal de recursos conforme a demanda da aplicação.

#### 4.3. AWS Elastic Beanstalk

É um serviço que facilita a implantação e gerenciamento de aplicações web e serviços em múltiplas linguagens, automatizando o provisionamento da infraestrutura, balanceamento de carga, escalabilidade e monitoramento. Permite foco no desenvolvimento sem necessidade de gerenciar diretamente os recursos subjacentes.

#### 4.4. AWS Batch

É um serviço que permite executar jobs de computação em lote de forma escalável e gerenciada, automatizando o provisionamento de recursos computacionais conforme a demanda. Suporta múltiplos tipos de jobs, filas, dependências entre tarefas e otimiza o uso de instâncias para reduzir custos operacionais.

#### 4.5. AWS Serverless Application Repository

É um catálogo de aplicações serverless pré-construídas e reutilizáveis que podem ser implantadas facilmente. Permite desenvolvedores descobrir, implantar e compartilhar aplicações baseadas em funções Lambda e outros recursos serverless, acelerando o desenvolvimento sem necessidade de escrever todo o código.

#### 4.6. AWS Outposts

É uma solução que oferece infraestrutura, serviços, APIs e ferramentas AWS em ambientes locais, garantindo consistência entre a nuvem e on-premises. É ideal para aplicações que exigem latência muito baixa, processamento local de dados ou conformidade regulatória específica.

#### 4.7. VMware Cloud on AWS

É um serviço que fornece um ambiente VMware totalmente gerenciado na nuvem AWS, permitindo migrar, executar e expandir cargas de trabalho VMware com acesso aos serviços nativos da AWS. Oferece integração simplificada para ambientes híbridos e consolida operações entre on-premises e nuvem.

#### 4.8. AWS Wavelength

É um serviço que traz recursos computacionais e armazenamento da AWS para as bordas das redes 5G, reduzindo latência para aplicações sensíveis a tempo, como IoT, jogos e streaming em tempo real. Permite desenvolver aplicações que requerem respostas ultra-rápidas próximas aos usuários finais.

## 5. Contêineres

#### 5.1. Amazon ECS (Elastic Container Service)

É um serviço gerenciado para orquestração de contêineres que permite executar aplicações em Docker de forma escalável, segura e altamente disponível. Suporta clusters de contêineres com agendamento automático, integração com balanceadores de carga e diferentes modos de execução, incluindo Fargate e instâncias EC2.

#### 5.2. Amazon ECS Anywhere (Elastic Container Service)

É uma extensão do Amazon ECS que permite executar e gerenciar contêineres em infraestrutura on-premises ou em outras nuvens, usando a mesma interface e APIs do ECS na nuvem AWS. Oferece consistência operacional e controle centralizado sobre aplicações em contêineres distribuídas.

#### 5.3. Amazon EKS (Elastic Kubernetes Service)

É um serviço gerenciado que simplifica a execução de clusters Kubernetes na AWS, cuidando da infraestrutura de controle e automação de operações. Permite executar aplicações containerizadas com escalabilidade, alta disponibilidade e segurança, utilizando o Kubernetes padrão e suas APIs nativas.

#### 5.4. Amazon EKS Anywhere (Elastic Kubernetes Service)

É uma solução que permite criar e operar clusters Kubernetes on-premises com ferramentas nativas da AWS, oferecendo suporte a atualizações automáticas e gerenciamento simplificado. Facilita a adoção do Kubernetes em ambientes locais com consistência em relação ao EKS na nuvem.

#### 5.5. Amazon EKS Distro (Elastic Kubernetes Service Distro)

É uma distribuição open source do Kubernetes usada pela AWS para construir o Amazon EKS, que pode ser instalada em ambientes on-premises ou outras nuvens. Permite criar clusters Kubernetes compatíveis e consistentes com o padrão EKS, facilitando portabilidade e operações híbridas.

#### 5.6. Amazon ECR (Elastic Container Registry)

É um serviço de registro de contêineres gerenciado para armazenar, gerenciar e distribuir imagens Docker de forma segura e escalável. Oferece integração com ferramentas de build e orquestração, suporte a controle de acesso baseado em políticas e imagens versionadas para facilitar o ciclo de vida dos contêineres.

## 6. Banco de dados

#### 6.1. Amazon RDS (Relational Database Service)

É um serviço gerenciado que simplifica a configuração, operação e escalabilidade de bancos de dados relacionais, suportando múltiplos motores como MySQL, PostgreSQL, MariaDB, Oracle e SQL Server. Oferece backups automáticos, patching, replicação e failover para alta disponibilidade.

#### 6.2. Amazon Aurora

É um banco de dados relacional gerenciado, compatível com MySQL e PostgreSQL, que oferece alta performance, disponibilidade e durabilidade. Utiliza arquitetura distribuída para replicação automática e failover rápido, suportando cargas intensas com menor latência em comparação a bancos tradicionais.

#### 6.3. Amazon Aurora Serverless

É uma configuração sob demanda do Aurora que ajusta automaticamente a capacidade computacional conforme o volume de conexões e consultas, sem necessidade de provisionamento prévio. Ideal para cargas de trabalho intermitentes ou imprevisíveis, otimizando custos ao pagar somente pelo uso efetivo.

#### 6.4. Amazon Redshift

É um data warehouse totalmente gerenciado, projetado para executar consultas analíticas complexas em grandes volumes de dados com alta performance. Utiliza armazenamento columnar, compressão e paralelismo massivo para acelerar análises, e permite escalabilidade tanto vertical quanto horizontal.

#### 6.5. Amazon DynamoDB

É um banco de dados NoSQL totalmente gerenciado que oferece baixa latência e alta performance para aplicações que requerem escalabilidade massiva. Suporta armazenamento de chave-valor e documentos, com replicação automática, backup, controle de acesso granular e funcionalidades como streams e TTL.

#### 6.6. Amazon ElastiCache

É um serviço gerenciado para implantação de caches na memória usando Redis ou Memcached, que melhora a performance de aplicações ao reduzir latência e carga em bancos de dados backend. Oferece escalabilidade, replicação, failover automático e persistência opcional para melhorar a disponibilidade.

#### 6.7. Amazon DocumentDB (MongoDB-compatible)

É um banco de dados NoSQL gerenciado, compatível com APIs MongoDB, projetado para armazenar, consultar e indexar documentos JSON. Oferece alta disponibilidade, escalabilidade e segurança, com backups automatizados e recuperação rápida para cargas de trabalho orientadas a documentos.

#### 6.8. Amazon Neptune

É um banco de dados gerenciado otimizado para armazenar e consultar grafos, suportando os modelos RDF e Property Graph. Fornece consultas rápidas e consistentes para aplicações que requerem relacionamentos complexos entre dados, com alta disponibilidade e segurança integrada.

#### 6.9. Amazon QLDB (Quantum Ledger Database)

É um banco de dados ledger gerenciado que fornece um registro imutável, criptograficamente verificável e sequencial de transações. Ideal para aplicações que exigem rastreamento transparente e auditável das mudanças nos dados, garantindo integridade e confiança sem necessidade de blockchain distribuído.

#### 6.10. Amazon Keyspaces (for Apache Cassandra)

É um banco de dados gerenciado compatível com Apache Cassandra que oferece escalabilidade, alta disponibilidade e replicação automática. Permite executar workloads Cassandra na AWS sem a necessidade de gerenciar a infraestrutura subjacente, facilitando a migração e operação de aplicações Cassandra.

## 7. Ferramentas do desenvolvedor

#### 7.1. AWS X-Ray

É um serviço que permite analisar e depurar aplicações distribuídas, coletando dados detalhados sobre requisições, latências e erros em microserviços e componentes. Ajuda a identificar gargalos de performance, visualizar fluxos de execução e otimizar a arquitetura de aplicações complexas.

## 8. Web e dispositivos móveis de front-end

#### 8.1. Amazon API Gateway

É um serviço gerenciado que permite criar, publicar, manter, monitorar e proteger APIs RESTful e WebSocket em grande escala. Suporta transformação de payload, controle de acesso, limitação de taxa e integração com múltiplos backends para facilitar o desenvolvimento de APIs seguras e escaláveis.

#### 8.2. AWS Amplify

É um conjunto de ferramentas e serviços para desenvolvimento rápido de aplicações web e móveis full stack. Oferece recursos para autenticação, armazenamento, APIs, hospedagem e integração contínua, facilitando a construção, implantação e gerenciamento de aplicações com foco em experiência do usuário.

#### 8.3. Amazon Pinpoint

É um serviço para engajamento de usuários que permite enviar mensagens direcionadas por email, SMS, push notifications e voz, com segmentação avançada e análises detalhadas. Facilita campanhas de marketing, comunicação personalizada e monitoramento da interação dos usuários com as mensagens enviadas.

#### 8.4. AWS Device Farm

É um serviço que oferece teste de aplicações móveis em dispositivos físicos reais hospedados na nuvem. Permite automatizar testes em uma ampla variedade de dispositivos e sistemas operacionais, identificando problemas de compatibilidade, desempenho e usabilidade antes da publicação.

## 9. Machine learning

#### 9.1. Amazon SageMaker

É uma plataforma completa para construir, treinar e implantar modelos de machine learning em escala. Facilita o desenvolvimento com ferramentas integradas, notebooks, algoritmos otimizados e automação, reduzindo o tempo de entrega de soluções inteligentes.

#### 9.2. Amazon Comprehend

É um serviço de processamento de linguagem natural que utiliza machine learning para identificar insights e relacionamentos em textos. Permite detectar sentimentos, entidades, tópicos e linguagem, facilitando análises automatizadas e extração de informações relevantes de grandes volumes de dados textuais.

#### 9.3. Amazon Rekognition

É um serviço que oferece análise de imagens e vídeos usando machine learning para detectar objetos, cenas, atividades, rostos e texto. Permite reconhecimento facial, moderação de conteúdo e análise de vídeo para segurança e automação.

#### 9.4. Amazon Polly

É um serviço que converte texto em fala natural, gerando áudio realista para diversas aplicações, como assistentes virtuais e sistemas de acessibilidade. Suporta múltiplos idiomas e vozes, possibilitando personalização e streaming em tempo real.

#### 9.5. Amazon Lex

É um serviço para construir interfaces de conversa baseadas em voz e texto utilizando machine learning. Permite criar chatbots e assistentes virtuais com compreensão de linguagem natural, reconhecimento automático de fala e gerenciamento de diálogos complexos.

#### 9.6. Amazon Transcribe

É um serviço que converte fala em texto automaticamente, fornecendo transcrições precisas para áudios em vários idiomas e formatos. Suporta pontuação automática, identificação de falantes e streaming para aplicações de legendas, atendimento e análise.

#### 9.7. Amazon Translate

É um serviço de tradução automática neural que oferece traduções rápidas e de alta qualidade entre múltiplos idiomas. Facilita a internacionalização de aplicações e comunicação multilíngue com suporte a personalização e integração em tempo real.

#### 9.8. Amazon Textract

É um serviço que extrai texto e dados automaticamente de documentos digitalizados, incluindo formulários e tabelas, usando machine learning. Substitui o processamento manual, possibilitando análise rápida e precisa de documentos complexos.

#### 9.9. Amazon Kendra

É um serviço de busca inteligente baseado em machine learning que fornece respostas precisas e relevantes para consultas feitas em conteúdos corporativos, como documentos, sites e bases de dados. Suporta linguagem natural e melhora a eficiência na recuperação de informações.

#### 9.10. Amazon Forecast

É um serviço que gera previsões precisas de séries temporais usando machine learning, sem necessidade de experiência prévia em modelos preditivos. Pode ser usado para demandas de vendas, inventário, planejamento financeiro e outros casos que dependem de previsão baseada em dados históricos.

#### 9.11. Amazon Fraud Detector

É um serviço que utiliza machine learning para detectar atividades fraudulentas em tempo real, como transações suspeitas e comportamentos anômalos. Permite criar, treinar e implantar modelos personalizados com base em dados específicos do cliente, reduzindo perdas e riscos operacionais.

## 10. Gerenciamento e governança

#### 10.1. AWS Management Console

É uma interface gráfica web que permite acessar, configurar e gerenciar recursos e serviços AWS de forma intuitiva, com suporte a dashboards personalizáveis e ferramentas para facilitar operações administrativas.

#### 10.2. AWS CLI (Command Line Interface)

É uma ferramenta de linha de comando que permite gerenciar e automatizar serviços AWS a partir do terminal. Facilita operações repetitivas, integração em scripts e orquestração de infraestrutura sem necessidade de interface gráfica.

#### 10.3. AWS CloudFormation

É um serviço que permite criar e gerenciar recursos AWS através de templates declarativos em YAML ou JSON. Automatiza o provisionamento e configuração de infraestrutura como código, garantindo replicabilidade, consistência e controle de versões.

#### 10.4. AWS CloudTrail

É um serviço que registra e monitora chamadas de API e atividades do usuário na conta AWS, fornecendo logs detalhados para auditoria, conformidade e análise de segurança. Permite rastrear alterações e detectar atividades suspeitas em tempo real.

#### 10.5. Amazon CloudWatch

É um serviço de monitoramento que coleta métricas, logs e eventos para recursos e aplicações AWS. Oferece dashboards, alarmes e ações automatizadas para identificar problemas operacionais, otimizar desempenho e manter a saúde dos sistemas.

#### 10.6. AWS Systems Manager

É uma solução unificada para gerenciar infraestrutura, automação, patching, inventário e operações de recursos AWS e on-premises. Fornece ferramentas para manter a segurança, conformidade e eficiência operacional.

#### 10.7. AWS Config

É um serviço que rastreia e avalia a configuração dos recursos AWS em tempo real, armazenando histórico para auditoria e conformidade. Permite definir regras para garantir que os recursos estejam em conformidade com políticas organizacionais.

#### 10.8. AWS Auto Scaling

É um serviço que ajusta automaticamente a capacidade de recursos computacionais para manter desempenho estável e otimizar custos. Monitora métricas definidas e aplica políticas de escalabilidade para aumentar ou reduzir instâncias conforme a demanda da aplicação.

#### 10.9. AWS Compute Optimizer

É um serviço que analisa histórico de uso de recursos computacionais e recomenda configurações otimizadas para melhorar desempenho e reduzir custos, incluindo tipos de instâncias EC2, volumes EBS e funções Lambda.

#### 10.10. AWS Trusted Advisor

É um serviço que analisa a conta AWS e fornece recomendações para otimização de custos, segurança, desempenho, tolerância a falhas e limites de serviço, auxiliando na melhoria contínua da arquitetura.

#### 10.11. AWS Well-Architected Tool

É uma ferramenta que ajuda a avaliar workloads com base nas melhores práticas da AWS, oferecendo relatórios e recomendações para melhorar segurança, confiabilidade, desempenho, eficiência e sustentabilidade da infraestrutura.

#### 10.12. AWS Organizations

É um serviço que permite gerenciar múltiplas contas AWS de forma centralizada, aplicando políticas, consolidando faturamento e definindo hierarquias para governança e controle de acesso em ambientes corporativos.

#### 10.13. AWS Control Tower

É uma solução para configurar e governar ambientes multi-conta AWS com boas práticas pré-definidas. Automatiza provisionamento de contas, políticas de segurança e conformidade, facilitando a gestão centralizada em larga escala.

#### 10.14. AWS License Manager

É um serviço que facilita o gerenciamento centralizado de licenças de software em ambientes AWS e on-premises, controlando uso, compliance e evitando custos excessivos associados a licenças não monitoradas.

#### 10.15. AWS Service Catalog

É um serviço que permite criar e gerenciar catálogos de recursos aprovados para uso dentro da organização, facilitando o provisionamento padronizado, controle de acesso e governança de infraestrutura.

#### 10.16. AWS Proton

É um serviço que automatiza provisionamento e implantação de aplicações containerizadas e serverless, usando templates para padronizar infraestrutura e código, acelerando o desenvolvimento e garantindo consistência.

#### 10.17. AWS Health Dashboard

É um serviço que fornece visibilidade sobre o status e eventos que afetam recursos AWS em uma conta, incluindo notificações proativas sobre problemas operacionais, manutenção programada e recomendações para mitigação de riscos.

#### 10.18. Amazon Managed Grafana

É um serviço gerenciado que oferece dashboards para visualização e análise de métricas e logs, com suporte a múltiplas fontes de dados. Facilita o monitoramento em tempo real e colaboração entre equipes.

#### 10.19. Amazon Managed Service for Prometheus

É um serviço gerenciado para coleta, armazenamento e consulta de métricas de monitoramento usando Prometheus, escalável e seguro, eliminando a necessidade de gerenciar a infraestrutura do Prometheus.

## 11. Serviços de mídia

#### 11.1. Amazon Elastic Transcoder

É um serviço de transcodificação de mídia na nuvem que converte arquivos de vídeo e áudio em formatos compatíveis com dispositivos variados. Permite criar presets personalizados para ajustar qualidade, resolução e formatos, facilitando a entrega de conteúdo otimizado para diferentes plataformas.

#### 11.2. Amazon Kinesis Video Streams

É um serviço que captura, armazena e processa fluxos de vídeo em tempo real para análise e machine learning. Oferece ingestão segura de vídeos de câmeras e dispositivos, com armazenamento durável e integração para processamentos como reconhecimento facial e monitoramento.

## 12. Migração e transferência

#### 12.1. AWS DMS (Database Migration Service)

É um serviço que facilita a migração e replicação contínua de bancos de dados relacionais, NoSQL e data warehouses para AWS, com suporte a migração homogênea e heterogênea, garantindo mínimo impacto na aplicação durante a transferência.

#### 12.2. AWS Migration Hub

É um painel centralizado para gerenciar, monitorar e rastrear o progresso de migrações de aplicações em múltiplos serviços AWS, proporcionando visibilidade consolidada do estado de migração e facilitando a coordenação entre equipes.

#### 12.3. AWS Application Migration Service

É um serviço que simplifica e automatiza a migração de servidores físicos, virtuais ou baseados em nuvem para AWS, minimizando downtime ao replicar continuamente dados e sincronizar aplicações durante o processo de migração.

#### 12.4. AWS Application Discovery Service

É um serviço que coleta automaticamente informações sobre a infraestrutura on-premises, como servidores, aplicações e dependências, para planejar e executar migrações para a nuvem com mais precisão e menor risco.

#### 12.5. AWS DataSync

É um serviço que automatiza e acelera a transferência de grandes volumes de dados entre armazenamento on-premises e AWS, usando protocolos seguros e otimizados para mover arquivos e objetos com alta eficiência e monitoramento integrado.

#### 12.6. AWS Transfer Family

É um serviço gerenciado que permite transferir arquivos diretamente para e da AWS usando protocolos tradicionais como SFTP, FTPS e FTP, facilitando a migração e integração de fluxos de trabalho legados com armazenamento na nuvem.

#### 12.7. AWS Snow Family

É uma coleção de dispositivos físicos para transferir grandes volumes de dados para a nuvem de forma segura e eficiente, ideal para ambientes com baixa conectividade ou requisitos de alta segurança. Inclui dispositivos Snowcone, Snowball e Snowmobile.

## 13. Redes e entrega de conteúdo

#### 13.1. AWS Client VPN

É um serviço gerenciado que permite conexões VPN seguras e escaláveis para acessar recursos AWS e on-premises a partir de qualquer lugar. Suporta autenticação multifator, integração com Active Directory e gerenciamento centralizado de conexões de usuários remotos.

#### 13.2. Amazon CloudFront

É uma rede de distribuição de conteúdo (CDN) que entrega dados, vídeos, aplicações e APIs com baixa latência e alta transferência global. Utiliza uma rede global de edge locations para cache e aceleração de conteúdo, otimizando a experiência do usuário final.

#### 13.3. AWS Direct Connect

É um serviço que estabelece conexões de rede dedicadas e privadas entre data centers, escritórios ou ambientes on-premises e a AWS, oferecendo maior largura de banda, menor latência e segurança em comparação com conexões via internet pública.

#### 13.4. ELB (Elastic Load Balancing)

É um serviço que distribui automaticamente o tráfego de entrada entre múltiplas instâncias ou containers, garantindo alta disponibilidade e escalabilidade de aplicações. Suporta diferentes tipos de balanceadores, incluindo Application, Network e Gateway Load Balancer.

#### 13.5. AWS Global Accelerator

É um serviço que melhora a disponibilidade e desempenho de aplicações globais ao direcionar o tráfego de usuários para endpoints ótimos usando a rede global da AWS. Fornece endereços IP estáveis e failover automático entre regiões.

#### 13.6. AWS PrivateLink

É um serviço que permite acessar serviços AWS e aplicações próprias de forma privada, usando endpoints de rede dentro da VPC, evitando exposição na internet pública. Facilita conexões seguras entre VPCs e ambientes híbridos.

#### 13.7. Amazon Route 53

É um serviço de DNS escalável e altamente disponível que gerencia o roteamento de usuários para aplicações através de políticas de roteamento baseadas em latência, geolocalização, failover e balanceamento de carga.

#### 13.8. AWS Site-to-Site VPN

É um serviço que estabelece túneis VPN IPsec entre redes on-premises e VPCs na AWS, garantindo comunicação segura e criptografada para ambientes híbridos e acesso remoto de redes corporativas.

#### 13.9. AWS Transit Gateway

É um serviço que simplifica a conexão e gerenciamento de múltiplas VPCs e redes on-premises, atuando como um hub central para roteamento eficiente e escalável, reduzindo a complexidade e custos de interconexão.

#### 13.10. Amazon VPC (Virtual Private Cloud)

É um serviço que permite provisionar uma rede virtual isolada na nuvem, onde é possível definir sub-redes, tabelas de roteamento, gateways e políticas de segurança para controlar o ambiente de rede de recursos AWS.

## 14. Segurança, identidade e conformidade

#### 14.1. AWS IAM (Identity and Access Management)

É um serviço que permite gerenciar usuários, grupos, permissões e políticas para controlar o acesso a recursos AWS com segurança, implementando princípios de menor privilégio e autenticação multifator.

#### 14.2. AWS IAM Identity Center (AWS Single Sign-On)

É um serviço que centraliza o gerenciamento de acesso e autenticação para múltiplas contas e aplicações AWS, permitindo o login único (SSO) com controle granular de permissões e integração com provedores externos.

#### 14.3. AWS KMS (Key Management Service)

É um serviço gerenciado para criação, armazenamento e controle de chaves criptográficas usadas para proteger dados, com suporte a operações de criptografia, rotação automática e políticas detalhadas de acesso.

#### 14.4. AWS Secrets Manager

É um serviço que gerencia, recupera e rotaciona automaticamente segredos, como senhas, chaves API e tokens, permitindo acesso seguro e programático a informações sensíveis usadas em aplicações.

#### 14.5. Amazon Cognito

É um serviço que gerencia autenticação, autorização e sincronização de usuários para aplicações web e móveis, suportando login social, diretório de usuários próprio e integração com provedores de identidade corporativos.

#### 14.6. AWS Directory Service

É um serviço que permite configurar e gerenciar diretórios Microsoft Active Directory ou diretórios compatíveis para autenticação e controle de acesso em ambientes AWS, suportando integração com ambientes on-premises.

#### 14.7. AWS RAM (Resource Access Manager)

É um serviço que permite compartilhar recursos AWS entre contas e organizações de forma segura, facilitando a colaboração e o uso eficiente de recursos sem necessidade de replicação.

#### 14.8. AWS Artifact

É um serviço que fornece acesso sob demanda a relatórios de conformidade e documentos de auditoria da AWS, facilitando a verificação dos controles de segurança e o alinhamento com requisitos regulatórios e padrões de governança.

#### 14.9. AWS Audit Manager

É um serviço que automatiza a coleta de evidências e avaliações para auditorias de conformidade, permitindo criar frameworks personalizados e monitorar controles para reduzir o esforço manual e acelerar processos de auditoria.

#### 14.10. AWS ACM (Certificate Manager)

É um serviço que facilita a provisão, gerenciamento e renovação automática de certificados SSL/TLS públicos e privados para proteger a comunicação entre clientes e aplicações, simplificando a configuração de segurança para sites e serviços.

#### 14.11. AWS CloudHSM

É um serviço que oferece módulos de segurança de hardware (HSM) dedicados para geração e gerenciamento de chaves criptográficas, garantindo controle exclusivo e conformidade rigorosa com padrões de segurança para dados sensíveis.

#### 14.12. Amazon Macie

É um serviço que usa machine learning para identificar e proteger dados sensíveis, como informações pessoais identificáveis (PII), em armazenamentos como S3, detectando riscos e ajudando a manter conformidade com privacidade.

#### 14.13. Amazon GuardDuty

É um serviço de detecção de ameaças contínuo que monitora eventos e atividades suspeitas em contas e workloads AWS, usando machine learning e inteligência de ameaças para identificar comportamentos maliciosos.

#### 14.14. Amazon Inspector

É um serviço automatizado que avalia a segurança e conformidade de instâncias EC2 e contêineres, identificando vulnerabilidades, exposições e desvios em configurações para fortalecer a postura de segurança.

#### 14.15. Amazon Detective

É um serviço que analisa dados de segurança para identificar, investigar e entender ameaças e comportamentos suspeitos em contas AWS, facilitando a detecção rápida de incidentes e ações corretivas.

#### 14.16. AWS Firewall Manager

É um serviço que facilita a configuração centralizada e o gerenciamento de regras de firewall para proteger múltiplas contas e recursos AWS, automatizando políticas de segurança consistentes para WAF, Shield Advanced e Network Firewall.

#### 14.17. AWS WAF (Web Application Firewall)

É um serviço que protege aplicações web contra ataques comuns, como SQL injection e cross-site scripting, permitindo definir regras personalizadas para bloquear tráfego malicioso antes que alcance os recursos backend.

#### 14.18. AWS Shield

É um serviço de proteção contra ataques DDoS que oferece detecção e mitigação automática para proteger aplicações AWS contra interrupções causadas por ataques volumétricos e sofisticados.

#### 14.19. AWS Network Firewall

É um serviço gerenciado que oferece firewall de rede com regras configuráveis para proteger VPCs contra tráfego malicioso, suportando inspeção de pacotes, filtragem baseada em regras e proteção contra ameaças avançadas.

#### 14.20. AWS Security Hub

É um serviço que centraliza e consolida dados de segurança de múltiplas fontes dentro da AWS, oferecendo visibilidade unificada, análises e recomendações para melhorar a postura de segurança.

## 15. Sem servidor

#### 15.1. AWS Lambda

É um serviço de computação serverless que executa código em resposta a eventos, gerenciando automaticamente a infraestrutura subjacente. Permite execução de funções em vários idiomas, com escalabilidade automática e cobrança por tempo de execução.

#### 15.2. AWS Fargate

É uma solução de computação serverless para execução de containers, eliminando a necessidade de gerenciar servidores ou clusters, onde o provisionamento, escalabilidade e manutenção são gerenciados automaticamente pela AWS.

#### 15.3. AWS AppSync

É um serviço que facilita a criação de APIs GraphQL escaláveis e em tempo real, permitindo a sincronização eficiente de dados entre aplicações e fontes diversas, com gerenciamento automático de atualizações e segurança integrada.

## 16. Armazenamento

#### 16.1. Amazon S3 (Simple Storage Service)

É um serviço de armazenamento de objetos escalável, durável e altamente disponível, projetado para armazenar e recuperar qualquer volume de dados a qualquer momento, com controle de acesso, versionamento e políticas de ciclo de vida.

#### 16.2. Amazon S3 Glacier

É uma solução de armazenamento de arquivos a longo prazo com custo reduzido, ideal para arquivamento e retenção de dados, oferecendo opções de recuperação variando de minutos a horas, com segurança e durabilidade.

#### 16.3. Amazon EBS (Elastic Block Store)

É um serviço que fornece armazenamento em bloco persistente para instâncias EC2, oferecendo volumes duráveis, com alta performance e opções de replicação, snapshots e criptografia para atender a diferentes necessidades de aplicação.

#### 16.4. Amazon EFS (Elastic File System)

É um sistema de arquivos elástico e gerenciado que fornece armazenamento compartilhado para múltiplas instâncias EC2, com escalabilidade automática, alta disponibilidade e suporte a acesso simultâneo com protocolo NFS.

#### 16.5. Amazon FSx (File System)

É um serviço que oferece sistemas de arquivos gerenciados e otimizados para cargas específicas, como FSx for Windows File Server para ambientes Windows e FSx for Lustre para aplicações de alto desempenho em HPC.

#### 16.6. AWS Backup

É um serviço centralizado que automatiza e gerencia backups de dados para múltiplos serviços AWS e ambientes on-premises, garantindo políticas consistentes de backup, retenção e recuperação de dados para proteção contra perda.

#### 16.7. AWS Storage Gateway

É um serviço híbrido que conecta ambientes on-premises a armazenamento em nuvem AWS, permitindo acesso local a dados na nuvem por meio de protocolos de armazenamento tradicionais, facilitando backup, arquivamento e migração.

[<- Voltar para a página principal](../../README.md)
