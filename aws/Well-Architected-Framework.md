# AWS Well-Architected Framework

O **AWS Well-Architected Framework** é um **guia oficial da AWS** que define as **melhores práticas para projetar, construir e operar soluções em cloud** de forma segura, eficiente e escalável.

Ele serve como base para:
- Avaliar arquiteturas existentes
- Corrigir problemas estruturais
- Criar soluções bem arquitetadas desde o início

---

## Objetivo do Framework

Garantir que aplicações na AWS sejam:
- Seguras
- Confiáveis
- Performáticas
- Econômicas
- Sustentáveis
- Operáveis ao longo do tempo

---

## Os 6 Pilares do AWS Well-Architected Framework

### 1. Excelência Operacional

Refere-se à capacidade de **monitorar, operar e melhorar continuamente** os sistemas.

#### Exemplos
- Monitoramento com **CloudWatch**
- Centralização de logs
- Automação de processos
- Resposta rápida a incidentes

👉 Objetivo: detectar e corrigir problemas antes que impactem o usuário.

---

### 2. Segurança

Foca na **proteção de dados, sistemas e ativos**.

#### Exemplos
- **IAM** (usuários, roles e políticas)
- **MFA** (autenticação multifator)
- **Security Groups** e firewalls
- Criptografia em repouso e em trânsito

👉 Objetivo: reduzir superfícies de ataque e proteger informações sensíveis.

---

### 3. Confiabilidade

Garante que o sistema **continue funcionando mesmo diante de falhas**.

#### Exemplos
- Uso de **múltiplas AZs**
- **Route 53** com políticas de failover
- Recuperação automática de falhas
- Backups e snapshots

👉 Objetivo: manter alta disponibilidade e rápida recuperação.

---

### 4. Eficiência de Desempenho

Busca utilizar os recursos corretos para cada tipo de workload.

#### Exemplos
- **Auto Scaling** para EC2
- Escolha correta de tipos de instância
- Uso de serviços gerenciados
- Cache com **ElastiCache**

👉 Objetivo: máxima performance sem desperdício de recursos.

---

### 5. Otimização de Custos

Foca em **reduzir gastos sem comprometer a qualidade** da solução.

#### Exemplos
- Migrar **On-Demand → Reserved / Savings Plans**
- Desligar recursos ociosos
- Usar Auto Scaling
- Monitorar custos com **AWS Budgets**

👉 Objetivo: pagar apenas pelo que realmente é necessário.

---

### 6. Sustentabilidade

Pilar mais recente, voltado para **uso eficiente de recursos e redução de impacto ambiental**.

#### Exemplos
- Redução de recursos ociosos
- Arquiteturas mais eficientes
- Uso de data centers com **energia renovável**
- Otimização de workloads

👉 Objetivo: diminuir consumo energético e impacto ambiental.

---

## Quando Usar o Well-Architected Framework

- Ao criar uma nova arquitetura
- Ao revisar sistemas existentes
- Para preparação para **certificações AWS**
- Para identificar riscos e melhorias

---

## Documentação Oficial

AWS Well-Architected Framework (PT-BR):  
https://docs.aws.amazon.com/pt_br/wellarchitected/latest/framework/the-pillars-of-the-framework.html
