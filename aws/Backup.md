# AWS Backup

O **AWS Backup** é um serviço gerenciado da AWS que permite **centralizar e automatizar backups** de dados em toda a arquitetura AWS.

---

## Visão Geral

O AWS Backup oferece uma solução unificada para fazer backup de:
- Dados de aplicações
- Configurações de serviços
- Infraestrutura completa
- Ambientes híbridos (on-premises e cloud)

---

## Características Principais

- **Backup Centralizado**
  - Interface única para gerenciar backups
  - Visibilidade de todos os backups
  - Políticas de backup consistentes

- **Suporte a Múltiplos Serviços**
  - **EC2**: Instâncias e volumes
  - **EBS**: Volumes de armazenamento
  - **RDS**: Bancos de dados relacionais
  - **DynamoDB**: Bancos de dados NoSQL
  - **EFS**: Sistema de arquivos
  - **Storage Gateway**: Gateways de armazenamento
  - **FSx**: Sistemas de arquivos Windows e Lustre
  - E muitos outros

- **Políticas de Backup (Backup Plans)**
  - Agendamento automático
  - Retenção configurável
  - Lifecycle management
  - Regras de backup por tags

- **Recuperação**
  - Restore point-in-time
  - Restore completo ou parcial
  - Restore cross-region
  - Restore cross-account

- **Compliance e Auditoria**
  - Logs de todas as operações
  - Integração com AWS CloudTrail
  - Relatórios de conformidade

---

## Casos de Uso Comuns

- **Backup Automatizado**
  - Backups diários, semanais ou mensais
  - Políticas de retenção
  - Lifecycle management automático

- **Disaster Recovery**
  - Backup de toda a arquitetura
  - Recuperação rápida em caso de desastre
  - Backup cross-region para alta disponibilidade

- **Compliance**
  - Atender requisitos regulatórios
  - Políticas de retenção obrigatórias
  - Auditoria e rastreabilidade

- **Migração e Testes**
  - Backup antes de mudanças
  - Restore para ambientes de teste
  - Clonagem de ambientes

---

## Benefícios

- **Simplicidade**: Interface única para todos os backups
- **Automação**: Backups agendados e automatizados
- **Confiabilidade**: Backups consistentes e verificados
- **Custo-Otimizado**: Lifecycle management reduz custos
- **Compliance**: Atende requisitos regulatórios

---

## Quando Usar AWS Backup

- Quando você precisa fazer backup de múltiplos serviços AWS
- Para automatizar políticas de backup
- Quando você quer centralizar o gerenciamento de backups
- Para atender requisitos de compliance e auditoria
- Quando você precisa de disaster recovery automatizado
