# AWS IoT Core

O **AWS IoT Core** é um serviço gerenciado da AWS que permite conectar **dispositivos IoT (Internet of Things)** à nuvem AWS de forma segura e escalável.

---

## Visão Geral

O IoT Core facilita a conexão de dispositivos inteligentes à AWS, permitindo que eles:
- Enviem dados para a nuvem
- Recebam comandos e atualizações
- Interajam com outros serviços AWS
- Sejam gerenciados de forma centralizada

---

## Características Principais

- **Conectividade de Dispositivos**
  - Suporte a milhões de dispositivos simultâneos
  - Protocolos: MQTT, HTTP, WebSockets
  - Conexão segura com TLS/SSL

- **Device Shadow**
  - Representação virtual do estado do dispositivo
  - Permite interação mesmo quando dispositivo está offline
  - Sincronização automática quando reconecta

- **Rules Engine**
  - Processa mensagens dos dispositivos
  - Roteia dados para outros serviços AWS
  - Transforma e filtra dados em tempo real

- **Integração com Serviços AWS**
  - **Lambda**: Processamento de dados
  - **S3**: Armazenamento de dados
  - **DynamoDB**: Banco de dados
  - **Kinesis**: Streams de dados
  - **SNS/SQS**: Notificações e filas

- **Segurança**
  - Certificados X.509
  - Políticas de segurança granulares
  - Autenticação e autorização

---

## Casos de Uso Comuns

- **Carros Conectados**
  - Telemetria de veículos
  - Monitoramento de performance
  - Atualizações over-the-air

- **Dispositivos Domésticos Inteligentes**
  - Geladeiras, TVs, termostatos
  - Assistentes de voz
  - Sistemas de segurança

- **Cidades Inteligentes**
  - Sensores de tráfego
  - Monitoramento ambiental
  - Iluminação pública

- **Indústria 4.0**
  - Monitoramento de máquinas
  - Manutenção preditiva
  - Automação industrial

---

## Benefícios

- **Escalabilidade**: Suporta milhões de dispositivos
- **Segurança**: Criptografia e autenticação robustas
- **Confiabilidade**: Alta disponibilidade e durabilidade
- **Integração**: Conecta facilmente com outros serviços AWS
- **Custo-Efetivo**: Paga apenas pelo que usar

---

## Quando Usar AWS IoT Core

- Quando você tem dispositivos IoT que precisam se conectar à nuvem
- Para projetos de carros conectados ou veículos inteligentes
- Em sistemas de automação residencial ou industrial
- Para coletar dados de sensores em tempo real
- Quando você precisa gerenciar e monitorar dispositivos remotamente
