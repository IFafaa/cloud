# 💰 AWS Budgets — Resumo Completo

## 📌 O que é o AWS Budgets
O **AWS Budgets** é o serviço da AWS utilizado para **criar orçamentos e monitorar gastos**, permitindo **notificações automáticas** quando os custos ou o uso ultrapassam limites definidos.

⚠️ Importante:  
O AWS Budgets **não interrompe nem desliga serviços automaticamente**.  
Ele serve **exclusivamente para alertar** sobre os gastos.

---

## 🎯 Objetivo do AWS Budgets
- Acompanhar como os gastos estão evoluindo
- Evitar surpresas na fatura
- Ajudar no controle financeiro da conta AWS
- Facilitar a gestão de custos em ambientes cloud

---

## 📊 Tipos de Orçamento

O AWS Budgets permite criar diferentes tipos de orçamento, como:

- **Orçamento por custo**
  - Baseado no valor gasto (ex: R$ 500 / mês)

- **Orçamento por uso**
  - Baseado no consumo de recursos (ex: horas de EC2)

- **Orçamento por reserva / Savings Plans**
  - Monitora a utilização de compromissos contratados

---

## 🔔 Alertas e Notificações

É possível configurar alertas de diversas formas:

- Quando atingir **X% do orçamento**
  - Ex: 50%, 80%, 100%

- Notificações:
  - Diárias
  - Mensais
  - Em tempo real (quando o limite é ultrapassado)

- Canais de notificação:
  - E-mail
  - SNS (integração com outros serviços)

---

## ⚠️ Pontos Importantes

- Criar um orçamento **não limita nem bloqueia gastos**
- Serviços **continuam rodando normalmente**
- O orçamento serve apenas como:
  - Monitoramento
  - Alerta
  - Controle financeiro

👉 Para ações automáticas (ex: desligar recursos), é necessário integrar com:
- AWS Lambda
- AWS SNS
- AWS EventBridge

---

## 🧠 Resumo Mental (Visão Geral)

- AWS Budgets
  - Controle de Custos
  - Monitoramento de Gastos
  - Alertas Automáticos
    - Percentual do orçamento
    - Diário / Mensal
  - Não interrompe serviços
  - Apenas notificação

