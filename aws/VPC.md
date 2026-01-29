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
