# AWS Lambda

O **AWS Lambda** é o serviço de **computação serverless** da AWS que permite executar **códigos/scripts sob demanda**, sem precisar provisionar ou gerenciar servidores.

Você apenas envia o código, define quando ele deve rodar, e a AWS cuida de toda a infraestrutura.

---

## Características Principais

- Execução de código **sob demanda**
- Totalmente **serverless**
- Suporte a várias linguagens (Node.js, Python, Java, Go, etc.)
- Escala automaticamente
- Modelo **pay as you go** (paga apenas pelo tempo de execução)

---

## Como Funciona

1. Você faz upload do código (função Lambda)
2. Define o **evento de disparo** (trigger)
3. O Lambda é executado automaticamente
4. Os logs são gerados e enviados para o **CloudWatch**

---

## Integrações Comuns

O Lambda pode:
- Manipular arquivos no **S3**
- Ler e escrever no **DynamoDB**
- Consumir e publicar mensagens em **SQS / SNS**
- Ser acionado via **HTTP (API Gateway)**
- Integrar com praticamente qualquer serviço da AWS

---

## Casos de Uso Comuns

- Processamento de arquivos enviados ao S3
- APIs serverless (via API Gateway)
- Automação de tarefas
- Execução de jobs assíncronos
- Integrações entre serviços AWS
- Processamento de eventos em tempo real

---

## Logs e Observabilidade

- Todos os logs são enviados automaticamente para o **Amazon CloudWatch**
- Facilita debug, métricas e monitoramento

---

## Quando Usar AWS Lambda

- Quando você não quer gerenciar servidores
- Para workloads **event-driven**
- Para aplicações altamente escaláveis
- Para tarefas curtas e bem definidas
