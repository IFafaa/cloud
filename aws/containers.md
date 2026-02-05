# Containers na AWS - ECS e EKS

A AWS oferece serviços gerenciados para executar aplicações em **containers**, permitindo deploy, gerenciamento e escalabilidade de aplicações containerizadas de forma eficiente.

---

## Visão Geral

Containers permitem empacotar aplicações com todas as suas dependências, garantindo que funcionem de forma consistente em qualquer ambiente.

### Principais Serviços de Containers na AWS

- **Amazon ECS (Elastic Container Service)** - Serviço gerenciado nativo da AWS
- **Amazon EKS (Elastic Kubernetes Service)** - Kubernetes gerenciado pela AWS
- **AWS Fargate** - Computação serverless para containers
- **Amazon ECR (Elastic Container Registry)** - Registro de imagens Docker

---

## Conceitos Fundamentais

### Container

- **Definição:** Unidade de software que empacota código, dependências e configurações
- **Benefícios:**
  - Consistência entre ambientes (dev, staging, prod)
  - Isolamento de aplicações
  - Portabilidade
  - Escalabilidade rápida

### Container Image

- **Definição:** Template imutável usado para criar containers
- **Formato comum:** Docker Image
- **Armazenamento:** Amazon ECR ou Docker Hub

### Container Registry

- **Função:** Armazena e gerencia imagens de containers
- **AWS:** Amazon ECR (Elastic Container Registry)
- **Alternativas:** Docker Hub, GitHub Container Registry

---

## Amazon ECS (Elastic Container Service)

O **Amazon ECS** é um serviço de orquestração de containers totalmente gerenciado pela AWS, projetado para facilitar a execução de aplicações containerizadas na nuvem AWS.

---

### Arquitetura do ECS

```
┌─────────────────────────────────────────────────────────────┐
│                    ECS Cluster                              │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐  │
│  │              Task Definition                          │  │
│  │  - Imagem do container                                │  │
│  │  - CPU/Memória                                        │  │
│  │  - Portas                                             │  │
│  │  - Variáveis de ambiente                             │  │
│  └──────────────────────────────────────────────────────┘  │
│                        │                                     │
│                        ▼                                     │
│  ┌──────────────────────────────────────────────────────┐  │
│  │                    ECS Service                        │  │
│  │  - Número de tasks (replicas)                         │  │
│  │  - Load Balancer                                      │  │
│  │  - Auto Scaling                                       │  │
│  └──────────────────────────────────────────────────────┘  │
│                        │                                     │
│                        ▼                                     │
│  ┌──────────────────────────────────────────────────────┐  │
│  │              Launch Type                               │  │
│  │  ┌──────────────┐          ┌──────────────┐          │  │
│  │  │   Fargate    │          │     EC2      │          │  │
│  │  │ (Serverless) │          │  (Gerenciado)│          │  │
│  │  └──────────────┘          └──────────────┘          │  │
│  └──────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

---

### Componentes do ECS

#### 1. Cluster

- **Função:** Agrupamento lógico de recursos de computação
- **Tipos:**
  - **Fargate Cluster:** Sem servidores para gerenciar
  - **EC2 Cluster:** Usa instâncias EC2 gerenciadas

**Exemplo:**
```
Cluster: meu-cluster-producao
- Região: us-east-1
- Launch Type: Fargate
- Tasks: 10 tasks rodando
```

#### 2. Task Definition

- **Função:** Template que descreve como executar um container
- **Contém:**
  - Imagem do container (ECR ou Docker Hub)
  - CPU e memória necessários
  - Portas a expor
  - Variáveis de ambiente
  - Logging configuration
  - IAM roles

**Exemplo de Task Definition:**

```json
{
  "family": "minha-app",
  "containerDefinitions": [
    {
      "name": "app-container",
      "image": "123456789.dkr.ecr.us-east-1.amazonaws.com/minha-app:latest",
      "cpu": 512,
      "memory": 1024,
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp"
        }
      ],
      "environment": [
        {
          "name": "ENV",
          "value": "production"
        }
      ]
    }
  ]
}
```

#### 3. Task

- **Função:** Instância de um container em execução
- **Criada a partir de:** Task Definition
- **Pode conter:** Um ou múltiplos containers (task com múltiplos containers)

**Exemplo:**
```
Task ID: abc123def456
Status: RUNNING
Task Definition: minha-app:10
Container: app-container (RUNNING)
CPU: 512 (0.5 vCPU)
Memory: 1024 MB
```

#### 4. Service

- **Função:** Mantém um número especificado de tasks em execução
- **Características:**
  - Auto-scaling baseado em métricas
  - Integração com Load Balancer
  - Health checks
  - Rolling updates (deploy sem downtime)

**Exemplo:**
```
Service: minha-app-service
Desired Count: 5 tasks
Running Count: 5 tasks
Load Balancer: meu-alb-123456
Auto Scaling: Habilitado (2-10 tasks)
```

---

### Launch Types do ECS

#### Fargate (Serverless)

**Características:**
- ✅ Sem servidores para gerenciar
- ✅ Pague apenas pelo que usar
- ✅ Escalabilidade automática
- ✅ Isolamento por task
- ✅ Integração nativa com outros serviços AWS

**Quando usar:**
- Aplicações que precisam de isolamento
- Workloads variáveis
- Equipes pequenas (sem necessidade de gerenciar infraestrutura)
- Aplicações que não precisam de controle fino sobre o SO

**Custo:**
- Baseado em CPU e memória alocadas
- Exemplo: 0.25 vCPU + 0.5 GB RAM = ~$0.04/hora

#### EC2 (Gerenciado)

**Características:**
- ✅ Controle total sobre instâncias EC2
- ✅ Múltiplas tasks por instância (mais econômico)
- ✅ Acesso SSH às instâncias
- ✅ Customização do SO e configurações

**Quando usar:**
- Aplicações que precisam de controle fino
- Workloads que precisam de otimização de custo (múltiplas tasks por instância)
- Aplicações que precisam de recursos específicos (GPU, etc.)
- Migração de aplicações existentes em EC2

**Custo:**
- Baseado no custo das instâncias EC2
- Mais econômico para workloads estáveis

**Comparação:**

| Característica | Fargate | EC2 |
|----------------|---------|-----|
| Gerenciamento de servidores | ❌ Não necessário | ✅ Você gerencia |
| Isolamento | Por task | Por instância |
| Múltiplas tasks por host | ❌ Não | ✅ Sim |
| Controle sobre SO | ❌ Limitado | ✅ Total |
| Custo para workloads pequenos | Mais caro | Mais barato |
| Custo para workloads grandes | Mais barato | Mais caro |
| Escalabilidade | Automática | Configurável |

---

### Exemplo Prático: Deploy de Aplicação no ECS

#### Cenário: Aplicação Web Node.js

**Passo 1: Criar Imagem e Publicar no ECR**

```bash
# Build da imagem
docker build -t minha-app .

# Tag para ECR
docker tag minha-app:latest 123456789.dkr.ecr.us-east-1.amazonaws.com/minha-app:latest

# Push para ECR
docker push 123456789.dkr.ecr.us-east-1.amazonaws.com/minha-app:latest
```

**Passo 2: Criar Task Definition**

```
Task Definition: minha-app
- Image: 123456789.dkr.ecr.us-east-1.amazonaws.com/minha-app:latest
- CPU: 512 (0.5 vCPU)
- Memory: 1024 MB
- Port: 3000
- Environment Variables:
  - NODE_ENV=production
  - DATABASE_URL=...
```

**Passo 3: Criar Service**

```
Service: minha-app-service
- Cluster: meu-cluster
- Task Definition: minha-app
- Launch Type: Fargate
- Desired Count: 3
- Load Balancer: meu-alb
- Auto Scaling: 2-10 tasks
```

**Passo 4: Configurar Load Balancer**

```
Application Load Balancer: meu-alb
- Target Group: minha-app-tg
- Health Check: /health
- Listener: Port 80 → HTTPS redirect
- Listener: Port 443 → Target Group
```

**Resultado:**

```
┌─────────────────────────────────────────────────────────┐
│                    INTERNET                             │
└───────────────────────┬─────────────────────────────────┘
                        │
                        ▼
┌─────────────────────────────────────────────────────────┐
│              Application Load Balancer                   │
└───────────────────────┬─────────────────────────────────┘
                        │
        ┌───────────────┼───────────────┐
        │               │               │
        ▼               ▼               ▼
┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│  ECS Task 1  │ │  ECS Task 2  │ │  ECS Task 3  │
│  (Fargate)   │ │  (Fargate)   │ │  (Fargate)   │
│  Container   │ │  Container   │ │  Container   │
└──────────────┘ └──────────────┘ └──────────────┘
```

---

### Auto Scaling no ECS

O ECS suporta auto-scaling baseado em métricas:

**Métricas comuns:**
- CPU Utilization
- Memory Utilization
- Request Count (via ALB)
- Custom CloudWatch Metrics

**Exemplo de Configuração:**

```
Service: minha-app-service
Auto Scaling Policy:
  - Target: CPU 70%
  - Min Tasks: 2
  - Max Tasks: 10
  - Scale Out: +2 tasks quando CPU > 70%
  - Scale In: -1 task quando CPU < 30%
```

---

### Integrações do ECS

#### Amazon ECR (Elastic Container Registry)
- Armazenamento de imagens Docker
- Integração nativa com ECS
- Scanning de vulnerabilidades
- Lifecycle policies

#### Application Load Balancer (ALB)
- Distribuição de tráfego entre tasks
- Health checks
- SSL/TLS termination
- Path-based routing

#### CloudWatch
- Logs de containers
- Métricas de performance
- Alarmes e notificações

#### IAM
- Roles para tasks
- Permissões granulares
- Integração com outros serviços AWS

---

## Amazon EKS (Elastic Kubernetes Service)

O **Amazon EKS** é um serviço gerenciado que facilita a execução de Kubernetes na AWS sem precisar instalar e operar o plano de controle do Kubernetes.

---

### O que é Kubernetes?

**Kubernetes (K8s)** é uma plataforma open-source para orquestração de containers que automatiza:
- Deploy de aplicações
- Escalabilidade
- Gerenciamento de containers
- Service discovery
- Load balancing
- Self-healing

---

### Arquitetura do EKS

```
┌─────────────────────────────────────────────────────────────┐
│                    EKS Cluster                              │
│                                                              │
│  ┌──────────────────────────────────────────────────────┐  │
│  │           Control Plane (Gerenciado pela AWS)        │  │
│  │  - API Server                                         │  │
│  │  - etcd                                               │  │
│  │  - Scheduler                                          │  │
│  │  - Controller Manager                                 │  │
│  └──────────────────────────────────────────────────────┘  │
│                        │                                     │
│                        ▼                                     │
│  ┌──────────────────────────────────────────────────────┐  │
│  │              Worker Nodes (EC2 ou Fargate)            │  │
│  │                                                         │  │
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐ │  │
│  │  │  Node 1      │  │  Node 2      │  │  Node 3      │ │  │
│  │  │  ┌────────┐  │  │  ┌────────┐  │  │  ┌────────┐  │ │  │
│  │  │  │ Pod 1   │  │  │  │ Pod 2   │  │  │  │ Pod 3   │ │  │
│  │  │  │ Pod 2   │  │  │  │ Pod 4   │  │  │  │ Pod 5   │ │  │
│  │  │  └────────┘  │  │  └────────┘  │  │  └────────┘  │ │  │
│  │  └──────────────┘  └──────────────┘  └──────────────┘ │  │
│  └──────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

---

### Componentes do Kubernetes/EKS

#### 1. Cluster

- **Função:** Conjunto de nodes (máquinas) que executam containers
- **Componentes:**
  - **Control Plane:** Gerenciado pela AWS (alta disponibilidade)
  - **Worker Nodes:** EC2 instances ou Fargate

#### 2. Node (Nó)

- **Função:** Máquina (física ou virtual) que executa containers
- **Tipos:**
  - **Master Node:** Control Plane (gerenciado pela AWS)
  - **Worker Node:** Executa os pods (você gerencia ou usa Fargate)

#### 3. Pod

- **Função:** Menor unidade deployável no Kubernetes
- **Pode conter:** Um ou múltiplos containers
- **Características:**
  - Compartilham recursos de rede e armazenamento
  - Sempre executam na mesma máquina

**Exemplo:**
```
Pod: minha-app-pod-abc123
- Container 1: app-container (Node.js)
- Container 2: sidecar-container (logger)
- Status: Running
- Node: worker-node-1
```

#### 4. Deployment

- **Função:** Gerencia réplicas de pods
- **Características:**
  - Rolling updates
  - Rollback automático
  - Auto-scaling
  - Health checks

**Exemplo:**
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: minha-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: minha-app
  template:
    metadata:
      labels:
        app: minha-app
    spec:
      containers:
      - name: app-container
        image: minha-app:latest
        ports:
        - containerPort: 3000
```

#### 5. Service

- **Função:** Expõe pods como um serviço de rede
- **Tipos:**
  - **ClusterIP:** Acesso interno ao cluster
  - **NodePort:** Expõe via porta do node
  - **LoadBalancer:** Cria um Load Balancer externo (ALB/NLB)
  - **ExternalName:** Mapeia para um DNS externo

**Exemplo:**
```yaml
apiVersion: v1
kind: Service
metadata:
  name: minha-app-service
spec:
  type: LoadBalancer
  selector:
    app: minha-app
  ports:
  - port: 80
    targetPort: 3000
```

#### 6. Namespace

- **Função:** Isolamento lógico dentro do cluster
- **Uso comum:**
  - Separar ambientes (dev, staging, prod)
  - Organizar recursos por equipe/projeto

**Exemplo:**
```
Namespace: production
- Deployment: minha-app
- Service: minha-app-service
- ConfigMap: minha-app-config

Namespace: development
- Deployment: minha-app-dev
- Service: minha-app-dev-service
```

---

### Launch Types do EKS

#### Managed Node Groups (EC2)

**Características:**
- ✅ Instâncias EC2 gerenciadas pela AWS
- ✅ Auto-scaling de nodes
- ✅ Atualizações automáticas
- ✅ Integração com EC2 Auto Scaling Groups

**Quando usar:**
- Controle sobre instâncias EC2
- Otimização de custos (múltiplos pods por node)
- Aplicações que precisam de recursos específicos

#### Fargate

**Características:**
- ✅ Serverless (sem gerenciar nodes)
- ✅ Isolamento por pod
- ✅ Pague apenas pelo que usar
- ✅ Escalabilidade automática

**Quando usar:**
- Aplicações que precisam de isolamento
- Workloads variáveis
- Equipes que não querem gerenciar infraestrutura

**Limitações do Fargate no EKS:**
- Não suporta DaemonSets
- Não suporta alguns recursos avançados do Kubernetes
- Custo pode ser maior para workloads estáveis

---

### Exemplo Prático: Deploy no EKS

#### Cenário: Aplicação Web com 3 réplicas

**Passo 1: Criar EKS Cluster**

```bash
eksctl create cluster \
  --name meu-cluster \
  --region us-east-1 \
  --nodegroup-name worker-nodes \
  --node-type t3.medium \
  --nodes 3 \
  --nodes-min 2 \
  --nodes-max 5
```

**Passo 2: Criar Deployment**

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: minha-app
  namespace: production
spec:
  replicas: 3
  selector:
    matchLabels:
      app: minha-app
  template:
    metadata:
      labels:
        app: minha-app
    spec:
      containers:
      - name: app-container
        image: 123456789.dkr.ecr.us-east-1.amazonaws.com/minha-app:latest
        ports:
        - containerPort: 3000
        env:
        - name: NODE_ENV
          value: "production"
        resources:
          requests:
            cpu: 250m
            memory: 512Mi
          limits:
            cpu: 500m
            memory: 1024Mi
```

**Passo 3: Criar Service (LoadBalancer)**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: minha-app-service
  namespace: production
spec:
  type: LoadBalancer
  selector:
    app: minha-app
  ports:
  - port: 80
    targetPort: 3000
    protocol: TCP
```

**Passo 4: Aplicar Configurações**

```bash
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
```

**Resultado:**

```
┌─────────────────────────────────────────────────────────┐
│                    INTERNET                             │
└───────────────────────┬─────────────────────────────────┘
                        │
                        ▼
┌─────────────────────────────────────────────────────────┐
│              Load Balancer (ALB/NLB)                     │
└───────────────────────┬─────────────────────────────────┘
                        │
        ┌───────────────┼───────────────┐
        │               │               │
        ▼               ▼               ▼
┌──────────────┐ ┌──────────────┐ ┌──────────────┐
│  Worker Node │ │  Worker Node │ │  Worker Node │
│  ┌────────┐ │ │  ┌────────┐ │ │  ┌────────┐ │
│  │ Pod 1   │ │ │  │ Pod 2   │ │ │  │ Pod 3   │ │
│  └────────┘ │ │  └────────┘ │ │  └────────┘ │
└──────────────┘ └──────────────┘ └──────────────┘
```

---

### Auto Scaling no EKS

#### Horizontal Pod Autoscaler (HPA)

Escala pods baseado em métricas:

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: minha-app-hpa
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: minha-app
  minReplicas: 2
  maxReplicas: 10
  metrics:
  - type: Resource
    resource:
      name: cpu
      target:
        type: Utilization
        averageUtilization: 70
```

#### Cluster Autoscaler

Escala nodes do cluster:

```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: cluster-autoscaler
spec:
  # Configuração para escalar nodes
```

---

### Integrações do EKS

#### AWS Load Balancer Controller
- Cria ALB/NLB automaticamente
- Integração nativa com Services do tipo LoadBalancer
- Suporte a ingress

#### Amazon ECR
- Armazenamento de imagens
- Integração com Kubernetes
- Scanning de vulnerabilidades

#### CloudWatch
- Logs de containers (via Fluent Bit)
- Métricas de cluster e pods
- Alarmes e dashboards

#### IAM Roles for Service Accounts (IRSA)
- Permissões granulares por pod
- Integração com outros serviços AWS
- Segurança aprimorada

---

## Comparação: ECS vs EKS

| Característica | ECS | EKS |
|----------------|-----|-----|
| **Orquestrador** | Proprietário AWS | Kubernetes (open-source) |
| **Curva de Aprendizado** | Mais simples | Mais complexo |
| **Flexibilidade** | Boa | Excelente |
| **Ecossistema** | AWS nativo | Kubernetes (portável) |
| **Gerenciamento** | Totalmente gerenciado | Control plane gerenciado |
| **Custo** | Mais barato | Mais caro (control plane) |
| **Portabilidade** | AWS apenas | Multi-cloud possível |
| **Comunidade** | AWS | Kubernetes (grande) |
| **Fargate** | ✅ Suportado | ✅ Suportado |
| **EC2** | ✅ Suportado | ✅ Suportado |
| **Auto Scaling** | ✅ Nativo | ✅ HPA + Cluster Autoscaler |
| **Service Discovery** | ✅ Nativo | ✅ Nativo (Kubernetes) |
| **Load Balancing** | ✅ ALB/NLB | ✅ ALB/NLB via controller |

---

## Quando Usar ECS

### Vantagens do ECS

- ✅ **Simplicidade:** Mais fácil de aprender e usar
- ✅ **Integração AWS:** Integração profunda com serviços AWS
- ✅ **Custo:** Mais econômico (sem custo do control plane)
- ✅ **Gerenciamento:** Totalmente gerenciado pela AWS
- ✅ **Fargate:** Serverless nativo e maduro

### Casos de Uso Ideais

- Aplicações que ficarão apenas na AWS
- Equipes que preferem simplicidade
- Aplicações que não precisam de recursos avançados do Kubernetes
- Startups e projetos novos
- Migração de aplicações EC2 para containers

---

## Quando Usar EKS

### Vantagens do EKS

- ✅ **Portabilidade:** Pode rodar em qualquer lugar (multi-cloud)
- ✅ **Ecossistema:** Grande ecossistema de ferramentas Kubernetes
- ✅ **Flexibilidade:** Recursos avançados do Kubernetes
- ✅ **Padrão da Indústria:** Kubernetes é padrão da indústria
- ✅ **Comunidade:** Grande comunidade e recursos

### Casos de Uso Ideais

- Aplicações que precisam de portabilidade (multi-cloud)
- Equipes com experiência em Kubernetes
- Aplicações complexas com muitos microserviços
- Organizações que já usam Kubernetes
- Necessidade de recursos avançados (operators, CRDs, etc.)

---

## Amazon ECR (Elastic Container Registry)

O **Amazon ECR** é o serviço de registro de containers da AWS, usado para armazenar e gerenciar imagens Docker.

### Características

- ✅ Integração nativa com ECS e EKS
- ✅ Scanning de vulnerabilidades
- ✅ Lifecycle policies (limpeza automática)
- ✅ Criptografia em repouso e em trânsito
- ✅ IAM para controle de acesso

### Exemplo de Uso

```bash
# Login no ECR
aws ecr get-login-password --region us-east-1 | \
  docker login --username AWS --password-stdin \
  123456789.dkr.ecr.us-east-1.amazonaws.com

# Build da imagem
docker build -t minha-app .

# Tag para ECR
docker tag minha-app:latest \
  123456789.dkr.ecr.us-east-1.amazonaws.com/minha-app:latest

# Push para ECR
docker push \
  123456789.dkr.ecr.us-east-1.amazonaws.com/minha-app:latest
```

---

## Casos de Uso Comuns

### 1. Aplicações Web Microserviços

**Cenário:** Aplicação com múltiplos serviços

**Solução:**
- ECS ou EKS para orquestração
- ALB para roteamento
- ECR para imagens
- Auto-scaling por serviço

### 2. CI/CD com Containers

**Cenário:** Pipeline de deploy automatizado

**Solução:**
- CodeBuild para build de imagens
- ECR para armazenamento
- ECS/EKS para deploy
- CodePipeline para orquestração

### 3. Aplicações Serverless com Containers

**Cenário:** Aplicações que precisam de isolamento mas não querem gerenciar servidores

**Solução:**
- ECS Fargate ou EKS Fargate
- Sem gerenciamento de infraestrutura
- Escalabilidade automática

### 4. Migração de Aplicações Legacy

**Cenário:** Aplicações monolíticas em servidores tradicionais

**Solução:**
- Containerizar aplicação
- Deploy no ECS/EKS
- Migração gradual
- Melhor escalabilidade

---

## Resumo Mental

- **Containers na AWS**
  - **Amazon ECS:**
    - Orquestrador nativo AWS
    - Componentes: Cluster, Task Definition, Task, Service
    - Launch Types: Fargate (serverless) e EC2
    - Simples e integrado com AWS
  - **Amazon EKS:**
    - Kubernetes gerenciado
    - Componentes: Cluster, Node, Pod, Deployment, Service
    - Launch Types: Managed Node Groups e Fargate
    - Portável e flexível
  - **Amazon ECR:**
    - Registro de imagens Docker
    - Integração com ECS/EKS
    - Scanning de vulnerabilidades
  - **Comparação:**
    - ECS: Mais simples, AWS nativo, mais barato
    - EKS: Mais flexível, portável, padrão da indústria
  - **Casos de Uso:**
    - Microserviços
    - CI/CD
    - Serverless containers
    - Migração de aplicações
