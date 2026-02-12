# AWS Services - Visão Geral

Este documento apresenta um **resumo geral dos principais serviços da AWS**, organizados por categoria e função.

---

## Cloud Computing Essentials

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![S3](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Storage/AmazonS3/AmazonS3.svg) | **Simple Storage Service (S3)** | Serviço de **armazenamento de objetos** altamente escalável, durável e disponível. Ideal para armazenar imagens, vídeos, backups, logs e arquivos estáticos. |
| ![EC2](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Compute/AmazonEC2/AmazonEC2.svg) | **Elastic Compute Cloud (EC2)** | Serviço de **computação na nuvem** que fornece capacidade de servidores virtuais redimensionáveis. Permite executar aplicações na nuvem com controle total sobre o ambiente. |

---

## Cloud First Steps

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![Management Console](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/ManagementGovernance/AWSManagementConsole/AWSManagementConsole.svg) | **Management Console** | Interface web para **gerenciar e monitorar** todos os serviços AWS de forma centralizada. Ponto de entrada principal para acessar recursos da AWS. |
| ![IAM](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/SecurityIdentityCompliance/IAM/IAM.svg) | **IAM (Identity and Access Management)** | Serviço para **gerenciar identidades, acessos e permissões** dentro de uma conta AWS. Controla quem pode acessar quais recursos e serviços. |
| ![CloudWatch](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/ManagementGovernance/AmazonCloudWatch/AmazonCloudWatch.svg) | **CloudWatch** | Serviço de **monitoramento e observabilidade** que coleta métricas, logs e eventos. Permite monitorar aplicações, responder a mudanças e otimizar recursos. |

---

## Computing Solutions

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![EC2](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Compute/AmazonEC2/AmazonEC2.svg) | **Elastic Compute Cloud (EC2)** | Serviço de **computação virtual** com servidores na nuvem. Permite escolher tipo de instância, sistema operacional e configurações de rede. |
| ![Lambda](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Compute/AWSLambda/AWSLambda.svg) | **Lambda** | Serviço de **computação serverless** que executa código sob demanda sem gerenciar servidores. Paga apenas pelo tempo de execução. |
| ![Fargate](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Containers/AmazonFargate/AmazonFargate.svg) | **Fargate** | Serviço de **computação serverless para containers**. Permite executar containers sem gerenciar servidores ou clusters. |
| ![ECS](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Containers/AmazonECS/AmazonECS.svg) | **ECS (Elastic Container Service)** | Serviço **gerenciado de orquestração de containers** que suporta Docker. Facilita execução, escalonamento e gerenciamento de aplicações containerizadas. |

---

## Cloud Economics

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![Cost Explorer](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Billing/AmazonCostExplorer/AmazonCostExplorer.svg) | **Cost Explorer** | Ferramenta para **visualizar e analisar custos** da AWS ao longo do tempo. Permite identificar tendências e oportunidades de economia. |
| ![Budgets](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Billing/AWSBudgets/AWSBudgets.svg) | **Budgets** | Serviço para **definir orçamentos** e receber alertas quando custos excedem limites definidos. Ajuda a controlar gastos na nuvem. |
| ![Cost & Usage Report](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Billing/AWSCostAndUsageReport/AWSCostAndUsageReport.svg) | **Cost & Usage Report** | Relatório detalhado de **custos e uso** de serviços AWS. Fornece dados granulares para análise financeira e otimização. |

---

## Networking Concepts

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![VPC](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/NetworkingContentDelivery/AmazonVPC/AmazonVPC.svg) | **Virtual Private Cloud (VPC)** | Serviço que permite criar uma **rede virtual isolada e privada** na nuvem AWS. Controle total sobre configuração de rede, IPs e gateways. |
| ![Route 53](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/NetworkingContentDelivery/AmazonRoute53/AmazonRoute53.svg) | **Route 53** | Serviço de **DNS (Domain Name System)** gerenciado e altamente disponível. Roteia tráfego para aplicações e fornece registro de domínios. |
| ![API Gateway](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/ApplicationIntegration/AmazonAPIGateway/AmazonAPIGateway.svg) | **API Gateway** | Serviço para **criar, publicar e gerenciar APIs REST e WebSocket**. Atua como ponto de entrada para aplicações backend. |

---

## Connecting VPCs

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![VPC Peering](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/NetworkingContentDelivery/AmazonVPCPeering/AmazonVPCPeering.svg) | **VPC Peering** | Conexão de rede que permite **conectar duas VPCs** para comunicação privada usando IPv4 ou IPv6. Tráfego permanece na rede AWS. |
| ![Transit Gateway](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/NetworkingContentDelivery/AWSTransitGateway/AWSTransitGateway.svg) | **Transit Gateway** | Serviço de **rede centralizada** que conecta VPCs, VPNs e conexões Direct Connect. Simplifica arquitetura de rede e reduz complexidade. |
| ![Direct Connect](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/NetworkingContentDelivery/AWSDirectConnect/AWSDirectConnect.svg) | **Direct Connect** | Serviço que estabelece uma **conexão de rede dedicada** entre datacenter on-premises e AWS. Fornece largura de banda consistente e baixa latência. |
| ![VPN](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/NetworkingContentDelivery/AWSVPN/AWSVPN.svg) | **VPN Connection** | Conexão **VPN segura** entre rede on-premises e VPC na AWS. Permite acesso seguro a recursos na nuvem através de túnel criptografado. |

---

## First NoSQL Database

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![DynamoDB](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Database/AmazonDynamoDB/AmazonDynamoDB.svg) | **DynamoDB** | Banco de dados **NoSQL gerenciado** rápido e flexível. Oferece performance de milissegundos em qualquer escala, com backup automático e criptografia. |

---

## Storage and File Systems

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![S3](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Storage/AmazonS3/AmazonS3.svg) | **Simple Storage Service (S3)** | Serviço de **armazenamento de objetos** com diferentes classes de armazenamento para otimizar custos e performance. |
| ![EBS](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Storage/AmazonEBS/AmazonEBS.svg) | **EBS (Elastic Block Store)** | Serviço de **armazenamento em blocos** de alta performance para instâncias EC2. Volumes persistentes e duráveis para cargas de trabalho. |
| ![EFS](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Storage/AmazonEFS/AmazonEFS.svg) | **EFS (Elastic File System)** | Sistema de **arquivos gerenciado** e escalável para EC2. Suporta acesso simultâneo de múltiplas instâncias com consistência forte. |
| ![FSx](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Storage/AmazonFSx/AmazonFSx.svg) | **FSx** | Serviço de **sistemas de arquivos gerenciados** de terceira geração. Inclui FSx for Windows File Server e FSx for Lustre para workloads específicos. |

---

## Auto-healing and Scaling Applications

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![Auto Scaling](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Compute/AmazonEC2AutoScaling/AmazonEC2AutoScaling.svg) | **EC2 Auto Scaling** | Serviço que **ajusta automaticamente a capacidade** de instâncias EC2. Garante disponibilidade e escala baseado em demanda. |
| ![ELB](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/NetworkingContentDelivery/ElasticLoadBalancing/ElasticLoadBalancing.svg) | **ELB (Elastic Load Balancer)** | Serviço que **distribui tráfego** entre múltiplas instâncias ou containers. Melhora disponibilidade e tolerância a falhas. |
| ![CloudFront](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/NetworkingContentDelivery/AmazonCloudFront/AmazonCloudFront.svg) | **CloudFront** | Rede de **distribuição de conteúdo (CDN)** global. Entrega conteúdo estático e dinâmico com baixa latência e alta velocidade de transferência. |

---

## Serverless Architectures

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![S3](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Storage/AmazonS3/AmazonS3.svg) | **Simple Storage Service (S3)** | Armazenamento serverless que **não requer provisionamento** de servidores. Escala automaticamente. |
| ![Lambda](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Compute/AWSLambda/AWSLambda.svg) | **Lambda** | Execução de código **serverless** que escala automaticamente. Executa funções em resposta a eventos. |
| ![API Gateway](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/ApplicationIntegration/AmazonAPIGateway/AmazonAPIGateway.svg) | **API Gateway** | API **serverless** que escala automaticamente. Gerencia tráfego, autenticação e autorização. |
| ![Step Functions](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/ApplicationIntegration/AWSStepFunctions/AWSStepFunctions.svg) | **Step Functions** | Orquestração de **workflows serverless**. Coordena múltiplos serviços AWS em processos visuais. |

---

## DevOps and Continuous Delivery

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![Code Commit](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/DeveloperTools/AWSCodeCommit/AWSCodeCommit.svg) | **Code Commit** | Serviço de **controle de versão gerenciado** baseado em Git. Repositórios privados e seguros para código. |
| ![Code Build](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/DeveloperTools/AWSCodeBuild/AWSCodeBuild.svg) | **Code Build** | Serviço de **compilação gerenciada** que compila código-fonte, executa testes e produz artefatos prontos para deploy. |
| ![Code Deploy](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/DeveloperTools/AWSCodeDeploy/AWSCodeDeploy.svg) | **Code Deploy** | Serviço que **automatiza deployments** para instâncias EC2, Lambda, ECS e serviços on-premises. Reduz tempo de inatividade. |
| ![Code Pipeline](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/DeveloperTools/AWSCodePipeline/AWSCodePipeline.svg) | **Code Pipeline** | Serviço de **CI/CD totalmente gerenciado** que automatiza pipelines de release. Integra Code Commit, Code Build e Code Deploy. |

---

## Relational Database Solutions

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![RDS](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Database/AmazonRDS/AmazonRDS.svg) | **RDS (Relational Database Service)** | Serviço de **banco de dados relacional gerenciado**. Suporta MySQL, PostgreSQL, MariaDB, Oracle e SQL Server com backups automáticos. |
| ![Aurora](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/Database/AmazonAurora/AmazonAurora.svg) | **Aurora** | Banco de dados relacional **compatível com MySQL e PostgreSQL** com performance até 5x superior. Alta disponibilidade e durabilidade. |

---

## Monitoring and Observability

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![CloudWatch](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/ManagementGovernance/AmazonCloudWatch/AmazonCloudWatch.svg) | **CloudWatch** | Serviço de **monitoramento e observabilidade** que coleta métricas, logs e eventos de recursos AWS e aplicações. |
| ![CloudTrail](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/ManagementGovernance/AWSCloudTrail/AWSCloudTrail.svg) | **CloudTrail** | Serviço que **registra atividade de API** e ações de usuários, roles e serviços AWS. Essencial para auditoria e compliance. |
| ![Config](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/ManagementGovernance/AWSConfig/AWSConfig.svg) | **Config** | Serviço que **avalia, audita e avalia configurações** de recursos AWS. Rastreia mudanças e verifica conformidade com regras. |
| ![X-Ray](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/DeveloperTools/AWSX-Ray/AWSX-Ray.svg) | **X-Ray** | Serviço que ajuda a **analisar e depurar aplicações distribuídas**. Visualiza requisições e identifica gargalos de performance. |

---

## Messaging and Queuing

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![SNS](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/ApplicationIntegration/AmazonSNS/AmazonSNS.svg) | **SNS (Simple Notification Service)** | Serviço de **notificações pub/sub gerenciado**. Envia mensagens para múltiplos assinantes via email, SMS, HTTP, Lambda, etc. |
| ![SQS](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/ApplicationIntegration/AmazonSQS/AmazonSQS.svg) | **SQS (Simple Queue Service)** | Serviço de **filas de mensagens gerenciado**. Desacopla componentes de aplicações e permite comunicação assíncrona entre serviços. |
| ![MQ](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/ApplicationIntegration/AmazonMQ/AmazonMQ.svg) | **MQ (Amazon MQ)** | Serviço de **message broker gerenciado** para Apache ActiveMQ e RabbitMQ. Migração fácil de message brokers existentes. |

---

## Security and Compliance

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![IAM](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/SecurityIdentityCompliance/IAM/IAM.svg) | **IAM (Identity and Access Management)** | Serviço para **gerenciar acessos e permissões**. Controla quem pode fazer o quê na conta AWS. |
| ![WAF](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/SecurityIdentityCompliance/AWSWAF/AWSWAF.svg) | **WAF (Web Application Firewall)** | Serviço que **protege aplicações web** contra vulnerabilidades comuns. Filtra e monitora requisições HTTP/HTTPS. |
| ![Shield](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/SecurityIdentityCompliance/AWSShield/AWSShield.svg) | **Shield** | Serviço de **proteção contra DDoS (Distributed Denial of Service)**. Protege aplicações na AWS contra ataques. |
| ![GuardDuty](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/SecurityIdentityCompliance/AmazonGuardDuty/AmazonGuardDuty.svg) | **GuardDuty** | Serviço de **detecção de ameaças gerenciado** que monitora continuamente ambientes AWS. Identifica atividades maliciosas. |
| ![Secrets Manager](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/SecurityIdentityCompliance/AWSSecretsManager/AWSSecretsManager.svg) | **Secrets Manager** | Serviço para **gerenciar segredos** como senhas, tokens e chaves de API. Rotação automática e integração com serviços AWS. |
| ![KMS](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/SecurityIdentityCompliance/AWSKeyManagementService/AWSKeyManagementService.svg) | **KMS (Key Management Service)** | Serviço para **criar e gerenciar chaves de criptografia**. Controla uso de chaves criptográficas em aplicações AWS. |
| ![NACL](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/NetworkingContentDelivery/AmazonVPCSecurityGroups/AmazonVPCSecurityGroups.svg) | **NACL (Network Access Control Lists)** | **Firewall opcional** na camada de sub-rede da VPC. Controla tráfego de entrada e saída em nível de rede. |
| ![Security Groups](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/NetworkingContentDelivery/AmazonVPCSecurityGroups/AmazonVPCSecurityGroups.svg) | **Security Groups** | **Firewall virtual** que controla tráfego de entrada e saída para instâncias EC2. Regras de permissão baseadas em porta e protocolo. |

---

## Migration to the Cloud

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![Application Migration Service](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/MigrationTransfer/AWSApplicationMigrationService/AWSApplicationMigrationService.svg) | **Application Migration Service** | Serviço que **automatiza migração de aplicações** de servidores físicos, virtuais ou cloud para AWS. Minimiza tempo de inatividade. |
| ![DMS](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/MigrationTransfer/AWSDatabaseMigrationService/AWSDatabaseMigrationService.svg) | **DMS (Database Migration Service)** | Serviço para **migrar bancos de dados** para AWS de forma segura. Suporta migração homogênea e heterogênea com tempo de inatividade mínimo. |
| ![Snowball](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/MigrationTransfer/AWSSnowball/AWSSnowball.svg) | **Snowball** | Dispositivo físico para **transferir grandes volumes de dados** para AWS offline. Ideal quando conexão de internet não é suficiente. |
| ![DataSync](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/MigrationTransfer/DataSync/DataSync.svg) | **DataSync** | Serviço que **acelera transferência de dados** entre on-premises e AWS. Simplifica migração de dados e sincronização contínua. |

---

## Machine Learning and AI

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![Comprehend](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/MachineLearning/AmazonComprehend/AmazonComprehend.svg) | **Comprehend** | Serviço de **processamento de linguagem natural (NLP)** que extrai insights de texto. Identifica sentimentos, entidades e tópicos. |
| ![SageMaker](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/MachineLearning/AmazonSageMaker/AmazonSageMaker.svg) | **SageMaker** | Plataforma **totalmente gerenciada para machine learning**. Permite construir, treinar e implantar modelos de ML rapidamente. |
| ![Lex](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/MachineLearning/AmazonLex/AmazonLex.svg) | **Lex** | Serviço para **construir interfaces conversacionais** usando voz e texto. Usa tecnologia de deep learning para reconhecimento de fala. |
| ![Rekognition](https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/main/dist/MachineLearning/AmazonRekognition/AmazonRekognition.svg) | **Rekognition** | Serviço de **análise de imagens e vídeos** usando deep learning. Detecta objetos, pessoas, texto, cenas e atividades. |

---

## Resumo

Esta visão geral apresenta os principais serviços AWS organizados por categoria em formato de tabela com ícones oficiais do repositório GitHub da AWS. Cada serviço resolve necessidades específicas de computação, armazenamento, rede, segurança, banco de dados, monitoramento e muito mais, permitindo construir arquiteturas completas e escaláveis na nuvem.
