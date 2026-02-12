# AWS Services - Visão Geral

Este documento apresenta um **resumo geral dos principais serviços da AWS**, organizados por categoria e função.

---

## Cloud Computing Essentials

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![S3](https://d1.awsstatic.com/icons/aws-service-icon-s3.8c5c0c5e.svg) | **Simple Storage Service (S3)** | Serviço de **armazenamento de objetos** altamente escalável, durável e disponível. Ideal para armazenar imagens, vídeos, backups, logs e arquivos estáticos. |
| ![EC2](https://d1.awsstatic.com/icons/aws-service-icon-ec2.8c5c0c5e.svg) | **Elastic Compute Cloud (EC2)** | Serviço de **computação na nuvem** que fornece capacidade de servidores virtuais redimensionáveis. Permite executar aplicações na nuvem com controle total sobre o ambiente. |

---

## Cloud First Steps

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![Management Console](https://d1.awsstatic.com/icons/aws-service-icon-management-console.8c5c0c5e.svg) | **Management Console** | Interface web para **gerenciar e monitorar** todos os serviços AWS de forma centralizada. Ponto de entrada principal para acessar recursos da AWS. |
| ![IAM](https://d1.awsstatic.com/icons/aws-service-icon-iam.8c5c0c5e.svg) | **IAM (Identity and Access Management)** | Serviço para **gerenciar identidades, acessos e permissões** dentro de uma conta AWS. Controla quem pode acessar quais recursos e serviços. |
| ![CloudWatch](https://d1.awsstatic.com/icons/aws-service-icon-cloudwatch.8c5c0c5e.svg) | **CloudWatch** | Serviço de **monitoramento e observabilidade** que coleta métricas, logs e eventos. Permite monitorar aplicações, responder a mudanças e otimizar recursos. |

---

## Computing Solutions

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![EC2](https://d1.awsstatic.com/icons/aws-service-icon-ec2.8c5c0c5e.svg) | **Elastic Compute Cloud (EC2)** | Serviço de **computação virtual** com servidores na nuvem. Permite escolher tipo de instância, sistema operacional e configurações de rede. |
| ![Lambda](https://d1.awsstatic.com/icons/aws-service-icon-lambda.8c5c0c5e.svg) | **Lambda** | Serviço de **computação serverless** que executa código sob demanda sem gerenciar servidores. Paga apenas pelo tempo de execução. |
| ![Fargate](https://d1.awsstatic.com/icons/aws-service-icon-fargate.8c5c0c5e.svg) | **Fargate** | Serviço de **computação serverless para containers**. Permite executar containers sem gerenciar servidores ou clusters. |
| ![ECS](https://d1.awsstatic.com/icons/aws-service-icon-ecs.8c5c0c5e.svg) | **ECS (Elastic Container Service)** | Serviço **gerenciado de orquestração de containers** que suporta Docker. Facilita execução, escalonamento e gerenciamento de aplicações containerizadas. |

---

## Cloud Economics

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![Cost Explorer](https://d1.awsstatic.com/icons/aws-service-icon-cost-explorer.8c5c0c5e.svg) | **Cost Explorer** | Ferramenta para **visualizar e analisar custos** da AWS ao longo do tempo. Permite identificar tendências e oportunidades de economia. |
| ![Budgets](https://d1.awsstatic.com/icons/aws-service-icon-budgets.8c5c0c5e.svg) | **Budgets** | Serviço para **definir orçamentos** e receber alertas quando custos excedem limites definidos. Ajuda a controlar gastos na nuvem. |
| ![Cost & Usage Report](https://d1.awsstatic.com/icons/aws-service-icon-cost-and-usage-report.8c5c0c5e.svg) | **Cost & Usage Report** | Relatório detalhado de **custos e uso** de serviços AWS. Fornece dados granulares para análise financeira e otimização. |

---

## Networking Concepts

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![VPC](https://d1.awsstatic.com/icons/aws-service-icon-vpc.8c5c0c5e.svg) | **Virtual Private Cloud (VPC)** | Serviço que permite criar uma **rede virtual isolada e privada** na nuvem AWS. Controle total sobre configuração de rede, IPs e gateways. |
| ![Route 53](https://d1.awsstatic.com/icons/aws-service-icon-route53.8c5c0c5e.svg) | **Route 53** | Serviço de **DNS (Domain Name System)** gerenciado e altamente disponível. Roteia tráfego para aplicações e fornece registro de domínios. |
| ![API Gateway](https://d1.awsstatic.com/icons/aws-service-icon-api-gateway.8c5c0c5e.svg) | **API Gateway** | Serviço para **criar, publicar e gerenciar APIs REST e WebSocket**. Atua como ponto de entrada para aplicações backend. |

---

## Connecting VPCs

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![VPC Peering](https://d1.awsstatic.com/icons/aws-service-icon-vpc-peering.8c5c0c5e.svg) | **VPC Peering** | Conexão de rede que permite **conectar duas VPCs** para comunicação privada usando IPv4 ou IPv6. Tráfego permanece na rede AWS. |
| ![Transit Gateway](https://d1.awsstatic.com/icons/aws-service-icon-transit-gateway.8c5c0c5e.svg) | **Transit Gateway** | Serviço de **rede centralizada** que conecta VPCs, VPNs e conexões Direct Connect. Simplifica arquitetura de rede e reduz complexidade. |
| ![Direct Connect](https://d1.awsstatic.com/icons/aws-service-icon-direct-connect.8c5c0c5e.svg) | **Direct Connect** | Serviço que estabelece uma **conexão de rede dedicada** entre datacenter on-premises e AWS. Fornece largura de banda consistente e baixa latência. |
| ![VPN](https://d1.awsstatic.com/icons/aws-service-icon-vpn.8c5c0c5e.svg) | **VPN Connection** | Conexão **VPN segura** entre rede on-premises e VPC na AWS. Permite acesso seguro a recursos na nuvem através de túnel criptografado. |

---

## First NoSQL Database

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![DynamoDB](https://d1.awsstatic.com/icons/aws-service-icon-dynamodb.8c5c0c5e.svg) | **DynamoDB** | Banco de dados **NoSQL gerenciado** rápido e flexível. Oferece performance de milissegundos em qualquer escala, com backup automático e criptografia. |

---

## Storage and File Systems

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![S3](https://d1.awsstatic.com/icons/aws-service-icon-s3.8c5c0c5e.svg) | **Simple Storage Service (S3)** | Serviço de **armazenamento de objetos** com diferentes classes de armazenamento para otimizar custos e performance. |
| ![EBS](https://d1.awsstatic.com/icons/aws-service-icon-ebs.8c5c0c5e.svg) | **EBS (Elastic Block Store)** | Serviço de **armazenamento em blocos** de alta performance para instâncias EC2. Volumes persistentes e duráveis para cargas de trabalho. |
| ![EFS](https://d1.awsstatic.com/icons/aws-service-icon-efs.8c5c0c5e.svg) | **EFS (Elastic File System)** | Sistema de **arquivos gerenciado** e escalável para EC2. Suporta acesso simultâneo de múltiplas instâncias com consistência forte. |
| ![FSx](https://d1.awsstatic.com/icons/aws-service-icon-fsx.8c5c0c5e.svg) | **FSx** | Serviço de **sistemas de arquivos gerenciados** de terceira geração. Inclui FSx for Windows File Server e FSx for Lustre para workloads específicos. |

---

## Auto-healing and Scaling Applications

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![Auto Scaling](https://d1.awsstatic.com/icons/aws-service-icon-auto-scaling.8c5c0c5e.svg) | **EC2 Auto Scaling** | Serviço que **ajusta automaticamente a capacidade** de instâncias EC2. Garante disponibilidade e escala baseado em demanda. |
| ![ELB](https://d1.awsstatic.com/icons/aws-service-icon-elb.8c5c0c5e.svg) | **ELB (Elastic Load Balancer)** | Serviço que **distribui tráfego** entre múltiplas instâncias ou containers. Melhora disponibilidade e tolerância a falhas. |
| ![CloudFront](https://d1.awsstatic.com/icons/aws-service-icon-cloudfront.8c5c0c5e.svg) | **CloudFront** | Rede de **distribuição de conteúdo (CDN)** global. Entrega conteúdo estático e dinâmico com baixa latência e alta velocidade de transferência. |

---

## Serverless Architectures

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![S3](https://d1.awsstatic.com/icons/aws-service-icon-s3.8c5c0c5e.svg) | **Simple Storage Service (S3)** | Armazenamento serverless que **não requer provisionamento** de servidores. Escala automaticamente. |
| ![Lambda](https://d1.awsstatic.com/icons/aws-service-icon-lambda.8c5c0c5e.svg) | **Lambda** | Execução de código **serverless** que escala automaticamente. Executa funções em resposta a eventos. |
| ![API Gateway](https://d1.awsstatic.com/icons/aws-service-icon-api-gateway.8c5c0c5e.svg) | **API Gateway** | API **serverless** que escala automaticamente. Gerencia tráfego, autenticação e autorização. |
| ![Step Functions](https://d1.awsstatic.com/icons/aws-service-icon-step-functions.8c5c0c5e.svg) | **Step Functions** | Orquestração de **workflows serverless**. Coordena múltiplos serviços AWS em processos visuais. |

---

## DevOps and Continuous Delivery

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![Code Commit](https://d1.awsstatic.com/icons/aws-service-icon-codecommit.8c5c0c5e.svg) | **Code Commit** | Serviço de **controle de versão gerenciado** baseado em Git. Repositórios privados e seguros para código. |
| ![Code Build](https://d1.awsstatic.com/icons/aws-service-icon-codebuild.8c5c0c5e.svg) | **Code Build** | Serviço de **compilação gerenciada** que compila código-fonte, executa testes e produz artefatos prontos para deploy. |
| ![Code Deploy](https://d1.awsstatic.com/icons/aws-service-icon-codedeploy.8c5c0c5e.svg) | **Code Deploy** | Serviço que **automatiza deployments** para instâncias EC2, Lambda, ECS e serviços on-premises. Reduz tempo de inatividade. |
| ![Code Pipeline](https://d1.awsstatic.com/icons/aws-service-icon-codepipeline.8c5c0c5e.svg) | **Code Pipeline** | Serviço de **CI/CD totalmente gerenciado** que automatiza pipelines de release. Integra Code Commit, Code Build e Code Deploy. |

---

## Relational Database Solutions

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![RDS](https://d1.awsstatic.com/icons/aws-service-icon-rds.8c5c0c5e.svg) | **RDS (Relational Database Service)** | Serviço de **banco de dados relacional gerenciado**. Suporta MySQL, PostgreSQL, MariaDB, Oracle e SQL Server com backups automáticos. |
| ![Aurora](https://d1.awsstatic.com/icons/aws-service-icon-aurora.8c5c0c5e.svg) | **Aurora** | Banco de dados relacional **compatível com MySQL e PostgreSQL** com performance até 5x superior. Alta disponibilidade e durabilidade. |

---

## Monitoring and Observability

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![CloudWatch](https://d1.awsstatic.com/icons/aws-service-icon-cloudwatch.8c5c0c5e.svg) | **CloudWatch** | Serviço de **monitoramento e observabilidade** que coleta métricas, logs e eventos de recursos AWS e aplicações. |
| ![CloudTrail](https://d1.awsstatic.com/icons/aws-service-icon-cloudtrail.8c5c0c5e.svg) | **CloudTrail** | Serviço que **registra atividade de API** e ações de usuários, roles e serviços AWS. Essencial para auditoria e compliance. |
| ![Config](https://d1.awsstatic.com/icons/aws-service-icon-config.8c5c0c5e.svg) | **Config** | Serviço que **avalia, audita e avalia configurações** de recursos AWS. Rastreia mudanças e verifica conformidade com regras. |
| ![X-Ray](https://d1.awsstatic.com/icons/aws-service-icon-xray.8c5c0c5e.svg) | **X-Ray** | Serviço que ajuda a **analisar e depurar aplicações distribuídas**. Visualiza requisições e identifica gargalos de performance. |

---

## Messaging and Queuing

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![SNS](https://d1.awsstatic.com/icons/aws-service-icon-sns.8c5c0c5e.svg) | **SNS (Simple Notification Service)** | Serviço de **notificações pub/sub gerenciado**. Envia mensagens para múltiplos assinantes via email, SMS, HTTP, Lambda, etc. |
| ![SQS](https://d1.awsstatic.com/icons/aws-service-icon-sqs.8c5c0c5e.svg) | **SQS (Simple Queue Service)** | Serviço de **filas de mensagens gerenciado**. Desacopla componentes de aplicações e permite comunicação assíncrona entre serviços. |
| ![MQ](https://d1.awsstatic.com/icons/aws-service-icon-mq.8c5c0c5e.svg) | **MQ (Amazon MQ)** | Serviço de **message broker gerenciado** para Apache ActiveMQ e RabbitMQ. Migração fácil de message brokers existentes. |

---

## Security and Compliance

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![IAM](https://d1.awsstatic.com/icons/aws-service-icon-iam.8c5c0c5e.svg) | **IAM (Identity and Access Management)** | Serviço para **gerenciar acessos e permissões**. Controla quem pode fazer o quê na conta AWS. |
| ![WAF](https://d1.awsstatic.com/icons/aws-service-icon-waf.8c5c0c5e.svg) | **WAF (Web Application Firewall)** | Serviço que **protege aplicações web** contra vulnerabilidades comuns. Filtra e monitora requisições HTTP/HTTPS. |
| ![Shield](https://d1.awsstatic.com/icons/aws-service-icon-shield.8c5c0c5e.svg) | **Shield** | Serviço de **proteção contra DDoS (Distributed Denial of Service)**. Protege aplicações na AWS contra ataques. |
| ![GuardDuty](https://d1.awsstatic.com/icons/aws-service-icon-guardduty.8c5c0c5e.svg) | **GuardDuty** | Serviço de **detecção de ameaças gerenciado** que monitora continuamente ambientes AWS. Identifica atividades maliciosas. |
| ![Secrets Manager](https://d1.awsstatic.com/icons/aws-service-icon-secrets-manager.8c5c0c5e.svg) | **Secrets Manager** | Serviço para **gerenciar segredos** como senhas, tokens e chaves de API. Rotação automática e integração com serviços AWS. |
| ![KMS](https://d1.awsstatic.com/icons/aws-service-icon-kms.8c5c0c5e.svg) | **KMS (Key Management Service)** | Serviço para **criar e gerenciar chaves de criptografia**. Controla uso de chaves criptográficas em aplicações AWS. |
| ![NACL](https://d1.awsstatic.com/icons/aws-service-icon-nacl.8c5c0c5e.svg) | **NACL (Network Access Control Lists)** | **Firewall opcional** na camada de sub-rede da VPC. Controla tráfego de entrada e saída em nível de rede. |
| ![Security Groups](https://d1.awsstatic.com/icons/aws-service-icon-security-groups.8c5c0c5e.svg) | **Security Groups** | **Firewall virtual** que controla tráfego de entrada e saída para instâncias EC2. Regras de permissão baseadas em porta e protocolo. |

---

## Migration to the Cloud

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![Application Migration Service](https://d1.awsstatic.com/icons/aws-service-icon-application-migration-service.8c5c0c5e.svg) | **Application Migration Service** | Serviço que **automatiza migração de aplicações** de servidores físicos, virtuais ou cloud para AWS. Minimiza tempo de inatividade. |
| ![DMS](https://d1.awsstatic.com/icons/aws-service-icon-dms.8c5c0c5e.svg) | **DMS (Database Migration Service)** | Serviço para **migrar bancos de dados** para AWS de forma segura. Suporta migração homogênea e heterogênea com tempo de inatividade mínimo. |
| ![Snowball](https://d1.awsstatic.com/icons/aws-service-icon-snowball.8c5c0c5e.svg) | **Snowball** | Dispositivo físico para **transferir grandes volumes de dados** para AWS offline. Ideal quando conexão de internet não é suficiente. |
| ![DataSync](https://d1.awsstatic.com/icons/aws-service-icon-datasync.8c5c0c5e.svg) | **DataSync** | Serviço que **acelera transferência de dados** entre on-premises e AWS. Simplifica migração de dados e sincronização contínua. |

---

## Machine Learning and AI

| Ícone | Serviço | Descrição |
|-------|---------|-----------|
| ![Comprehend](https://d1.awsstatic.com/icons/aws-service-icon-comprehend.8c5c0c5e.svg) | **Comprehend** | Serviço de **processamento de linguagem natural (NLP)** que extrai insights de texto. Identifica sentimentos, entidades e tópicos. |
| ![SageMaker](https://d1.awsstatic.com/icons/aws-service-icon-sagemaker.8c5c0c5e.svg) | **SageMaker** | Plataforma **totalmente gerenciada para machine learning**. Permite construir, treinar e implantar modelos de ML rapidamente. |
| ![Lex](https://d1.awsstatic.com/icons/aws-service-icon-lex.8c5c0c5e.svg) | **Lex** | Serviço para **construir interfaces conversacionais** usando voz e texto. Usa tecnologia de deep learning para reconhecimento de fala. |
| ![Rekognition](https://d1.awsstatic.com/icons/aws-service-icon-rekognition.8c5c0c5e.svg) | **Rekognition** | Serviço de **análise de imagens e vídeos** usando deep learning. Detecta objetos, pessoas, texto, cenas e atividades. |

---

## Resumo

Esta visão geral apresenta os principais serviços AWS organizados por categoria em formato de tabela com ícones oficiais. Cada serviço resolve necessidades específicas de computação, armazenamento, rede, segurança, banco de dados, monitoramento e muito mais, permitindo construir arquiteturas completas e escaláveis na nuvem.
