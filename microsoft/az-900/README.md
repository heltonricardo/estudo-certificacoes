# AZ-900: Microsoft Azure Fundamentals

[Voltar para a página principal](../../README.md)

<img src="assets/badge.svg" alt="AZ-900: Microsoft Azure Fundamentals" width="200"/>

<hr />

## MODELOS DE CLOUD

### IaaS (Infraestrutura como serviço)

- Alugar servidores físicos;
- Para quem não quer ter o serviço de cloud público;
- Você tem que gerenciar os próprios servidores;
- Você aplica as próprias licenças;
- Você instala os softwares necessários.

### PaaS (Plataforma como serviço)

- Quando se utiliza uma aplicação oferecida pelo próprio Azure, como um CND, por exemplo;
- Você paga pela utilização e não se preocupa com licença de software.

### SaaS (Software como serviço)

- Por exemplo o Office 365;
- Não precisa se preocupar com atualizações ou manutenções.

<hr />

## TIPOS DE CLOUD

### Private ($$$)

- Quando você monta a própria estrutura cloud;
- Monta sua estrutura cloud em um espaço de datacenter;
- Você precisa se preocupar com licenças, hardwares, manutenções
- Muito utilizado por quem não gosta dos outros dois tipos. Exemplo: bancos e governos, que não querem que um terceiro faça manutenção ou tenha acesso físico.

### Public ($): Mais usado pela facilidade e preço

- É como a AWS, Azure ou Google Cloud. Essas empresas tomam conta de toda a parte física e você somente aluga a parte virtual (VMs, DBs etc).

### Hybrid ($$)

- Traz recursos de ambos os tipos já citados, permitindo usar VMs e máquinas físicas para aplicações específicas, por exemplo.

<hr />

## ESTRUTURA DA MICROSOFT AZURE

### Availability Zone (Zona de disponibilidade)

- São os datacenters propriamente ditos: os prédios, com ar condicionado, sistemas de gestão de energia elétrica;
- Onde ficam instalados os racks com memórias, processadores, discos etc.

### Region (Região)

- São localizações geográficas que possuem 3 ou mais Zonas de Disponibilidade. Todas as zonas dentro de uma Região são espelhadas, ou seja, caso ocorra algum desastre e umas das Zonas fique indisponível, as outras servirão os clients sem mesmo que eles notem (uma VM não será reiniciada, por exemplo). Dentro de uma região, todas as Zonas de disponibilidade funcionam como um só datacenter.

> Nem todas as regiões possuem todos os serviços oferecidos pelo Azure, e os valores podem alterar de acordo com a localização.

<hr />

## GRUPOS DE RECURSOS

Maneira usada para separar seus recursos. Por exemplo: você pode criar um grupo para cada setor da empresa ou filial, ou para cada estado, ou país. É bem flexível e permite gerir melhor os seus recursos, podendo visualizar, por exemplo, o quanto cada grupo custa para manter.

<hr />

## MÁQUINA VIRTUAL

1. Primeiro, criamos um grupo de recursos:

   - Procure na tela inicial ou digite `Grupos de Recursos`
   - Clique em `Criar`
   - Em `Grupo de recursos`, insira um nome, por exemplo `Servidores`
   - Escolha uma região
   - Clique em `Revisar + criar`
   - Clique em `Criar`

1. Agora sim, criamos a máquina virtual

   - Procure na tela inicial ou digite `Máquinas Virtuais`
   - Clique em `Criar`
   - Clique em `Máquina virtual`
   - Guia `Básico`:
     - Escolha o `Grupo de Recursos` criado anteriormente
     - Insira um nome para máquina virtual, exemplo: `Servidor01`
     - Escolha uma região
     - Para o exemplo, deixaremos sem redundância para `Opções de disponibilidade`
     - Agora, para a `Imagem`, utilizaremos um Windows, exemplo: `Windows Server 2019 Datacenter - Gen2`
     - Em `Tamanho`, escolheremos a mais barata por mês (esse valor é cobrado se a máquina ficar ligada durante todos os dias do mês. Para fins de teste, ligaremos e desligaremos quando necessário, gerando um custo bem baixo para a máquina - o que será descontado do crédito inicial grátis que a própria Microsoft oferece ao criarmos a conta)
     - Insira um nome de usuário e senha para criar uma conta dentro do SO
     - Deixe `RDP (3389)` em `Selecione as portas de entradas`
   - Guia `Discos`:
     - Deixaremos as opções padrão
   - Guia `Rede`:
     - Deixaremos as opções padrão
   - Guia `Gerenciamento`:
     - Deixaremos as opções padrão
   - Guia `Avançado`:
     - Deixaremos as opções padrão
   - Guia `Marcas` (Tags):
     - Insira um nome, por exemplo: `Server`
     - Insira um valor, por exemplo: `Servidor01`
   - Clique em `Revisar + criar`
   - Clique em `Criar`

1. Vamos agora acessar a máquina criada

   - Ao finalizar a criação, clique em `Ir para o recurso`
   - Procure na tela inicial ou digite `Máquinas Virtuais`
   - Clique no nome do servidor criado anteriormente
   - Clique em `Conectar`
   - Clique em `RDP`
   - Baixe o arquivo RDP
   - Execute o arquivo baixado
   - Clique em `Conectar`
   - Insira seu usuário e senha criados anteriormente
   - Para encerrar a sessão, basta fechar a guia do RDP (note, em seu gerenciador do Azure, que a máquina continua ligada = cobrando)

1. Excluindo a VM

   - Na mesma tela de conexão, clique em `Excluir`
   - Selecione todos os recursos associados à máquina, como discos, interfaces e outros (eles continuarão consumindo créditos se não excluídos)
   - Aceite os termo
   - Clique em `Excluir`

<hr />

## CLI - COMMAND-LINE INTERFACE

O Command-Line Interface - Interface de Linha de Comando - serve para executarmos comandos do Azure a partir da sua máquina local, não sendo necessário acessar o painel visual da Microsoft Azure. É necessário configurar seu terminal. Existe também o Cloud Shell, um terminal disponível no próprio painel do Azure, que pode ser usado diretamente do navegador de internet.

<hr />

## MARKETPLACE

Loja com soluções, pagas e gratuitas, que já foram criadas por terceiros ou pela Microsoft. Por exemplo: é possível criar uma VM que já venha com aplicações instaladas e configuradas.

<hr />

## VM SCALE SET - CONJUNTOS DE ESCALAS DE VMs

É um artifício que permite que criemos agrupamentos de VMs para escalar a performance (aumentando ou diminuindo recursos) de acordo com algum parâmetro. Por exemplo: quando montamos um site em uma VM esperando poucos acessos, costumamos economizar no hardware, mas se essa máquina começa a receber muitos acessos simultâneos, provavelmente travará. Por isso, usamos o Scale Set. Definindo que: ao chegar em 50% de processamento na CPU, deve ser criada uma cópia da VM que também começará a receber acessos (balanceados pelo próprio Azure). Você pode definir a quantidade mínima e máxima de VMs. Quando a demanda não é mais necessária, o Scale Set trata de excluir as máquinas extras. Ele também ajuda de outra maneira: se definirmos que sempre serão no mínimo duas máquinas e uma delas falhar, ele mesmo será responsável por criar outra e excluir a defeituosa.

<hr />

## APP SERVICE

Recurso que permite que enviemos o código fonte de um sistema, e o próprio Azure fica responsável por criar e configurar a estrutura para executar a aplicação. Aceita várias linguagens, como: Java, Python, .Net e PHP.

<hr />

## ACI - AZURE CONTAINER INSTANCE

Sistema do Azure que permite mandarmos a imagem da aplicação para os servidores da Microsoft.

<hr />

## AKS - AZURE KUBERNETE SERVICE

Sistema do Azure para gerenciamento de orquestradores de containers.

<hr />

## AVD - AZURE VIRTUAL DESKTOP

A área de trabalho virtual do Azure é um recurso que permite criar máquinas que servem como desktops e podem ser acessadas por aplicativos ou pelo navegador de internet.

<hr />

## APLICATIVO DE FUNÇÕES

Recurso que permite criarmos funções de aplicativos para serem executadas somente quando necessárias. Isso torna possível diminuir o hardware para executar uma aplicação inteira e custeando partes dessa aplicação somente enquanto são executadas. A vantagem é que não é preciso duplicar a aplicação toda quando existe grande demanda, o autoscale gerencia tudo e criará mais instâncias de cada função sob demanda.

<hr />

## VNET

As redes virtuais são artifícios que possibilitam o isolamento de máquinas dentro de diferentes redes.

#### Como criar uma VNET dentro do Azure:

- Guia `Básico`
  1. Acesse o recurso `Redes virtuais`
  1. Clique em `Criar`
  1. Escolha ou crie um grupo de recursos. Ex: Dev
  1. Insira um nome para a VNET. Ex: Dev
- Guia `Endereços IP`
  1. Usaremos a rede sugerida: `10.1.0.0/16`
- Guia `Segurança`
  1. Habilite o BastionHost - recurso que permite que acessemos as máquinas dentro da VNET de forma remota
  1. Insira um nome. Ex: Dev-Bastion
  1. Insira uma sub-rede para o bastion. Ex: `10.1.2.0/24`
  1. Em `Endereço IP público` selecione um ou crie clicando em `Crie um` e inserindo um nome. Ex: Dev-Public
- Clique em `Revisar + criar`
- Clique em `Criar` e aguarde a finalização

#### Criando VMs dentro da VNET

Agora basta seguir o guia de como criar uma máquina virtual (alguns tópicos acima - utilize uma imagem Linux para facilitar) e na guia `Redes` selecionar, para `Rede Virtual`, a rede criado no passo anterior. Para o exemplo, criaremos duas máquinas dentro dessa rede VNET.

#### Testando a conexão das VMs

Com as máquinas criadas, precisamos verificar se ambas têm conexão com a internet e entre si:

1. Entre no recurso de Máquina Virtual no Azure
1. Selecione uma delas
1. Clique em `Conectar` > `Bastion`
1. Insira suas credenciais de usuário escolhidas durante a criação da VM
1. Clique em `Conectar` (uma nova guia do navegador será aberta com o terminal da máquina)
1. Execute o comando `sudo su`
1. Execute o comando `ifconfig` (caso precise instalar, execute: `apt install net-tools`)
1. Procure pelo endereço que segue a palavra `inet` na seção `eth0` - provavelmente será `10.1.0.4` - esse é o endereço IP da VM (o Azure costuma utilizar os 3 primeiros IPs disponíveis dentro de cada rede). O IP da máquina virtual também é informado no painel do Azure: depois de selecionar a VM, procure a seção `Propriedades`
1. Execute o comando `ping 8.8.8.8` e verifique se ela possui acesso à internet
1. Execute o comando `ping <X>` (onde <X> é o IP da segunda VM) e verifique se ela possui acesso à outra máquina da mesma VNET

#### Excluindo os recursos

1. Excluindo as VMs
   1. Acesse o recurso de Máquina Virtual do Azure
   1. Selecione todas
   1. Clique em `...`
   1. Clique em `Excluir`
   1. No campo de confirmação, digite `Sim`
   1. Clique em `Excluir`
1. Excluindo a rede virtual
   1. Acesse o recurso de Redes Virtuais do Azure
   1. Selecione a rede criada
   1. Clique em `Dispositivos conectados`
   1. Selecione o BastionHost criado
   1. Clique em `Excluir` e confirme
   1. Faça o mesmo procedimento para os endereços das VMS
   1. No menu principal de Redes Virtuais, clique em `Excluir` e confirme

<hr />

## LOAD BALANCER

Um Balanceador de Cargas gerencia os acessos para recursos de múltiplas origens. Ex: quando usamos VM Scale Set (citado acima), um mesmo recurso passa a ter várias origens (VMs clones) e é o Load Balancer quem recebe todo o tráfego externo e distribui as solicitações para as VMs de acordo com as configurações que ele tem.

Nessa estrutura, podemos considerar o Load Balancer como algo que divide o sistema em duas partes. A primeira parte, visível publicamente, chamamos de `Fronted`. A segunda parte, composta pela área das VMs, é chamada de `Backend`.

<hr />

## VPN GATEWAY

É um recurso que cria um "túnel seguro" de conexão entre suas máquinas locais e suas máquinas virtuais no Azure, permitindo que todas as máquinas ajam como se estivessem no mesmo ambiente. Geralmente esse tipo de conexão requer uma senha forte para funcionar.

<hr />

## APPLICATION GATEWAY

O Gateway de Aplicativo é um recurso dentro do Balanceamento de carga que permite gerenciar o tráfego para os aplicativos, pois os balanceadores simples so operam o tráfego baseados no endereço IP. É possível encaminhar o tráfego com base na URL. Ex: se `/images` estiver na URL, você poderá encaminhar o tráfego para um conjunto específico de servidores (conhecido como um pool) configurado para as imagens.

<hr />

## EXPRESS ROUTE

A Rota Expressa é o suporte dado pelo Azure para clientes que desejam usar essa tecnologia. Nesse conceito, você entra em contato com a sua empresa de internet e solicita uma conexão direta entre você e o Azure. Isso permite atingir velocidades muito altas de transmissão de dados.

<hr />

## CDN - CONTENT DELIVERY NETWORK

É um recurso disponibilizado pelo Azure que duplica seu conteúdo para vários servidores ao redor do mundo a fim de otimizar a facilidade e velocidade de acesso para os clientes. Ex: Você cria um site no Brasil e ele é duplicado para outros servidores em outros países. Portanto, quando um cliente requisitar esse site estando na Ásia, ele será servido com o conteúdo do servidor mais próximo a ele.

<hr />

## BLOB STORAGE

É um centro de armazenamento de arquivos. É possível guardar todos os arquivos lá e somente referenciá-los nos seus sites, por exemplo, permitindo que as VMs possam ser mais enxutas em questões de hardware. A Microsoft definiu três maneiras de precificar o BLOB:

- Hot $$$: Para arquivos acessados e modificados frequentemente
- Cool $$: Para arquivos acessados e modificados não frequentemente
- Archive $: Para arquivos que quase nunca são acessados e modificados. EX: backups

#### Criando um Blob Storage

1. Acesse o recurso Contas de Armazenamento
1. Clique em `Criar`
1. Selecione o grupo de recurso
1. Insira um nome da conta de armazenamento
1. Clique em `Examinar + criar`
1. Clique em `Criar`
1. Acesse o recurso Gerenciador de Armazenamento
1. Expanda sua inscrição ativa do Azure
1. Expanda sua conta de armazenamento
1. Clique com o botão direito do mouse em cima de `Contêineres de blob`
1. Clique em `Criar contêiner de blob`
1. Escolha um nome e um nível de acesso
1. Clique em `Criar`

#### Fazendo upload de um arquivo

1. Acesse o recurso Gerenciador de Armazenamento
1. Expanda sua inscrição ativa do Azure
1. Expanda sua conta de armazenamento
1. Selecione o Contêiner de blob criado
1. Clique em `Carregar`
1. Selecione o arquivo
1. Clique em `Carregar`

Selecionando o arquivo, ao clica em `Copiar URL`, é copiado para sua área de transferência o endereço desse arquivo no Azure

<hr />

## DISCOS

Os discos de armazenamento com sistemas operacionais usados nas VMs podem ser classificados em:

- `HDD`: Mais lento, mais barato, excelente para backups
- `Standard SSD`: Mais rápido, mais caro, para alta disponibilidade de dados
- `Premium SSD`: Muito mais rápido, muito mais caro, para aplicações muito sensíveis à latência
- `Ultra Disk`: é um `Premium SSD` que consegue chegar a até 64TB de espaço disponível para armazenamento. O valor é extremamente elevado, comparado às outras opções

<hr />

## BANCO DE DADOS

O Azure tem suporte a diversos Sistemas Gerenciadores de Banco de Dados (SGBD), entre eles o Cosmos DB. Vamos criar um:

1. Acesse o recurso `Azure Cosmos DB`
1. Clique em `Criar`
1. Selecione a API mais adequada, usaremos `Núcleo (SQL)`
1. Guia `Noções básicas`
   1. Selecione um grupo de recursos
   1. Insira um nome. Ex: testedb
   1. Escolha uma localização. Ex: Oeste dos EUA 2
1. Guia `Distribuição Global`
   1. Habilite a redundância geográfica
1. Guia `Política de Backup`
   1. Escolha a política de backup mais adequada (`Periódico`: backup por tempo; `Contínuo`: backup quando ocorre uma alteração)
   2. Configure como necessário
1. Clique em `Examinar + criar`
1. Clique em `Criar`

O Azure possui uma ferramenta de migração de banco de dados para que você possa enviar o seu banco de dados local, ou até mesmo de outro provedor cloud, para ela de forma fácil e rápida. Essa funcionalidade é encontrada no recurso `Serviços de Migração de Banco de Dados do Azure`

<hr />

## SEGURANÇA

A Microsoft disponibiliza camadas de proteção para os dados armazenados, chamadas de Defesa em Profundidade:

- `Física`: proteção de quem pode entrar nos prédios e datacenters
- `Identidade e Acesso`: proteção de quem pode fazer login em sua conta com múltiplo fator de autenticação e logs
- `Perimiter`: proteção entre sua topologia e a internet, como firewalls
- `Rede`: proteção da comunicação entre recursos, que é negada por padrão
- `Computação`: proteção quanto a forma de acessar os recursos dentro do Azure, como BastionHost
- `Aplicação`: proteção em relação à atualização dos softwares
- `Dados`: proteção com criptografia de arquivos

<hr />

## FIREWALL

É um recurso suportado pelo Azure para permitir e bloquear solicitações de recursos entre ele e a internet. O comportamento padrão sempre é negar tudo, até que sejam adicionadas regras permissivas.

<hr />

## KEY VAULT

O cofre de senhas da Azure é um sistemas de armazenamento seguro de usuários e senhas das aplicações e gerência de credenciais. Por exemplo: tem-se um banco de dados cujo usuário e senha foram armazenados no cofre. Uma empresa terceira precisa ter acesso ao seu banco de dados. Então você gera uma credencial exclusiva que essa empresa poderá utilizar até que a credencial seja suspensa.

<hr />

## MICROSOFT SENTINEL

Solução que oferece análise inteligente de segurança e inteligência contra ameaças em toda a empresa, com uma solução para detecção de alertas, visibilidade de ameaças, procura proativa e resposta a ameaças.

<hr />

## IoT do Azure

A Internet das Coisas (IoT) do Azure é uma coleção de serviços cloud geridos pela Microsoft que controlam milhões de recursos de IoT. Uma solução IoT é composta por um ou mais dispositivos IoT que comunicam com um ou mais serviços de backend alojados na cloud.

<hr />

## Azure Big Data

Solução de arquitetura Big Data projetada para lidar com ingestão, processamento e análise de dados grandes ou complexos demais para sistemas de banco de dados tradicionais. Inclui muitos serviços que podem ser usados em uma arquitetura de Big Data. Eles se enquadram em duas categorias:

- `Serviços gerenciados`: que possuem o nome do Azure, como Azure Data Lake Store, Azure Data Lake Analytics e Hub de Eventos do Azure
- `Tecnologias de software livre baseadas na plataforma Apache Hadoop`, tecnologias que não carregam o nome do Azure, como HDFS, HBase, Hive, Pig e Spark

Considere este estilo de arquitetura quando você precisar:

- Armazenar e processar dados em volumes muito grandes para um banco de dados tradicional.
- Transformar dados não estruturados para análise e relatório.
- Capturar, processar e analisar fluxos não associados de dados em tempo real ou com baixa latência.
- Usar Azure Machine Learning ou Serviços Cognitivos da Microsoft.

<hr />

## Azure Machine Learning

Serviço de nuvem para acelerar e gerenciar o ciclo de vida dos projetos de machine learning. Os cientistas de dados e os engenheiros de ML encontrarão ferramentas para acelerar e automatizar seus fluxos de trabalho. Os desenvolvedores de aplicativos encontrarão ferramentas para integrar modelos em aplicativos ou serviços. Os desenvolvedores de plataforma encontrarão um conjunto robusto de ferramentas para a criação de ferramentas avançadas de ML.

<hr />

## ASSINATURAS

Sistema do Azure que gerencia todos os recursos dentro de uma conta. Geralmente tem-se uma conta por empresa. Cada conta pode ter várias assinaturas, conseguindo assim dividir a empresa em setores, áreas ou até mesmo entre filiais. Todo recurso criado é relacionado a uma assinatura

<hr />

## GERENCIAMENTO DE CUSTOS E ORÇAMENTO

Sistem do Azure que ajuda a gerir os custos do cliente com os serviços cloud. A Análise de Custo mostra de várias maneiras o custo e previsão dos custos para o período selecionado. Os orçamentos são avisos enviados por sms ou e-mail quando determinada condição de custo tornar-se verdadeira. Ex: Enviar um e-mail quando meu custo ultrapassar 80% do valor que tenho para gastar esse mês.

<hr />

## CALCULADORA DE PREÇO

Recurso do Azure que permite calcular a estimativa do custo dos serviços oferecidos. É bem completa, customizável e permite até mesmo verificar descontos quando contratamos serviços por períodos pré-estabelecidos pela Microsoft

<hr />

## PLANO DE SUPORTE

O Azure possui quatro tipos de suporte para os serviços do Azure

- `Básico`: padrão, já incluso
- `Developer`: $
- `Standad`: $$
- `Professional Direct`: $$$

No painel do Azure é possível alterar o seu plano de suporte

<hr />

## SLA - SERVICE LEVEL AGREEMENT

Seu contrato com o Microsoft Azure como cliente. Por exemplo: a Microsoft garante que sua VM estará 99.99% do tempo disponível para conexão. Caso isso não aconteça, faz parte dos termos que ela o reembolse de forma proporcional automaticamente

<hr />

## ATUALIZAÇÕES DO AZURE

Página das atualizações mais recentes sobre os produtos e recursos do Azure que mostra em que fase encontra-se a disponibilidade de cada um deles.

1. Em desenvolvimento
2. Preview
3. Disponível

[Voltar para a página principal](../../README.md)
