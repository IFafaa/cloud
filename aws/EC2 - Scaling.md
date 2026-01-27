# Escalabilidade no EC2 - Resumo Completo

## Visão Geral

O **Amazon EC2** possui diversos recursos que permitem **escalar aplicações automaticamente**, garantindo performance, disponibilidade e otimização de custos.

Existem **dois tipos principais de escalabilidade**:

- **Escalabilidade Vertical**
- **Escalabilidade Horizontal**

---

## Escalabilidade Vertical (Vertical Scaling)

A escalabilidade vertical consiste em **aumentar o poder computacional de uma instância existente**.

### Exemplos

- Aumentar CPU
- Aumentar memória (RAM)
- Migrar para um tipo de instância mais potente

### Características

- Simples de implementar
- Pode exigir parada da instância
- Possui limite máximo de hardware

### Indicada para

- Aplicações simples
- Ambientes menores
- Workloads que não escalam facilmente

---

## Escalabilidade Horizontal (Horizontal Scaling)

A escalabilidade horizontal consiste em **adicionar ou remover instâncias EC2**, conforme a demanda.

### Características

- Alta disponibilidade
- Escalabilidade praticamente ilimitada
- Exige balanceamento de carga

Para esse tipo de escalabilidade, é **obrigatório o uso de um Load Balancer**.

---

## Load Balancer (Balanceador de Carga)

O **Load Balancer** é o componente responsável por ficar entre:
- O usuário (browser / cliente)
- As instâncias EC2

Ele distribui as requisições para as instâncias disponíveis, garantindo:
- Melhor desempenho
- Alta disponibilidade
- Tolerância a falhas

---

## Tipos de Load Balancer

### ELB (Classic Load Balancer)

- Indicado para:
  - Serviços internos
  - Aplicações legadas
- Menos recursos que os modelos modernos

### ALB (Application Load Balancer)

- Indicado para:
  - Tráfego público
  - Aplicações web modernas
- Funciona na camada 7 (HTTP/HTTPS)
- Permite:
  - Roteamento por path
  - Roteamento por host
  - Integração com containers e microserviços

---

## Auto Scaling

O **Auto Scaling** é o serviço responsável por **gerenciar automaticamente a quantidade de instâncias EC2**.

### O que ele faz

- Cria novas instâncias quando a demanda aumenta
- Remove instâncias quando a demanda diminui
- Substitui instâncias que falharam
- Mantém a aplicação saudável

### Benefícios

- Alta disponibilidade
- Elasticidade automática
- Otimização de custos

---

## Resumo Mental

- Escalabilidade EC2
  - Vertical
    - Aumentar recursos da instância
    - Limites físicos
  - Horizontal
    - Adicionar/remover instâncias
    - Requer Load Balancer
  - Load Balancer
    - Distribuição de tráfego
    - Alta disponibilidade
    - Tipos
      - ELB (Classic)
      - ALB (Application)
  - Auto Scaling
    - Criação automática de instâncias
    - Substituição em caso de falha
    - Redução de custos
