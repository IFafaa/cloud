# Amazon CloudFront

O **Amazon CloudFront** é um serviço de **CDN (Content Delivery Network)** rápido e altamente seguro oferecido pela Amazon Web Services (AWS). Ele distribui dados, vídeos, aplicativos e APIs para os usuários com baixa latência e altas velocidades de transferência.

---

## Visão Geral

O CloudFront é uma rede global de entrega de conteúdo que:

- Acelera a entrega de conteúdo estático e dinâmico
- Reduz a latência através de uma rede global de Edge Locations
- Protege aplicações com integração de segurança AWS
- Escala automaticamente para lidar com picos de tráfego
- Integra-se profundamente com outros serviços AWS

---

## Como Funciona o CloudFront

### Arquitetura Básica

```
┌─────────────────────────────────────────────────────────────┐
│                    USUÁRIO FINAL                             │
│                  (Brasil, Europa, etc.)                      │
└───────────────────────┬───────────────────────────────────────┘
                        │
                        │ Requisição HTTP/HTTPS
                        ▼
┌─────────────────────────────────────────────────────────────┐
│              EDGE LOCATION (Mais Próxima)                   │
│              ┌──────────────────────────┐                 │
│              │  Cache do CloudFront       │                 │
│              │  - Verifica se tem cache    │                 │
│              │  - Se SIM: retorna imediato│                 │
│              │  - Se NÃO: busca no Origin │                 │
│              └──────────────────────────┘                 │
└───────────────────────┬───────────────────────────────────────┘
                        │
                        │ (se não estiver em cache)
                        ▼
┌─────────────────────────────────────────────────────────────┐
│                    ORIGIN                                    │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐  │
│  │   S3     │  │   EC2    │  │   ALB     │  │  Custom   │  │
│  │  Bucket  │  │  Instance│  │  (ELB)    │  │  Origin   │  │
│  └──────────┘  └──────────┘  └──────────┘  └──────────┘  │
└─────────────────────────────────────────────────────────────┘
```

### Fluxo de Requisição

1. **Usuário faz requisição** → `https://d1234.cloudfront.net/imagem.jpg`
2. **DNS resolve** → Route 53 direciona para Edge Location mais próxima
3. **Edge Location verifica cache:**
   - ✅ **Cache Hit:** Retorna conteúdo imediatamente (baixa latência)
   - ❌ **Cache Miss:** Busca no Origin, armazena em cache e retorna
4. **Conteúdo entregue** ao usuário com baixa latência

---

## Conceitos Fundamentais

### Edge Locations (Pontos de Presença - PoPs)

- **Função:** Servidores distribuídos globalmente que armazenam cópias do conteúdo
- **Localização:** Centenas de locais em todo o mundo
- **Benefício:** Reduz distância física entre usuário e conteúdo
- **Cache:** Armazena conteúdo frequentemente acessado

### Origin (Origem)

- **Função:** Fonte original do conteúdo
- **Tipos suportados:**
  - **S3 Bucket** (mais comum para conteúdo estático)
  - **EC2 Instance** (aplicações dinâmicas)
  - **Elastic Load Balancer (ALB/NLB)**
  - **Custom Origin** (servidor HTTP/HTTPS próprio)
  - **S3 Website Endpoint**
  - **MediaStore Container**

### Distribution (Distribuição)

- **Função:** Configuração que define como o CloudFront entrega conteúdo
- **Tipos:**
  - **Web Distribution:** Para sites, APIs, conteúdo HTTP/HTTPS
  - **RTMP Distribution:** Para streaming de vídeo (deprecated)

### Cache Behavior (Comportamento de Cache)

- **Função:** Define regras de como o CloudFront trata requisições
- **Configurações:**
  - Path patterns (caminhos)
  - TTL (Time To Live) do cache
  - Headers permitidos
  - Query strings
  - Cookies

---

## Características Principais

### 1. Desempenho Melhorado

**Como funciona:**
- Rede global de **Edge Locations (PoPs)** em centenas de locais
- Roteamento inteligente para o PoP mais próximo do usuário
- Cache de conteúdo estático e dinâmico
- Otimizações automáticas de protocolo (HTTP/2, HTTP/3)

**Benefícios:**
- ✅ Redução significativa de latência
- ✅ Maior velocidade de transferência
- ✅ Melhor experiência do usuário
- ✅ Redução de carga no servidor origin

**Exemplo:**

```
Sem CloudFront:
Usuário (Brasil) → Origin (us-east-1) → ~150ms de latência

Com CloudFront:
Usuário (Brasil) → Edge Location (São Paulo) → ~10ms de latência
```

---

### 2. Segurança Robusta

O CloudFront oferece múltiplas camadas de segurança:

#### AWS Shield Integration
- **Shield Standard:** Proteção DDoS básica (gratuita)
- **Shield Advanced:** Proteção DDoS avançada (paga)
- Proteção automática contra ataques distribuídos

#### AWS WAF (Web Application Firewall)
- Filtragem de requisições maliciosas
- Proteção contra SQL injection, XSS, etc.
- Regras customizáveis
- Rate limiting

#### HTTPS e SSL/TLS
- Entrega segura de conteúdo via HTTPS
- Integração com **AWS Certificate Manager (ACM)**
- Certificados SSL/TLS gerenciados automaticamente
- Suporte a TLS 1.2 e 1.3
- Redirecionamento automático HTTP → HTTPS

#### Signed URLs e Signed Cookies
- Controle de acesso a conteúdo privado
- URLs temporárias com expiração
- Cookies assinados para acesso restrito

**Diagrama de Segurança:**

```
┌─────────────────────────────────────────────────────────┐
│                    USUÁRIO                              │
└───────────────────────┬─────────────────────────────────┘
                        │
                        │ Requisição HTTPS
                        ▼
┌─────────────────────────────────────────────────────────┐
│              AWS Shield (DDoS Protection)                │
└───────────────────────┬─────────────────────────────────┘
                        │
                        ▼
┌─────────────────────────────────────────────────────────┐
│              AWS WAF (Web Application Firewall)         │
│  - Filtra requisições maliciosas                        │
│  - Rate limiting                                        │
│  - Proteção contra SQL injection, XSS                   │
└───────────────────────┬─────────────────────────────────┘
                        │
                        ▼
┌─────────────────────────────────────────────────────────┐
│              CloudFront Distribution                    │
│  - HTTPS/TLS                                            │
│  - Signed URLs (se configurado)                         │
└───────────────────────┬─────────────────────────────────┘
                        │
                        ▼
┌─────────────────────────────────────────────────────────┐
│                    ORIGIN                               │
└─────────────────────────────────────────────────────────┘
```

---

### 3. Escalabilidade Automática

**Características:**
- ✅ Escala automaticamente sem intervenção manual
- ✅ Lida com picos de tráfego instantaneamente
- ✅ Sem necessidade de provisionamento prévio
- ✅ Suporta milhões de requisições por segundo
- ✅ Distribui carga globalmente

**Exemplo de Cenário:**

```
Evento ao vivo (lançamento de produto):
- 10:00 AM: 1.000 usuários simultâneos
- 10:05 AM: 100.000 usuários simultâneos
- 10:10 AM: 1.000.000 usuários simultâneos

CloudFront escala automaticamente sem downtime
```

---

### 4. Personalização e Otimização

O CloudFront permite personalizar a entrega de conteúdo:

#### Cache Policies
- **CachingOptimized:** Máximo cache (conteúdo estático)
- **CachingDisabled:** Sem cache (conteúdo dinâmico)
- **Elemental-MediaPackage:** Para streaming de vídeo

#### Origin Request Policies
- Controla quais headers/query strings são enviados ao origin
- Reduz carga no servidor origin

#### Response Headers Policies
- Adiciona headers de segurança (CORS, CSP, etc.)
- Customização de headers de resposta

#### Compression
- Compressão automática (Gzip, Brotli)
- Reduz tamanho de transferência
- Melhora velocidade de carregamento

---

### 5. Integração com Serviços AWS

O CloudFront integra-se profundamente com outros serviços AWS:

#### S3 (Simple Storage Service)
- **Uso mais comum:** Hospedar sites estáticos
- **Benefício:** Baixo custo de armazenamento
- **Configuração:** Origin aponta para S3 bucket

**Exemplo:**
```
S3 Bucket: meu-site.s3.amazonaws.com
CloudFront Distribution: d1234.cloudfront.net
→ CloudFront entrega conteúdo do S3 com cache global
```

#### EC2 e Elastic Load Balancer
- **Uso:** Aplicações dinâmicas
- **Benefício:** Cache de conteúdo estático, acelera dinâmico
- **Configuração:** Origin aponta para ALB/NLB

#### Route 53
- **Uso:** DNS para domínios customizados
- **Benefício:** Integração nativa com CloudFront
- **Configuração:** Alias record aponta para CloudFront

#### Lambda@Edge
- **Função:** Executa código Lambda nas Edge Locations
- **Uso:** Personalização de requisições/respostas
- **Benefício:** Processamento na borda (baixa latência)

#### AWS Certificate Manager (ACM)
- **Uso:** Gerenciamento de certificados SSL/TLS
- **Benefício:** Certificados gratuitos e renovação automática

---

## Tipos de Distribuição

### Web Distribution

**Uso:** Sites, APIs, conteúdo HTTP/HTTPS

**Características:**
- Suporta HTTP e HTTPS
- Cache de conteúdo estático e dinâmico
- Integração com Lambda@Edge
- Suporte a múltiplos origins

**Exemplo de Configuração:**

```
Distribution Type: Web
Origin: meu-bucket.s3.amazonaws.com
Default Cache Behavior:
  - Viewer Protocol Policy: Redirect HTTP to HTTPS
  - Allowed HTTP Methods: GET, HEAD, OPTIONS
  - Cache Policy: CachingOptimized
  - TTL: 86400 segundos (1 dia)
```

### RTMP Distribution (Deprecated)

**Status:** Descontinuado pela AWS
**Alternativa:** Use MediaPackage ou outros serviços de streaming

---

## Casos de Uso Comuns

### 1. Sites Estáticos

**Cenário:** Site hospedado no S3

**Configuração:**
```
Origin: S3 Bucket (site estático)
Cache: Máximo (conteúdo raramente muda)
HTTPS: Habilitado (certificado ACM)
```

**Benefícios:**
- ✅ Baixo custo (S3 + CloudFront)
- ✅ Alta performance global
- ✅ Escalabilidade automática
- ✅ SSL/TLS gratuito

---

### 2. Streaming de Vídeo

**Cenário:** Plataforma de vídeo on-demand

**Configuração:**
```
Origin: S3 Bucket ou MediaStore
Cache: Vídeos populares em cache
Signed URLs: Para conteúdo premium
```

**Benefícios:**
- ✅ Baixa latência de início de reprodução
- ✅ Redução de custos de transferência
- ✅ Suporte a múltiplos formatos
- ✅ Proteção de conteúdo com Signed URLs

---

### 3. APIs e Aplicações Dinâmicas

**Cenário:** API REST com conteúdo dinâmico

**Configuração:**
```
Origin: ALB (Application Load Balancer)
Cache: Apenas endpoints estáticos
Lambda@Edge: Personalização de requisições
```

**Benefícios:**
- ✅ Cache de respostas de API quando apropriado
- ✅ Redução de carga no servidor
- ✅ Melhor performance global
- ✅ Proteção com WAF

---

### 4. Distribuição de Software

**Cenário:** Downloads de aplicativos, patches, atualizações

**Configuração:**
```
Origin: S3 Bucket
Cache: Longo TTL (arquivos raramente mudam)
Signed URLs: Para downloads privados
```

**Benefícios:**
- ✅ Alta velocidade de download global
- ✅ Redução de custos de transferência
- ✅ Controle de acesso com Signed URLs
- ✅ Escalabilidade para milhões de downloads

---

## Configurações Avançadas

### Cache Behaviors (Comportamentos de Cache)

Permite configurar diferentes comportamentos para diferentes paths:

```
Path Pattern: /images/*
  - Cache Policy: CachingOptimized
  - TTL: 31536000 (1 ano)
  - Compress: Sim

Path Pattern: /api/*
  - Cache Policy: CachingDisabled
  - TTL: 0 (sem cache)
  - Compress: Sim

Path Pattern: /*
  - Cache Policy: CachingOptimized
  - TTL: 86400 (1 dia)
```

### Signed URLs e Signed Cookies

**Signed URLs:** URLs temporárias com expiração

```
Exemplo:
https://d1234.cloudfront.net/video.mp4?
  Expires=1234567890&
  Signature=abc123...
```

**Signed Cookies:** Cookies assinados para acesso restrito

**Uso:**
- Conteúdo premium
- Downloads privados
- Vídeos pagos
- Documentos confidenciais

### Custom Error Pages

Permite personalizar páginas de erro:

```
404 Not Found → /custom-404.html
403 Forbidden → /custom-403.html
500 Error → /custom-500.html
```

### Field-Level Encryption

Criptografia de campos específicos em requisições:
- Dados sensíveis (cartão de crédito, SSN)
- Criptografia antes de enviar ao origin
- Descriptografia no origin

---

## Modelo de Preços (Pay-as-you-go)

### Componentes de Custo

1. **Transferência de Dados (Data Transfer Out)**
   - Primeiros 10 TB/mês: $0.085 por GB
   - Próximos 40 TB/mês: $0.080 por GB
   - Próximos 100 TB/mês: $0.060 por GB
   - Acima de 150 TB/mês: $0.040 por GB

2. **Requisições HTTP/HTTPS**
   - Primeiros 10 milhões: $0.0075 por 10.000
   - Acima de 10 milhões: $0.0070 por 10.000

3. **Invalidation Requests**
   - Primeiras 1.000 invalidações/mês: Grátis
   - Acima de 1.000: $0.005 por path

### Opções de Economia

#### CloudFront Savings Plans
- Compromisso de uso (1 ou 3 anos)
- Desconto de até 30%
- Ideal para uso previsível e consistente

#### Data Transfer Out to Internet
- Desconto progressivo por volume
- Quanto mais dados transferidos, menor o custo por GB

---

## Invalidação de Cache

Quando você atualiza conteúdo, pode precisar limpar o cache:

### Métodos de Invalidação

1. **Invalidation Manual**
   - Console AWS ou API
   - Especifica paths a invalidar
   - Processamento em alguns minutos
   - Custo após 1.000/mês

2. **Versionamento de Arquivos**
   - Adiciona versão ao nome do arquivo
   - `imagem.jpg` → `imagem-v2.jpg`
   - Evita necessidade de invalidação
   - **Recomendado:** Melhor prática

**Exemplo de Versionamento:**

```
Antes:
https://d1234.cloudfront.net/logo.png

Depois (com versionamento):
https://d1234.cloudfront.net/logo-v2.png
```

---

## Integração com Lambda@Edge

**Lambda@Edge** permite executar código Lambda nas Edge Locations:

### Tipos de Triggers

1. **Viewer Request:** Antes de verificar cache
2. **Origin Request:** Antes de enviar ao origin
3. **Origin Response:** Após receber do origin
4. **Viewer Response:** Antes de enviar ao viewer

### Casos de Uso

- Personalização de conteúdo por região
- A/B testing
- Autenticação na borda
- Modificação de headers
- Redirecionamentos customizados
- Geração de respostas dinâmicas

**Exemplo:**

```javascript
// Lambda@Edge: Adiciona header customizado
exports.handler = (event, context, callback) => {
    const response = event.Records[0].cf.response;
    response.headers['x-custom-header'] = [
        { key: 'X-Custom-Header', value: 'valor-customizado' }
    ];
    callback(null, response);
};
```

---

## Monitoramento e Logs

### CloudWatch Metrics

Métricas disponíveis:
- **Requests:** Número de requisições
- **Bytes Downloaded:** Dados transferidos
- **4xx/5xx Errors:** Erros HTTP
- **Cache Hit Rate:** Taxa de acerto do cache
- **Latency:** Latência de requisições

### Access Logs

Logs detalhados de acesso:
- Requisições recebidas
- Status codes
- IPs dos usuários
- User agents
- Referrers

**Configuração:**
```
Destination: S3 Bucket
Log Prefix: cloudfront-logs/
Retention: Configurável
```

---

## Resumo Mental

- **Amazon CloudFront**
  - CDN (Content Delivery Network) da AWS
  - **Conceitos:**
    - Edge Locations (PoPs)
    - Origin (S3, EC2, ALB, Custom)
    - Distribution (Web, RTMP)
    - Cache Behavior
  - **Características:**
    - Desempenho melhorado (baixa latência)
    - Segurança (Shield, WAF, HTTPS)
    - Escalabilidade automática
    - Personalização e otimização
  - **Integrações:**
    - S3 (sites estáticos)
    - EC2/ALB (aplicações dinâmicas)
    - Route 53 (DNS)
    - Lambda@Edge (processamento na borda)
    - ACM (certificados SSL/TLS)
  - **Casos de Uso:**
    - Sites estáticos
    - Streaming de vídeo
    - APIs e aplicações
    - Distribuição de software
  - **Configurações:**
    - Cache behaviors
    - Signed URLs/Cookies
    - Custom error pages
    - Field-level encryption
  - **Custos:**
    - Pay-as-you-go
    - Data transfer out
    - Requisições HTTP/HTTPS
    - Savings plans disponíveis
