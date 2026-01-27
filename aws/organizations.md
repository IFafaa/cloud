# AWS Organizations - Resumo Completo

## Visão Geral

O **AWS Organizations** é o serviço da AWS que permite **gerenciar e organizar múltiplas contas AWS de forma centralizada**, facilitando governança, segurança e controle de custos em ambientes complexos.

Ele é especialmente útil para empresas que possuem **vários times, regiões ou ambientes** (dev, stage, prod).

---

## Caso de Uso - Empresa Global

Imagine uma empresa internacional com:
- Uma equipe no **Brasil** (`sa-east-1`)
- Uma equipe nos **Estados Unidos** (`us-east-1`)
- Desenvolvedores em ambos os países

Nesse cenário:
- Não faz sentido um desenvolvedor do Brasil conseguir modificar recursos da conta ou região dos EUA
- Cada time deve ter acesso apenas ao que é necessário

O AWS Organizations permite **isolar contas**, **restringir ações** e **organizar permissões em alto nível**.

---

## Estrutura do AWS Organizations

### Conta de Gerenciamento (Management Account)

- Conta principal da organização
- Responsável por:
  - Criar e gerenciar contas
  - Definir políticas globais
  - Visualizar custos consolidados
- Deve ser altamente protegida

### Unidades Organizacionais (OUs)

As **Organizational Units (OUs)** permitem agrupar contas com objetivos semelhantes.

**Exemplos de OUs:**
- `Brazil`
- `USA`
- `Development`
- `Production`
- `Finance`

Políticas podem ser aplicadas no nível da OU, afetando todas as contas dentro dela.

### Contas AWS

- Cada conta é isolada por padrão
- Ideal para:
  - Separar ambientes (dev/stage/prod)
  - Separar times
  - Reduzir impacto de falhas ou erros humanos

---

## Centralização de Custos

Uma grande vantagem do AWS Organizations é a **centralização do faturamento**.

- Uma única fatura consolidada
- Custos distribuídos por conta
- Melhor visibilidade e controle financeiro
- Não é necessário criar múltiplas contas root independentes

Ideal para empresas com estrutura global.

---

## Políticas de Controle de Serviço (SCPs)

As **Service Control Policies (SCPs)** definem **o que é permitido ou proibido** em nível organizacional.

### Pontos importantes

- SCPs **não concedem permissões**
- SCPs apenas **restringem ações**
- Elas atuam como um **guardrail (proteção)**

Mesmo que o IAM permita uma ação,  
se a SCP negar, a ação **não será executada**.

---

## Relação AWS Organizations x IAM

- **IAM**
  - Define permissões
  - Controla *quem pode fazer o quê*

- **AWS Organizations**
  - Restringe permissões
  - Define *o que nunca pode ser feito*

O Organizations atua **acima do IAM**, garantindo governança e segurança global.

---

## Quando Usar AWS Organizations

- Empresas com múltiplas contas AWS
- Times distribuídos
- Ambientes separados (dev, stage, prod)
- Necessidade de governança e compliance
- Controle financeiro centralizado

---

## Resumo Mental

- AWS Organizations
  - Gerenciamento Centralizado
  - Múltiplas Contas
  - Unidades Organizacionais (OUs)
  - SCPs (Service Control Policies)
    - Apenas restringem
  - Atua acima do IAM
  - Centralização de custos
  - Ideal para empresas e times grandes
