# AWS Services - Visão Geral

Este documento apresenta um **resumo geral dos principais serviços da AWS**, organizados por categoria e função.

---

## Cloud Computing Essentials

### Simple Storage Service (S3)
Serviço de **armazenamento de objetos** altamente escalável, durável e disponível. Ideal para armazenar imagens, vídeos, backups, logs e arquivos estáticos.

### Elastic Compute Cloud (EC2)
Serviço de **computação na nuvem** que fornece capacidade de servidores virtuais redimensionáveis. Permite executar aplicações na nuvem com controle total sobre o ambiente.

---

## Cloud First Steps

### Management Console
Interface web para **gerenciar e monitorar** todos os serviços AWS de forma centralizada. Ponto de entrada principal para acessar recursos da AWS.

### IAM (Identity and Access Management)
Serviço para **gerenciar identidades, acessos e permissões** dentro de uma conta AWS. Controla quem pode acessar quais recursos e serviços.

### CloudWatch
Serviço de **monitoramento e observabilidade** que coleta métricas, logs e eventos. Permite monitorar aplicações, responder a mudanças e otimizar recursos.

---

## Computing Solutions

### Elastic Compute Cloud (EC2)
Serviço de **computação virtual** com servidores na nuvem. Permite escolher tipo de instância, sistema operacional e configurações de rede.

### Lambda
Serviço de **computação serverless** que executa código sob demanda sem gerenciar servidores. Paga apenas pelo tempo de execução.

### Fargate
Serviço de **computação serverless para containers**. Permite executar containers sem gerenciar servidores ou clusters.

### ECS (Elastic Container Service)
Serviço **gerenciado de orquestração de containers** que suporta Docker. Facilita execução, escalonamento e gerenciamento de aplicações containerizadas.

---

## Cloud Economics

### Cost Explorer
Ferramenta para **visualizar e analisar custos** da AWS ao longo do tempo. Permite identificar tendências e oportunidades de economia.

### Budgets
Serviço para **definir orçamentos** e receber alertas quando custos excedem limites definidos. Ajuda a controlar gastos na nuvem.

### Cost & Usage Report
Relatório detalhado de **custos e uso** de serviços AWS. Fornece dados granulares para análise financeira e otimização.

---

## Networking Concepts

### Virtual Private Cloud (VPC)
Serviço que permite criar uma **rede virtual isolada e privada** na nuvem AWS. Controle total sobre configuração de rede, IPs e gateways.

### Route 53
Serviço de **DNS (Domain Name System)** gerenciado e altamente disponível. Roteia tráfego para aplicações e fornece registro de domínios.

### API Gateway
Serviço para **criar, publicar e gerenciar APIs REST e WebSocket**. Atua como ponto de entrada para aplicações backend.

---

## Connecting VPCs

### VPC Peering
Conexão de rede que permite **conectar duas VPCs** para comunicação privada usando IPv4 ou IPv6. Tráfego permanece na rede AWS.

### Transit Gateway
Serviço de **rede centralizada** que conecta VPCs, VPNs e conexões Direct Connect. Simplifica arquitetura de rede e reduz complexidade.

### Direct Connect
Serviço que estabelece uma **conexão de rede dedicada** entre datacenter on-premises e AWS. Fornece largura de banda consistente e baixa latência.

### VPN Connection
Conexão **VPN segura** entre rede on-premises e VPC na AWS. Permite acesso seguro a recursos na nuvem através de túnel criptografado.

---

## First NoSQL Database

### DynamoDB
Banco de dados **NoSQL gerenciado** rápido e flexível. Oferece performance de milissegundos em qualquer escala, com backup automático e criptografia.

---

## Storage and File Systems

### Simple Storage Service (S3)
Serviço de **armazenamento de objetos** com diferentes classes de armazenamento para otimizar custos e performance.

### EBS (Elastic Block Store)
Serviço de **armazenamento em blocos** de alta performance para instâncias EC2. Volumes persistentes e duráveis para cargas de trabalho.

### EFS (Elastic File System)
Sistema de **arquivos gerenciado** e escalável para EC2. Suporta acesso simultâneo de múltiplas instâncias com consistência forte.

### FSx
Serviço de **sistemas de arquivos gerenciados** de terceira geração. Inclui FSx for Windows File Server e FSx for Lustre para workloads específicos.

---

## Auto-healing and Scaling Applications

### EC2 Auto Scaling
Serviço que **ajusta automaticamente a capacidade** de instâncias EC2. Garante disponibilidade e escala baseado em demanda.

### ELB (Elastic Load Balancer)
Serviço que **distribui tráfego** entre múltiplas instâncias ou containers. Melhora disponibilidade e tolerância a falhas.

### CloudFront
Rede de **distribuição de conteúdo (CDN)** global. Entrega conteúdo estático e dinâmico com baixa latência e alta velocidade de transferência.

---

## Serverless Architectures

### Simple Storage Service (S3)
Armazenamento serverless que **não requer provisionamento** de servidores. Escala automaticamente.

### Lambda
Execução de código **serverless** que escala automaticamente. Executa funções em resposta a eventos.

### API Gateway
API **serverless** que escala automaticamente. Gerencia tráfego, autenticação e autorização.

### Step Functions
Orquestração de **workflows serverless**. Coordena múltiplos serviços AWS em processos visuais.

---

## DevOps and Continuous Delivery

### Code Commit
Serviço de **controle de versão gerenciado** baseado em Git. Repositórios privados e seguros para código.

### Code Build
Serviço de **compilação gerenciada** que compila código-fonte, executa testes e produz artefatos prontos para deploy.

### Code Deploy
Serviço que **automatiza deployments** para instâncias EC2, Lambda, ECS e serviços on-premises. Reduz tempo de inatividade.

### Code Pipeline
Serviço de **CI/CD totalmente gerenciado** que automatiza pipelines de release. Integra Code Commit, Code Build e Code Deploy.

---

## Relational Database Solutions

### RDS (Relational Database Service)
Serviço de **banco de dados relacional gerenciado**. Suporta MySQL, PostgreSQL, MariaDB, Oracle e SQL Server com backups automáticos.

### Aurora
Banco de dados relacional **compatível com MySQL e PostgreSQL** com performance até 5x superior. Alta disponibilidade e durabilidade.

---

## Monitoring and Observability

### CloudWatch
Serviço de **monitoramento e observabilidade** que coleta métricas, logs e eventos de recursos AWS e aplicações.

### CloudTrail
Serviço que **registra atividade de API** e ações de usuários, roles e serviços AWS. Essencial para auditoria e compliance.

### Config
Serviço que **avalia, audita e avalia configurações** de recursos AWS. Rastreia mudanças e verifica conformidade com regras.

### X-Ray
Serviço que ajuda a **analisar e depurar aplicações distribuídas**. Visualiza requisições e identifica gargalos de performance.

---

## Messaging and Queuing

### SNS (Simple Notification Service)
Serviço de **notificações pub/sub gerenciado**. Envia mensagens para múltiplos assinantes via email, SMS, HTTP, Lambda, etc.

### SQS (Simple Queue Service)
Serviço de **filas de mensagens gerenciado**. Desacopla componentes de aplicações e permite comunicação assíncrona entre serviços.

### MQ (Amazon MQ)
Serviço de **message broker gerenciado** para Apache ActiveMQ e RabbitMQ. Migração fácil de message brokers existentes.

---

## Security and Compliance

### IAM (Identity and Access Management)
Serviço para **gerenciar acessos e permissões**. Controla quem pode fazer o quê na conta AWS.

### WAF (Web Application Firewall)
Serviço que **protege aplicações web** contra vulnerabilidades comuns. Filtra e monitora requisições HTTP/HTTPS.

### Shield
Serviço de **proteção contra DDoS (Distributed Denial of Service)**. Protege aplicações na AWS contra ataques.

### GuardDuty
Serviço de **detecção de ameaças gerenciado** que monitora continuamente ambientes AWS. Identifica atividades maliciosas.

### Secrets Manager
Serviço para **gerenciar segredos** como senhas, tokens e chaves de API. Rotação automática e integração com serviços AWS.

### KMS (Key Management Service)
Serviço para **criar e gerenciar chaves de criptografia**. Controla uso de chaves criptográficas em aplicações AWS.

### NACL (Network Access Control Lists)
**Firewall opcional** na camada de sub-rede da VPC. Controla tráfego de entrada e saída em nível de rede.

### Security Groups
**Firewall virtual** que controla tráfego de entrada e saída para instâncias EC2. Regras de permissão baseadas em porta e protocolo.

---

## Migration to the Cloud

### Application Migration Service
Serviço que **automatiza migração de aplicações** de servidores físicos, virtuais ou cloud para AWS. Minimiza tempo de inatividade.

### DMS (Database Migration Service)
Serviço para **migrar bancos de dados** para AWS de forma segura. Suporta migração homogênea e heterogênea com tempo de inatividade mínimo.

### Snowball
Dispositivo físico para **transferir grandes volumes de dados** para AWS offline. Ideal quando conexão de internet não é suficiente.

### DataSync
Serviço que **acelera transferência de dados** entre on-premises e AWS. Simplifica migração de dados e sincronização contínua.

---

## Machine Learning and AI

### Comprehend
Serviço de **processamento de linguagem natural (NLP)** que extrai insights de texto. Identifica sentimentos, entidades e tópicos.

### SageMaker
Plataforma **totalmente gerenciada para machine learning**. Permite construir, treinar e implantar modelos de ML rapidamente.

### Lex
Serviço para **construir interfaces conversacionais** usando voz e texto. Usa tecnologia de deep learning para reconhecimento de fala.

### Rekognition
Serviço de **análise de imagens e vídeos** usando deep learning. Detecta objetos, pessoas, texto, cenas e atividades.

---

## Resumo

Esta visão geral apresenta os principais serviços AWS organizados por categoria. Cada serviço resolve necessidades específicas de computação, armazenamento, rede, segurança, banco de dados, monitoramento e muito mais, permitindo construir arquiteturas completas e escaláveis na nuvem.
