# Fila e Mensageria na AWS

A AWS oferece serviços específicos para **processamento assíncrono**, desacoplamento de sistemas e comunicação entre serviços.

---

## AWS SQS (Simple Queue Service)

O **SQS** é o serviço de **fila** da AWS.

### Características principais
- Mensagens podem ficar armazenadas por até **14 dias**
  - Valor padrão: **4 dias**
- Ideal para processamento assíncrono
- Ajuda a desacoplar serviços
- Evita que o usuário fique “preso” aguardando tarefas demoradas

### Casos de Uso Comuns
- Processamento de jobs em background
- Envio de e-mails após uma ação do usuário
- Geração de relatórios
- Processamento de uploads
- Integração entre microserviços

### Exemplos práticos de uso de fila
- Usuário faz um pedido → pedido vai para a fila → worker processa
- Upload de arquivo → fila dispara conversão/processamento
- API recebe requisição → responde rápido → processamento ocorre depois

---

## AWS SNS (Simple Notification Service)

O **SNS** é o serviço de **mensageria / pub-sub** da AWS.

### Características principais
- Baseado em **tópicos**
- É necessário que os **subscribers** estejam inscritos em um tópico
- Uma mensagem pode ser enviada para vários destinos ao mesmo tempo

### Tipos de Subscribers
- E-mail
- SMS
- HTTP/HTTPS
- SQS
- Lambda

### Casos de Uso Comuns
- Notificações em tempo real
- Alertas de sistema
- Integração entre múltiplos serviços
- Fan-out de mensagens

### Exemplos práticos de uso de mensageria
- Evento de pagamento aprovado → notifica financeiro, estoque e e-mail
- Alerta de falha em serviço → envia notificação para o time
- Evento em sistema → dispara múltiplos processos em paralelo

---

## Diferença entre SQS e SNS

| SQS | SNS |
|----|----|
| Modelo de fila | Modelo pub/sub |
| Uma mensagem para um consumidor | Uma mensagem para vários subscribers |
| Processamento assíncrono | Notificação e distribuição |
| Ideal para jobs | Ideal para eventos e alertas |
