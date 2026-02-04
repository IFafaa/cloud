# VPC (Virtual Private Cloud)

A **VPC** é o serviço da AWS que permite configurar a **rede** onde ficarão localizados seus recursos, como:
- Instâncias EC2
- Bancos de dados (RDS, DynamoDB)
- Load Balancers
- Outros serviços AWS

> **Nota:** Buckets S3 não ficam dentro de VPCs, mas podem ser acessados através de VPC Endpoints.

---

## Estrutura de Rede na AWS

A hierarquia básica de rede na AWS segue esta estrutura:

```
┌─────────────────────────────────────────────────────────┐
│                    REGION (us-east-1)                   │
│                                                          │
│  ┌──────────────────────────────────────────────────┐  │
│  │              VPC (172.16.0.0/16)                 │  │
│  │                                                   │  │
│  │  ┌──────────────────────────────────────────┐   │  │
│  │  │      Subnet A (172.16.0.0/20)            │   │  │
│  │  │  ┌──────────────┐  ┌──────────────┐      │   │  │
│  │  │  │  EC2-1       │  │  EC2-2       │      │   │  │
│  │  │  │  172.16.0.10 │  │  172.16.0.11 │      │   │  │
│  │  │  └──────────────┘  └──────────────┘      │   │  │
│  │  └──────────────────────────────────────────┘   │  │
│  │                                                   │  │
│  │  ┌──────────────────────────────────────────┐   │  │
│  │  │      Subnet B (172.16.16.0/20)           │   │  │
│  │  │  ┌──────────────┐  ┌──────────────┐      │   │  │
│  │  │  │  RDS-DB      │  │  EC2-3       │      │   │  │
│  │  │  │  172.16.16.5 │  │  172.16.16.10│      │   │  │
│  │  │  └──────────────┘  └──────────────┘      │   │  │
│  │  └──────────────────────────────────────────┘   │  │
│  │                                                   │  │
│  │  ┌──────────────────────────────────────────┐   │  │
│  │  │      Subnet C (172.16.32.0/20)           │   │  │
│  │  │  ┌──────────────┐                        │   │  │
│  │  │  │  EC2-4       │                        │   │  │
│  │  │  │  172.16.32.5 │                        │   │  │
│  │  │  └──────────────┘                        │   │  │
│  │  └──────────────────────────────────────────┘   │  │
│  └──────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────┘
```

### Hierarquia Simplificada

```
Region
  └── VPC (CIDR Block)
        └── Subnet (CIDR Block menor)
              └── Instâncias/Recursos (IPs específicos)
```

---

## Componentes Principais da VPC

### 1. VPC (Virtual Private Cloud)
- **Função:** Isola sua rede logicamente na AWS
- **CIDR Block:** Define o range de IPs disponível (ex: `172.16.0.0/16`)
- **Escopo:** Uma VPC existe dentro de uma única região

### 2. Subnets
- **Função:** Dividem a VPC em segmentos menores
- **Tipos:**
  - **Public Subnet:** Tem rota para Internet Gateway (acesso público)
  - **Private Subnet:** Sem rota direta para internet (mais segura)
- **CIDR Block:** Deve estar dentro do range da VPC

### 3. Internet Gateway (IGW)
- **Função:** Permite comunicação bidirecional entre VPC e internet
- **Características:**
  - Um por VPC
  - Altamente disponível e escalável
  - Não adiciona latência

### 4. Route Tables (Tabelas de Rota)
- **Função:** Define para onde o tráfego de rede é direcionado
- **Rotas comuns:**
  - `0.0.0.0/0` → Internet Gateway (tráfego público)
  - `10.0.0.0/16` → Local (tráfego dentro da VPC)

---

## Conectividade com a Internet

Para que sua VPC tenha acesso à internet, é necessário:

### Configuração Básica

```
┌─────────────────────────────────────────────┐
│           INTERNET                          │
└──────────────────┬──────────────────────────┘
                   │
                   │
        ┌──────────▼──────────┐
        │  Internet Gateway   │
        │      (IGW)          │
        └──────────┬──────────┘
                   │
                   │
        ┌──────────▼──────────┐
        │       VPC            │
        │  ┌────────────────┐ │
        │  │  Route Table   │ │
        │  │  0.0.0.0/0 →   │ │
        │  │  IGW           │ │
        │  └────────────────┘ │
        │                      │
        │  ┌────────────────┐ │
        │  │  Public Subnet │ │
        │  │  (associada à  │ │
        │  │  Route Table)  │ │
        │  └────────────────┘ │
        └──────────────────────┘
```

### Componentes Necessários

1. **Internet Gateway**
   - Criado e anexado à VPC
   - Responsável por permitir comunicação entre VPC e internet
   - Gratuito (sem custo adicional)

2. **Route Table**
   - Deve ser configurada na VPC
   - Exemplo de rota:
     ```
     Destino          | Target
     -----------------|------------------
     172.16.0.0/16    | local (VPC)
     0.0.0.0/0        | igw-xxxxx (Internet Gateway)
     ```
   - A rota `0.0.0.0/0` significa: "todo tráfego não local vai para o Internet Gateway"

---

## Exemplo Prático Completo

### Cenário: Aplicação Web com Banco de Dados

Vamos criar uma VPC para hospedar uma aplicação web com alta disponibilidade:

```
┌─────────────────────────────────────────────────────────────────────┐
│                    REGION: us-east-1                                │
│                                                                      │
│  ┌──────────────────────────────────────────────────────────────┐  │
│  │  VPC: minha-vpc-producao                                     │  │
│  │  CIDR: 172.16.0.0/16 (65.536 IPs disponíveis)               │  │
│  │                                                               │  │
│  │  ┌──────────────────────────────────────────────────────────┐ │  │
│  │  │  Availability Zone: us-east-1a                         │ │  │
│  │  │                                                          │ │  │
│  │  │  ┌──────────────────────────────────────────────────┐  │ │  │
│  │  │  │  Public Subnet A (172.16.0.0/20)                 │  │ │  │
│  │  │  │  ┌────────────┐  ┌────────────┐  ┌────────────┐ │  │ │  │
│  │  │  │  │  EC2-Web-1 │  │  EC2-Web-2 │  │  Load      │ │  │ │  │
│  │  │  │  │  172.16.0.10│  │  172.16.0.11│  │  Balancer │ │  │ │  │
│  │  │  │  └────────────┘  └────────────┘  └────────────┘ │  │ │  │
│  │  │  │  Route Table: 0.0.0.0/0 → Internet Gateway       │  │ │  │
│  │  │  └──────────────────────────────────────────────────┘  │ │  │
│  │  │                                                          │ │  │
│  │  │  ┌──────────────────────────────────────────────────┐  │ │  │
│  │  │  │  Private Subnet A (172.16.16.0/20)                │  │ │  │
│  │  │  │  ┌────────────┐                                   │  │ │  │
│  │  │  │  │  RDS-DB-1  │                                   │  │ │  │
│  │  │  │  │  172.16.16.5│                                   │  │ │  │
│  │  │  │  └────────────┘                                   │  │ │  │
│  │  │  │  Route Table: Apenas tráfego local                │  │ │  │
│  │  │  └──────────────────────────────────────────────────┘  │ │  │
│  │  └──────────────────────────────────────────────────────────┘ │  │
│  │                                                               │  │
│  │  ┌──────────────────────────────────────────────────────────┐ │  │
│  │  │  Availability Zone: us-east-1b                            │ │  │
│  │  │                                                           │ │  │
│  │  │  ┌──────────────────────────────────────────────────┐   │ │  │
│  │  │  │  Public Subnet B (172.16.32.0/20)                │   │ │  │
│  │  │  │  ┌────────────┐  ┌────────────┐                  │   │ │  │
│  │  │  │  │  EC2-Web-3 │  │  EC2-Web-4 │                  │   │ │  │
│  │  │  │  │  172.16.32.10│  │  172.16.32.11│              │   │ │  │
│  │  │  │  └────────────┘  └────────────┘                  │   │ │  │
│  │  │  │  Route Table: 0.0.0.0/0 → Internet Gateway       │   │ │  │
│  │  │  └──────────────────────────────────────────────────┘   │ │  │
│  │  │                                                           │ │  │
│  │  │  ┌──────────────────────────────────────────────────┐   │ │  │
│  │  │  │  Private Subnet B (172.16.48.0/20)               │   │ │  │
│  │  │  │  ┌────────────┐                                   │   │ │  │
│  │  │  │  │  RDS-DB-2  │                                   │   │ │  │
│  │  │  │  │  172.16.48.5│                                   │   │ │  │
│  │  │  │  └────────────┘                                   │   │ │  │
│  │  │  │  Route Table: Apenas tráfego local                │   │ │  │
│  │  │  └──────────────────────────────────────────────────┘   │ │  │
│  │  └──────────────────────────────────────────────────────────┘ │  │
│  │                                                              │  │
│  │  ┌──────────────────────────────────────────────────────┐  │  │
│  │  │  Internet Gateway (igw-1234567890abcdef)             │  │  │
│  │  └──────────────────────────────────────────────────────┘  │  │
│  └──────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────┘
```

### Detalhamento da Configuração

#### VPC Principal
- **Nome:** `minha-vpc-producao`
- **CIDR Block:** `172.16.0.0/16`
- **Região:** `us-east-1`
- **IPs disponíveis:** 65.536 (2^16)

#### Subnets Públicas (Public Subnets)
| Subnet | CIDR | AZ | Uso |
|--------|------|----|-----|
| Public Subnet A | `172.16.0.0/20` | us-east-1a | Servidores web, Load Balancer |
| Public Subnet B | `172.16.32.0/20` | us-east-1b | Servidores web (redundância) |

**Características:**
- Associadas à Route Table com rota para Internet Gateway
- Recursos podem ter IPs públicos
- Acessíveis diretamente da internet

#### Subnets Privadas (Private Subnets)
| Subnet | CIDR | AZ | Uso |
|--------|------|----|-----|
| Private Subnet A | `172.16.16.0/20` | us-east-1a | Banco de dados primário |
| Private Subnet B | `172.16.48.0/20` | us-east-1b | Banco de dados secundário |

**Características:**
- Route Table sem rota para Internet Gateway
- Recursos não têm IPs públicos
- Mais seguras (não acessíveis diretamente da internet)

### Fluxo de Tráfego

```
INTERNET
   │
   ▼
Internet Gateway
   │
   ▼
Public Subnet (Route Table: 0.0.0.0/0 → IGW)
   │
   ├──► EC2-Web-1 (172.16.0.10)
   ├──► EC2-Web-2 (172.16.0.11)
   └──► Load Balancer
           │
           ▼
   Private Subnet (Route Table: apenas local)
           │
           └──► RDS-DB-1 (172.16.16.5)
```

### Benefícios desta Arquitetura

1. **Alta Disponibilidade:** Recursos distribuídos em múltiplas AZs
2. **Segurança:** Bancos de dados em subnets privadas
3. **Escalabilidade:** Fácil adicionar mais instâncias nas subnets
4. **Isolamento:** Tráfego interno permanece dentro da VPC

---

## Resumo dos Conceitos

| Conceito | Descrição | Exemplo |
|----------|-----------|---------|
| **Region** | Localização geográfica | `us-east-1`, `sa-east-1` |
| **VPC** | Rede isolada logicamente | `172.16.0.0/16` |
| **Subnet** | Segmento da VPC em uma AZ | `172.16.0.0/20` |
| **Internet Gateway** | Gateway para internet | `igw-xxxxx` |
| **Route Table** | Tabela de roteamento | Define rotas de rede |
| **Public Subnet** | Subnet com acesso à internet | EC2 com IP público |
| **Private Subnet** | Subnet sem acesso direto à internet | RDS, bancos de dados |

---

## Boas Práticas

1. ✅ Use múltiplas Availability Zones para alta disponibilidade
2. ✅ Separe recursos públicos e privados em subnets diferentes
3. ✅ Mantenha bancos de dados em subnets privadas
4. ✅ Use Network ACLs e Security Groups para segurança adicional
5. ✅ Planeje o CIDR block considerando crescimento futuro
6. ✅ Documente suas rotas e configurações de rede

---

## Serviços de Segurança e Conectividade

Além da estrutura básica de rede, a **VPC** possui integração com diversos serviços da AWS que aumentam o **controle de segurança**, **conectividade** e **observabilidade** do ambiente.

---

### Segurança de Rede

#### NACL (Network Access Control List)

- **Função:** Protege **subnets** (entrada e saída)
- **Características:**
  - Funciona como uma **lista de regras** (firewall de nível de subnet)
  - As regras são avaliadas **de cima para baixo**
  - A primeira regra que corresponde define se o tráfego é permitido ou negado
  - **Stateless:** Precisa de regras explícitas para entrada E saída
- **Analogia:** Segurança de uma festa conferindo a lista e liberando a entrada

**Exemplo de Regras NACL:**
```
Regra # | Tipo   | Protocolo | Porta | Origem/Destino | Ação
--------|--------|-----------|-------|----------------|------
100     | HTTP   | TCP       | 80    | 0.0.0.0/0      | PERMITIR
200     | HTTPS  | TCP       | 443   | 0.0.0.0/0      | PERMITIR
*       | ALL    | ALL       | ALL   | 0.0.0.0/0      | NEGAR
```

> **Nota:** NACL opera no nível de subnet, enquanto Security Groups operam no nível de instância.

#### VPC Flow Logs

- **Função:** Fornece **observabilidade da VPC**
- **Registra:**
  - O que entra na VPC
  - O que sai da VPC
  - Origem e destino do tráfego
  - Protocolos e portas utilizadas
- **Útil para:**
  - Auditoria de segurança
  - Análise de tráfego
  - Debug de problemas de rede
  - Detecção de anomalias
- **Destinos:** CloudWatch Logs, S3, ou Kinesis Data Firehose

**Exemplo de Log:**
```
2 123456789010 eni-abc123 10.0.1.5 172.31.80.31 443 49153 6 20 4249 1418530010 1418530070 ACCEPT OK
```

---

### Conectividade entre VPCs

#### VPC Peering

- **Função:** Cria um **"túnel" de conexão direta entre duas VPCs**
- **Características:**
  - Conexão ponto-a-ponto
  - Ideal para conexões simples (2-3 VPCs)
  - Não há custo de transferência entre VPCs na mesma região
- **Limitações:**
  - Pouco escalável (não recomendado para muitos relacionamentos)
  - Não transitivo (VPC A ↔ VPC B ↔ VPC C não permite A ↔ C diretamente)
  - Requer configuração de rotas em ambas as VPCs

**Diagrama:**
```
┌──────────────┐         ┌──────────────┐
│   VPC A      │◄───────►│   VPC B      │
│ 10.0.0.0/16  │ Peering │ 172.16.0.0/16│
└──────────────┘         └──────────────┘
```

#### AWS Transit Gateway

- **Função:** Hub central de conexão entre múltiplas VPCs e outros recursos
- **Conecta:**
  - Múltiplas VPCs
  - VPNs (Site-to-Site e Client VPN)
  - Direct Connect
  - Outros Transit Gateways
- **Vantagens:**
  - Altamente escalável
  - Roteamento transitivo
  - Gerenciamento centralizado
  - Ideal para ambientes grandes e complexos
- **Alternativa recomendada ao VPC Peering** quando há muitas VPCs

**Diagrama:**
```
        ┌──────────────────┐
        │ Transit Gateway  │
        │   (Hub Central)  │
        └────────┬─────────┘
                 │
    ┌────────────┼────────────┐
    │            │            │
┌───▼───┐   ┌───▼───┐   ┌───▼───┐
│ VPC A │   │ VPC B │   │ VPC C │
└───────┘   └───────┘   └───────┘
```

---

### Conectividade com Serviços AWS

#### VPC Endpoints

- **Função:** Cria uma conexão **privada** entre uma VPC e serviços da AWS
- **Características:**
  - Não expõe o tráfego à internet pública
  - Usa a infraestrutura privada da AWS
  - Aumenta a segurança
  - Reduz dependência de internet pública
- **Tipos:**
  - **Gateway Endpoints:** Para S3 e DynamoDB (gratuito)
  - **Interface Endpoints:** Para outros serviços (custo por hora + dados)
- **Exemplo comum:** Acesso privado ao **S3** sem passar pela internet

**Diagrama:**
```
┌──────────────┐
│     VPC      │
│              │
│  ┌────────┐  │
│  │  EC2   │──┼──► VPC Endpoint (privado)
│  └────────┘  │              │
└──────────────┘              │
                              ▼
                        ┌─────────┐
                        │   S3    │
                        └─────────┘
```

#### AWS PrivateLink

- **Função:** Solução para expor serviços hospedados na sua VPC de forma **segura e escalável**
- **Cenário de uso:**
  - Você tem um serviço/app hospedado em EC2 dentro de uma VPC
  - Vários clientes querem consumir esse serviço
  - Precisa de conexão privada e segura
- **Por que não VPC Peering?**
  - Não é escalável para muitos clientes
  - Difícil de gerenciar múltiplas conexões
  - Requer configuração em cada VPC cliente
- **Solução:**
  - Criar um **Network Load Balancer** (NLB)
  - Expor o serviço via **PrivateLink**
  - Conexão privada, segura e escalável para múltiplos clientes
  - Clientes acessam via VPC Endpoint em suas próprias VPCs

**Diagrama:**
```
┌──────────────┐
│ VPC Cliente 1│──┐
└──────────────┘  │
                  │
┌──────────────┐  │    ┌──────────────────┐
│ VPC Cliente 2│──┼───►│  PrivateLink     │
└──────────────┘  │    │  (NLB + Endpoint)│
                  │    └────────┬─────────┘
┌──────────────┐  │             │
│ VPC Cliente 3│──┘             │
└──────────────┘                ▼
                         ┌──────────────┐
                         │ VPC Provedor │
                         │  ┌────────┐  │
                         │  │  EC2   │  │
                         │  │ Service│  │
                         │  └────────┘  │
                         └──────────────┘
```

---

### Conectividade com Ambientes Externos

#### VPC Client VPN

- **Função:** VPN gerenciada da AWS para conectar **usuários individuais** diretamente à AWS
- **Características:**
  - Conecta usuários remotos à VPC
  - Gerenciado pela AWS (sem necessidade de servidor VPN próprio)
  - Suporta autenticação via Active Directory, SAML, etc.
- **Indicado para:**
  - Cloud engineers
  - Equipe de infraestrutura
  - Administradores
  - Desenvolvedores remotos
- **Foco:** Segurança de acesso individual

**Diagrama:**
```
┌──────────────┐
│   Usuário    │
│  (Laptop)    │
└──────┬───────┘
       │
       │ Internet
       │
       ▼
┌──────────────┐
│ Client VPN   │
│  Endpoint    │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│     VPC      │
│  ┌────────┐  │
│  │  EC2   │  │
│  └────────┘  │
└──────────────┘
```

#### VPC Site-to-Site VPN

- **Função:** Conexão segura entre infraestrutura on-premises e ambiente AWS
- **Características:**
  - Conecta datacenter/escritório à AWS
  - Voltada para **vários usuários** simultaneamente
  - Suporta maior banda do que o Client VPN
  - Usa túneis IPsec
- **Componentes:**
  - **Virtual Private Gateway (VGW):** Na AWS
  - **Customer Gateway (CGW):** No datacenter do cliente
  - **VPN Connection:** Conexão entre os dois

**Diagrama:**
```
┌──────────────────────┐
│  Datacenter          │
│  On-Premises         │
│  ┌──────────────┐   │
│  │ Customer     │   │
│  │ Gateway      │   │
│  └──────┬───────┘   │
└─────────┼───────────┘
          │
          │ Internet (IPsec VPN)
          │
          ▼
┌──────────────────────┐
│  AWS                 │
│  ┌──────────────┐   │
│  │ Virtual      │   │
│  │ Private      │   │
│  │ Gateway      │   │
│  └──────┬───────┘   │
│         │           │
│         ▼           │
│  ┌──────────────┐   │
│  │     VPC      │   │
│  └──────────────┘   │
└──────────────────────┘
```

#### AWS Direct Connect

- **Função:** Cria uma **conexão física direta** entre você e a AWS
- **Características:**
  - Literalmente um cabo dedicado (fibra óptica)
  - Não passa pela internet pública
  - Alta performance e baixa latência
  - Alta estabilidade e disponibilidade
- **Benefícios:**
  - Baixa latência consistente
  - Alta estabilidade (SLA de 99.99%)
  - Redução de custos de transferência de dados (em grandes volumes)
  - Não depende da internet pública
- **Tipos:**
  - **Dedicated Connection:** Conexão física dedicada
  - **Hosted Connection:** Compartilhada através de parceiro

**Diagrama:**
```
┌──────────────────────┐
│  Datacenter          │
│  On-Premises         │
│  ┌──────────────┐   │
│  │ Router       │   │
│  └──────┬───────┘   │
└─────────┼───────────┘
          │
          │ Conexão Física Dedicada
          │ (Fibra Óptica)
          │
          ▼
┌──────────────────────┐
│  AWS Direct Connect  │
│  Location            │
└─────────┬───────────┘
          │
          ▼
┌──────────────────────┐
│  AWS                 │
│  ┌──────────────┐   │
│  │ Virtual      │   │
│  │ Private      │   │
│  │ Gateway      │   │
│  └──────┬───────┘   │
│         │           │
│         ▼           │
│  ┌──────────────┐   │
│  │     VPC      │   │
│  └──────────────┘   │
└──────────────────────┘
```

---

## Resumo de Serviços de Conectividade

| Serviço | Uso | Escalabilidade | Custo |
|---------|-----|----------------|-------|
| **VPC Peering** | Conectar 2-3 VPCs | Baixa | Gratuito (mesma região) |
| **Transit Gateway** | Hub para múltiplas VPCs | Alta | Por hora + dados |
| **VPC Endpoints** | Acesso privado a serviços AWS | Alta | Gateway: Grátis / Interface: Por hora |
| **PrivateLink** | Expor serviços para múltiplos clientes | Alta | Por hora + dados |
| **Client VPN** | Usuários individuais → AWS | Média | Por hora + dados |
| **Site-to-Site VPN** | Datacenter → AWS | Média | Por hora |
| **Direct Connect** | Conexão física dedicada | Alta | Taxa mensal + dados |

---

## Quando Usar Cada Serviço

### Segurança
- **NACL:** Controle de tráfego no nível de subnet (complementa Security Groups)
- **VPC Flow Logs:** Auditoria, monitoramento e troubleshooting de rede

### Conectividade entre VPCs
- **VPC Peering:** Poucas VPCs (2-3), conexões simples
- **Transit Gateway:** Muitas VPCs, arquitetura complexa, necessidade de roteamento transitivo

### Conectividade com Serviços AWS
- **VPC Endpoints:** Acesso privado a S3, DynamoDB, outros serviços AWS
- **PrivateLink:** Expor seus próprios serviços para múltiplos clientes de forma escalável

### Conectividade Externa
- **Client VPN:** Usuários individuais precisam acessar recursos na AWS
- **Site-to-Site VPN:** Conectar datacenter/escritório à AWS via internet
- **Direct Connect:** Necessidade de alta performance, baixa latência, grande volume de dados
