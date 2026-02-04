# Amazon Route 53

O **Route 53** é o serviço de **DNS (Domain Name System)** da AWS.  
Ele permite configurar o redirecionamento de usuários do seu **domínio** para diferentes serviços da AWS, como:

- EC2
- ELB / ALB (Elastic Load Balancer / Application Load Balancer)
- S3
- CloudFront
- Outros serviços AWS

---

## Visão Geral

O Route 53 é um serviço de DNS altamente disponível e escalável que permite:

- Registrar domínios
- Gerenciar registros DNS
- Roteamento inteligente de tráfego
- Integração total com o ecossistema AWS
- Health checks e failover automático

---

## Benefícios do Route 53

- ✅ Serviço altamente disponível e escalável
- ✅ Total integração com o ecossistema AWS
- ✅ Permite controle avançado de roteamento através de **routing policies**
- ✅ Health checks integrados
- ✅ Suporte a múltiplas políticas de roteamento simultâneas
- ✅ Baixa latência global

---

## Routing Policies (Políticas de Roteamento)

As **routing policies** definem como o tráfego será direcionado quando um usuário acessa seu domínio. Cada política atende a diferentes necessidades de roteamento.

---

### 1. Simple Routing (Roteamento Simples)

**Função:** Retorna um único valor para uma consulta DNS.

**Características:**
- Mais básica e direta
- Retorna apenas um registro por consulta
- Não inclui health checks
- Ideal para configurações simples

**Exemplo Prático:**

```
Domínio: exemplo.com
Tipo: A Record
Valor: 192.0.2.1

Usuário acessa: exemplo.com
Route 53 retorna: 192.0.2.1
```

**Cenário de Uso:**
- Site simples com um único servidor
- Aplicação hospedada em um único endpoint
- Configuração inicial de domínio

---

### 2. Weighted Routing (Roteamento por Peso)

**Função:** Distribui tráfego entre múltiplos recursos com base em pesos atribuídos.

**Características:**
- Cada registro tem um peso (0-255)
- O tráfego é distribuído proporcionalmente aos pesos
- Permite testes A/B ou distribuição gradual
- Útil para migrações graduais

**Exemplo Prático:**

```
Domínio: exemplo.com
Registro 1:
  - Valor: servidor1.exemplo.com (192.0.2.1)
  - Peso: 70
  - Tipo: A Record

Registro 2:
  - Valor: servidor2.exemplo.com (192.0.2.2)
  - Peso: 30
  - Tipo: A Record

Distribuição:
- 70% do tráfego → servidor1 (192.0.2.1)
- 30% do tráfego → servidor2 (192.0.2.2)
```

**Cenário de Uso:**
- Teste A/B de novas versões
- Migração gradual de servidores
- Distribuição de carga proporcional
- Teste de performance entre ambientes

**Diagrama:**

```
┌─────────────────┐
│   Usuários      │
└────────┬────────┘
         │
         │ DNS Query: exemplo.com
         ▼
┌─────────────────┐
│   Route 53      │
│  (Weighted)     │
└────────┬────────┘
         │
    ┌────┴────┐
    │         │
70% │         │ 30%
    ▼         ▼
┌────────┐ ┌────────┐
│Server 1│ │Server 2│
│70% tráf.│ │30% tráf.│
└────────┘ └────────┘
```

---

### 3. Latency-based Routing (Roteamento por Latência)

**Função:** Direciona o usuário para a região com **menor latência** baseado na localização do usuário e do recurso.

**Características:**
- Route 53 mede a latência entre usuários e regiões
- Retorna o endpoint com menor latência
- Ideal para aplicações globais
- Melhora a experiência do usuário

**Exemplo Prático:**

```
Domínio: exemplo.com

Registro 1:
  - Valor: us-east-1.elb.amazonaws.com
  - Região: us-east-1 (N. Virginia)
  - Tipo: A Record (Alias)

Registro 2:
  - Valor: eu-west-1.elb.amazonaws.com
  - Região: eu-west-1 (Ireland)
  - Tipo: A Record (Alias)

Registro 3:
  - Valor: ap-southeast-1.elb.amazonaws.com
  - Região: ap-southeast-1 (Singapore)
  - Tipo: A Record (Alias)

Comportamento:
- Usuário no Brasil → us-east-1 (menor latência)
- Usuário na Europa → eu-west-1 (menor latência)
- Usuário na Ásia → ap-southeast-1 (menor latência)
```

**Cenário de Uso:**
- Aplicações globais com múltiplas regiões
- Otimização de performance para usuários internacionais
- Redução de latência percebida
- Aplicações sensíveis a latência (jogos, streaming)

**Diagrama:**

```
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│ Usuário BR   │  │ Usuário EU   │  │ Usuário AS   │
└──────┬───────┘  └──────┬───────┘  └──────┬───────┘
       │                 │                 │
       │ DNS Query       │ DNS Query       │ DNS Query
       ▼                 ▼                 ▼
┌─────────────────────────────────────────────────┐
│           Route 53 (Latency-based)              │
│  Mede latência e retorna endpoint mais próximo  │
└─────────────────────────────────────────────────┘
       │                 │                 │
       ▼                 ▼                 ▼
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│  us-east-1   │  │  eu-west-1   │  │ ap-southeast-1│
│  (N. Virginia)│  │  (Ireland)   │  │  (Singapore)  │
└──────────────┘  └──────────────┘  └──────────────┘
```

---

### 4. Failover Routing (Roteamento por Failover)

**Função:** Utilizada para **alta disponibilidade** com failover automático.

**Características:**
- Define endpoint primário e secundário
- Health checks monitoram o endpoint primário
- Se o primário falhar, tráfego é redirecionado automaticamente
- Suporta failover ativo-passivo ou ativo-ativo

**Exemplo Prático:**

```
Domínio: exemplo.com

Registro Primário:
  - Valor: servidor-primario.exemplo.com (192.0.2.1)
  - Tipo: Failover PRIMARY
  - Health Check: Habilitado
  - Tipo: A Record

Registro Secundário:
  - Valor: servidor-secundario.exemplo.com (192.0.2.2)
  - Tipo: Failover SECONDARY
  - Health Check: Não necessário (herda do primário)
  - Tipo: A Record

Comportamento:
- Normal: Todo tráfego → servidor-primario (192.0.2.1)
- Falha: Health check detecta problema
- Failover: Todo tráfego → servidor-secundario (192.0.2.2)
```

**Cenário de Uso:**
- Alta disponibilidade crítica
- Disaster recovery
- Aplicações que não podem ter downtime
- Backup automático de infraestrutura

**Diagrama:**

```
┌─────────────────┐
│   Usuários      │
└────────┬────────┘
         │
         │ DNS Query: exemplo.com
         ▼
┌─────────────────┐
│   Route 53      │
│  (Failover)     │
│                 │
│  Health Check   │◄──┐
│  ┌──────────┐   │  │ Monitora
│  │ PRIMARY  │───┘  │
│  └──────────┘      │
└────────┬───────────┘
         │
         │ Primário OK?
         ▼
    ┌────┴────┐
    │        │
   SIM      NÃO
    │        │
    ▼        ▼
┌────────┐ ┌────────┐
│Server 1│ │Server 2│
│(Primário)│ │(Secundário)│
└────────┘ └────────┘
```

---

### 5. Geolocation Routing (Roteamento por Localização Geográfica)

**Função:** Direciona o tráfego com base na **localização geográfica** do usuário (país/continente).

**Características:**
- Roteamento baseado em localização do usuário
- Permite conteúdo localizado
- Útil para compliance e regras regionais
- Suporta registro padrão para localizações não mapeadas

**Exemplo Prático:**

```
Domínio: exemplo.com

Registro 1:
  - Valor: servidor-br.exemplo.com (192.0.2.10)
  - Localização: Brazil
  - Tipo: A Record

Registro 2:
  - Valor: servidor-eu.exemplo.com (192.0.2.20)
  - Localização: Europe
  - Tipo: A Record

Registro 3:
  - Valor: servidor-us.exemplo.com (192.0.2.30)
  - Localização: United States
  - Tipo: A Record

Registro 4 (Padrão):
  - Valor: servidor-default.exemplo.com (192.0.2.1)
  - Localização: Default
  - Tipo: A Record

Comportamento:
- Usuário no Brasil → servidor-br (192.0.2.10)
- Usuário na França → servidor-eu (192.0.2.20)
- Usuário nos EUA → servidor-us (192.0.2.30)
- Usuário em outro país → servidor-default (192.0.2.1)
```

**Cenário de Uso:**
- Conteúdo localizado por região
- Compliance com leis regionais (ex: GDPR na Europa)
- Restrições geográficas de conteúdo
- Aplicações com regras de negócio regionais
- Streaming de conteúdo com direitos regionais

**Diagrama:**

```
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│ Usuário BR   │  │ Usuário EU   │  │ Usuário US   │
└──────┬───────┘  └──────┬───────┘  └──────┬───────┘
       │                 │                 │
       │ DNS Query       │ DNS Query       │ DNS Query
       ▼                 ▼                 ▼
┌─────────────────────────────────────────────────┐
│      Route 53 (Geolocation)                     │
│  Identifica localização geográfica do usuário   │
└─────────────────────────────────────────────────┘
       │                 │                 │
       ▼                 ▼                 ▼
┌──────────────┐  ┌──────────────┐  ┌──────────────┐
│ Server BR    │  │ Server EU    │  │ Server US    │
│ (Brasil)     │  │ (Europa)     │  │ (EUA)        │
└──────────────┘  └──────────────┘  └──────────────┘
```

---

### 6. Geoproximity Routing (Roteamento por Proximidade Geográfica)

**Função:** Roteamento baseado na proximidade geográfica com possibilidade de ajuste de "bias" (viés).

**Características:**
- Similar ao Geolocation, mas com bias ajustável
- Permite expandir ou reduzir a área de influência
- Bias positivo: expande a área de roteamento
- Bias negativo: reduz a área de roteamento
- Mais flexível que Geolocation

**Exemplo Prático:**

```
Domínio: exemplo.com

Registro 1:
  - Valor: servidor-sa.exemplo.com (192.0.2.10)
  - Localização: South America
  - Bias: +10 (expande área de influência)
  - Tipo: A Record

Registro 2:
  - Valor: servidor-na.exemplo.com (192.0.2.20)
  - Localização: North America
  - Bias: -5 (reduz área de influência)
  - Tipo: A Record

Comportamento:
- Bias +10: Servidor SA atende usuários em área maior
- Bias -5: Servidor NA atende usuários em área menor
- Permite ajuste fino da distribuição geográfica
```

**Cenário de Uso:**
- Ajuste fino de distribuição geográfica
- Balanceamento de carga baseado em proximidade
- Otimização de custos por região
- Controle granular de roteamento geográfico

**Diferença entre Geolocation e Geoproximity:**

| Característica | Geolocation | Geoproximity |
|----------------|-------------|--------------|
| Base | País/Continente fixo | Proximidade + Bias ajustável |
| Flexibilidade | Baixa | Alta |
| Bias | Não suporta | Suporta (+/-) |
| Uso | Regras fixas | Ajuste dinâmico |

---

### 7. Multivalue Answer Routing (Roteamento Multivalor)

**Função:** Retorna múltiplos valores (até 8) em ordem aleatória, com health checks opcionais.

**Características:**
- Retorna até 8 registros saudáveis aleatoriamente
- Health checks opcionais para cada registro
- Apenas registros saudáveis são retornados
- Distribuição aleatória para balanceamento básico
- Não é um load balancer completo

**Exemplo Prático:**

```
Domínio: exemplo.com

Registro 1:
  - Valor: servidor1.exemplo.com (192.0.2.1)
  - Health Check: Habilitado
  - Tipo: A Record

Registro 2:
  - Valor: servidor2.exemplo.com (192.0.2.2)
  - Health Check: Habilitado
  - Tipo: A Record

Registro 3:
  - Valor: servidor3.exemplo.com (192.0.2.3)
  - Health Check: Habilitado
  - Tipo: A Record

Comportamento:
- Cada consulta DNS retorna até 8 IPs saudáveis
- Ordem aleatória a cada consulta
- Se servidor1 estiver offline, apenas servidor2 e servidor3 são retornados
- Cliente escolhe qual IP usar (balanceamento no cliente)
```

**Cenário de Uso:**
- Balanceamento básico sem Load Balancer
- Alta disponibilidade simples
- Aplicações que fazem múltiplas consultas DNS
- Redução de dependência de um único endpoint

**Diagrama:**

```
┌─────────────────┐
│   Usuário       │
└────────┬────────┘
         │
         │ DNS Query: exemplo.com
         ▼
┌─────────────────┐
│   Route 53      │
│  (Multivalue)   │
│                 │
│  Health Checks  │
│  ┌──────────┐   │
│  │Server 1  │───┼──► OK ✓
│  │Server 2  │───┼──► OK ✓
│  │Server 3  │───┼──► FAIL ✗
│  └──────────┘   │
└────────┬────────┘
         │
         │ Retorna apenas saudáveis
         │ (ordem aleatória)
         ▼
┌─────────────────┐
│ Resposta DNS:   │
│ - 192.0.2.1     │
│ - 192.0.2.2     │
│ (Server 3 não   │
│  incluído)      │
└─────────────────┘
```

---

## Comparação de Routing Policies

| Policy | Casos de Uso | Health Check | Múltiplos Valores | Complexidade |
|--------|--------------|--------------|-------------------|--------------|
| **Simple** | Configuração básica | ❌ | ❌ | Baixa |
| **Weighted** | Teste A/B, migração gradual | Opcional | ✅ | Média |
| **Latency-based** | Aplicações globais | Opcional | ✅ | Média |
| **Failover** | Alta disponibilidade | ✅ | ❌ | Média |
| **Geolocation** | Conteúdo localizado | Opcional | ✅ | Média |
| **Geoproximity** | Roteamento geográfico flexível | Opcional | ✅ | Alta |
| **Multivalue** | Balanceamento simples | Opcional | ✅ | Baixa |

---

## Health Checks

O Route 53 oferece **health checks** para monitorar a saúde dos endpoints:

### Tipos de Health Checks

1. **Endpoint Health Check**
   - Monitora um endpoint específico (IP, hostname)
   - Verifica HTTP, HTTPS, TCP
   - Intervalo configurável (10-30 segundos)

2. **CloudWatch Alarm Health Check**
   - Baseado em métricas do CloudWatch
   - Integração com outros serviços AWS

3. **Calculated Health Check**
   - Combina múltiplos health checks
   - Lógica AND/OR

### Exemplo de Configuração

```
Health Check: servidor-primario
- Protocolo: HTTP
- Porta: 80
- Path: /health
- Intervalo: 30 segundos
- Timeout: 5 segundos
- Threshold: 3 falhas consecutivas
```

---

## Casos de Uso Comuns

### 1. Aplicações Globais com Múltiplas Regiões
- **Policy:** Latency-based Routing
- **Benefício:** Menor latência para usuários globais

### 2. Balanceamento Inteligente de Tráfego
- **Policy:** Weighted Routing
- **Benefício:** Distribuição proporcional e testes A/B

### 3. Estratégias de Alta Disponibilidade
- **Policy:** Failover Routing
- **Benefício:** Failover automático em caso de falha

### 4. Conteúdo Localizado e Compliance
- **Policy:** Geolocation Routing
- **Benefício:** Conteúdo específico por região

### 5. Integração Direta com Infraestrutura AWS
- **Alias Records** para ELB, CloudFront, S3
- **Benefício:** Sem custo adicional de consultas DNS

---

## Alias Records

**Alias Records** são uma funcionalidade especial do Route 53:

### Características

- ✅ Gratuito (sem custo de consultas)
- ✅ Integração nativa com serviços AWS
- ✅ Health checks automáticos
- ✅ Atualização automática quando o recurso muda

### Serviços Suportados

- **ELB / ALB / NLB** (Elastic Load Balancers)
- **CloudFront** (CDN)
- **S3** (Static Website Hosting)
- **API Gateway**
- **Elastic Beanstalk**
- **VPC Endpoints**

### Exemplo

```
Domínio: exemplo.com
Tipo: A Record (Alias)
Alias Target: dualstack.meu-alb-123456.us-east-1.elb.amazonaws.com
```

---

## Resumo Mental

- **Amazon Route 53**
  - Serviço de DNS da AWS
  - **Routing Policies:**
    - Simple (básico)
    - Weighted (peso)
    - Latency-based (latência)
    - Failover (alta disponibilidade)
    - Geolocation (localização)
    - Geoproximity (proximidade + bias)
    - Multivalue (múltiplos valores)
  - **Health Checks** (monitoramento)
  - **Alias Records** (integração AWS)
  - Casos de uso globais e alta disponibilidade
