# AWS STS (Security Token Service)

O **AWS STS (Security Token Service)** é um serviço da AWS que **gera credenciais de acesso temporárias e seguras** para acessar recursos e serviços da AWS.

---

## Visão Geral

O STS permite que você solicite credenciais temporárias (tokens) que podem ser usadas para acessar serviços AWS de forma segura, sem precisar compartilhar credenciais permanentes.

---

## Características Principais

- **Credenciais Temporárias**
  - Tokens com tempo de expiração configurável
  - Podem ser renovados ou expirados automaticamente
  - Mais seguras que credenciais permanentes

- **Controle de Acesso Granular**
  - Permissões específicas por token
  - Baseado em IAM roles e policies
  - Acesso limitado no tempo e escopo

- **Integração com Serviços AWS**
  - EC2 pode assumir roles para acessar S3
  - Lambda pode acessar outros serviços
  - Aplicações podem obter credenciais temporárias

---

## Como Funciona

**Exemplo prático:**
- Um **EC2** precisa acessar um bucket **S3**
- Em vez de usar credenciais permanentes (não recomendado)
- O EC2 assume uma **IAM Role** via STS
- O STS gera um **token temporário** com permissões específicas
- O EC2 usa esse token para acessar o S3
- O token expira automaticamente após o tempo configurado

---

## Casos de Uso Comuns

- EC2 acessando outros serviços AWS (S3, DynamoDB, etc.)
- Aplicações assumindo roles temporárias
- Acesso cross-account seguro
- Integração com provedores de identidade externos (via Cognito)
- Acesso temporário para usuários ou sistemas externos

---

## Benefícios

- **Segurança aprimorada**: Credenciais temporárias reduzem o risco de vazamento
- **Princípio do menor privilégio**: Permissões específicas e limitadas
- **Auditoria**: Todas as requisições são registradas no CloudTrail
- **Rotação automática**: Tokens expiram e podem ser renovados

---

## Quando Usar AWS STS

- Quando serviços AWS precisam acessar outros serviços
- Quando você quer evitar usar credenciais permanentes
- Para implementar acesso cross-account seguro
- Para fornecer acesso temporário a recursos AWS
- Em integrações com sistemas externos que precisam de acesso limitado
