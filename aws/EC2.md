# Amazon EC2 - Resumo Completo

## Visão Geral

O **Amazon EC2 (Elastic Compute Cloud)** é o serviço da AWS que permite o **aluguel de máquinas virtuais**, chamadas de **instâncias**, para executar diversos tipos de aplicações e sistemas.

Com o EC2, é possível provisionar recursos computacionais sob demanda, de forma escalável e altamente configurável.

---

## Principais Casos de Uso

O EC2 pode ser utilizado para rodar:

- Servidores web
- Aplicações e páginas web
- Bancos de dados
- Servidores de jogos
- Processamento de dados
- Machine Learning e Inteligência Artificial
- Ambientes de teste e desenvolvimento

---

## Tipos de Instância (Configurações de Hardware)

A AWS oferece uma grande variedade de **tipos de instância**, permitindo escolher o hardware ideal para cada cenário.

### Exemplos de escolha por necessidade

- **Banco de Dados**
  - Instâncias com maior capacidade de armazenamento
  - Melhor performance de I/O (disco)

- **Machine Learning / IA**
  - Instâncias com **GPU dedicada**
  - Maior poder de processamento paralelo

- **Servidores de Jogos**
  - Instâncias com melhor **desempenho de rede**
  - Baixa latência é um fator crítico

- **Aplicações Web**
  - Instâncias balanceadas entre CPU, memória e rede

Cada tipo de instância é otimizado para um perfil específico de carga de trabalho.

---

## Sistema de Cobrança

O serviço EC2 possui **três principais modelos de cobrança**:

### On-Demand

- Pague apenas pelo tempo de uso
- Sem compromisso de longo prazo
- Ideal para:
  - Ambientes temporários
  - Testes
  - Workloads imprevisíveis

### Savings Plans

- Contrato de uso por um período definido (ex: 1 ou 3 anos)
- Reduz significativamente o custo
- Ideal para:
  - Workloads estáveis
  - Ambientes de produção previsíveis

### Spot Instances

- Utiliza a capacidade ociosa da AWS
- Custo muito reduzido
- **A instância pode ser interrompida a qualquer momento**
- Ideal para:
  - Testes
  - Processamentos em batch
  - Ambientes que não exigem alta disponibilidade

---

## Security Groups

Os **Security Groups** funcionam como o **firewall das instâncias EC2**.

Eles controlam todo o tráfego de rede **de entrada (inbound)** e **de saída (outbound)**.

### O que é possível configurar

- Quem pode acessar a instância
- Quais portas estão liberadas
- Protocolos permitidos (TCP, UDP, ICMP, etc.)
- IPs específicos ou ranges (CIDR)
- Comunicação entre instâncias

### Características importantes

- As regras são **stateful**
- Se uma requisição de entrada é permitida, a resposta é automaticamente permitida
- Segurança aplicada **no nível da instância**

---

## AMI (Amazon Machine Image)

As **AMIs** são imagens utilizadas para criar instâncias EC2.

### O que uma AMI pode conter

- Sistema operacional
- Configurações da máquina
- Variáveis de ambiente
- Dependências
- Arquivos
- Configurações da aplicação

### Benefícios

- Criação rápida de novas instâncias
- Padronização de ambientes
- Facilita escalabilidade e automação

### Exemplo

- Criar uma AMI baseada em uma instância configurada
- Subir uma nova instância utilizando essa AMI
- A nova instância terá exatamente o mesmo ambiente

---

## Resumo Mental

- Amazon EC2
  - Máquinas Virtuais (Instâncias)
  - Casos de Uso
    - Web
    - Banco de Dados
    - Jogos
    - Machine Learning
  - Tipos de Instância
    - CPU
    - Memória
    - GPU
    - Rede
  - Modelos de Cobrança
    - On-Demand
    - Savings Plans
    - Spot
  - Segurança
    - Security Groups (Firewall)
  - AMI
    - Imagem da instância
    - Padronização
    - Escalabilidade
